# Hop
> Via the `oligopipe prioritize` submodule

Hop stands for the High-throughput oligogenic prioritizer. It is a prioritization tool which, given a patients' WES
data and information about the patient's disease (encoded as phenotypic terms, a list of candidate genes for the disease,
or both), outputs a ranking of bi-locus variant combinations which are the most likely to cause the disease. 

The method has been published in _Bioinformatics_: [https://doi.org/10.1093/bioinformatics/btae184](https://doi.org/10.1093/bioinformatics/btae184).

## Structure of Hop

**METHOD**

Hop assigns each variant combination three scores: a Pathogenicity Score (PS), 
a Disease-relevance Score (DS) and a Final Score (FS). The Final Score is used to rank all
variant combinations in the exome in decreasing order (i.e. the first ranked combination is the combination with the highest FS).

**PATHOGENICITY SCORING**

The PS is obtained from the VarCoPP2.0 predictor, which assigns bi-locus combinations a value between 0 and 1
which corresponds to the probability that the combination is disease-causing. For a complete description of this predictor 
see [VarCoPP](varcopp.md). 

**DISEASE-RELEVANCE SCORING**

The DS is computed using a Random-Walk-with-Restart (RWR) algorithm in a knowledge graph. 
The knowledge graph used is the Biological networks and Oligogenic Combinations integrated as a Knowledge graph (BOCK), and includes biological databases and ontologies which were deemed relevant for the study 
of oligogenic diseases. More information on BOCK and the data sources can be found in the following article: [https://doi.org/10.1186/s12859-023-05451-5](https://doi.org/10.1186/s12859-023-05451-5). 

The RWR algorithm starts from a set of seed nodes and outputs a score for each node in the network which can be interpreted 
as a proximity score of the node to the set of seeds. In Hop, the seed nodes can be the HPO terms describing the patient's phenotype,
genes belonging to a gene panel associated with the patient's disease or both types of information. 
From these seeds, the RWR algorithm is used to score the proximity of all human genes. 
The Disease-relevance Score of a gene pair is then computed as the mean of the individual gene proximity scores. 

**FINAL SCORING**

The PS and DS are normalized exome-wide using min-max normalization to ensure equal weight of the PS and DS. Then the 
Final Score is computed as the average of the PS and DS. The combinations are ranked in descending order, so that the 
combination with the highest Final Score is ranked first. 

## Important note and implementation

Since Hop runs on all possible combinations in a provided VCF, this can lead to a large number of combinations to be 
predicted. In order to focus on the most relevant combinations, it is therefore implemented to only output the top N 
combinations, with `N` being a parameter that is specified by the user and defaults to 100. It is important to not use a 
too large value of N as it can lead to memory issues. 

To not keep all variant combinations in an exome in memory, Hop is therefore implemented to compute the scores of all 
possible variant combinations iteratively, and to only keep in memory the top N combinations. 
