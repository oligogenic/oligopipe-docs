# VarCoPP2.0
> Via the `oligopipe predict` submodule

VarCoPP stands for Variant Combination Pathogenicity Predictor. It is a machine-learning method that predicts the 
pathogenicity of any bi-locus variant combination (i.e. a combination of two to four variant alleles between two genes).

The method has been published in the _PNAS_ journal: [https://doi.org/10.1073/pnas.1815601116](https://doi.org/10.1073/pnas.1815601116). 
The first version of the model was later improved to **VarCoPP2.0** using new training data, new features and a different type of model.
VarCoPP2.0 has been published in _BMC Bioinformatics_: [https://doi.org/10.1186/s12859-023-05291-3](https://doi.org/10.1186/s12859-023-05291-3). 

Based on VarCoPP, a bi-locus variant combination can either be **candidate disease-causing** or **neutral**.

VarCoPP has been trained separately for the **GRCh37/hg19** and **GRCh38/hg38** genome assembly, the correct model will run based on your assembly choice in the input.

> **NOTE:** The use of VarCoPP for the analysis of complete patient exomes is **NOT** recommended, as the method is not fine-tuned for exomes. 
> Please restrict your analysis to **relevant gene panels** for the disease of interest.
> If your VCF contains the complete exome of an individual, you can pass it to `oligopipe predict` as it is, and use the **Variant Filtering** and **Gene Filtering** options.
>
> Alternatively, you can run a HOP prioritization analysis on a complete exome using `oligopipe prioritize` (see [HOP](hop.md)).

## Structure of VarCoPP

**ALGORITHM**

VarCoPP2.0 is a **Balanced** [Random Forest (RF)](https://en.wikipedia.org/wiki/Random_forest) predictor that consists of 400 decision trees.

**TRAINING DATA**

The VarCoPP2.0 predictor has been trained on the pathogenic variant combinations present in the [Oligogenic Diseases Database (OLIDA)](http://olida.ibsquare.be/) against a large subset of variant data derived from control individuals of the [1000 Genomes Project (1KGP)](http://www.internationalgenome.org/).

The variant types that were used for training were the same for both OLIDA and 1KGP: exonic and splicing variants of up to 3.5% MAF, while all genes were protein coding genes.

**RESULT CALCULATION**

VarCoPP2.0 outputs a **VarCoPP score**, i.e. the probability (value between 0 and 1) that a variant combination belongs to the disease-causing class. If this probability is above 0.50 (hg19) or 0.4575 (hg38), the model predicts that the combination is disease-causing.

## Prediction features

VarCoPP uses different variant, gene and gene pair biological features to make the predictions.

| Feature | Source | Feature abbreviation | Gene / Variant allele |
| --- | --- | --- | --- |
| CADD raw score  <br>PMID: [24487276](https://pubmed.ncbi.nlm.nih.gov/24487276/) | CADD v1.6 | CADD1  <br>CADD2  <br>CADD3  <br>CADD4 | Gene A / Variant allele 1  <br>Gene A / Variant allele 2  <br>Gene B / Variant allele 1  <br>Gene B / Variant allele 2 |
| Gene haploinsufficiency prediction  <br>PMID: [28137713](https://pubmed.ncbi.nlm.nih.gov/28137713/) | dbNSFP v4.1 | HIPred_A  <br>HIPred_B | Gene A  <br>Gene B |
| Inheritance specific pathogenicity prediction  <br>for autosomal dominant (AD),  <br>autosomal recessive (AR),  <br>and X-linked (XL) modes of inheritance  <br>PMID: [27354691](http://pubmed.ncbi.nlm.nih.gov/27354691/) | [publication  <br>supplementary  <br>data](http://pubmed.ncbi.nlm.nih.gov/27354691/) | ISPP\_AD\_A  <br>ISPP\_AD\_B  <br>ISPP\_AR\_A  <br>ISPP\_AR\_B  <br>ISPP\_XL\_A | Gene A  <br>Gene B  <br>Gene A  <br>Gene B  <br>Gene A |
| Selective pressure (dN/dS)  <br>PMID: [26896847](https://pubmed.ncbi.nlm.nih.gov/26896847/) | Ensembl v99 | dN\_dS\_A | Gene A |
| Biological distance  <br>PMID: [24694260](https://pubmed.ncbi.nlm.nih.gov/24694260/) | Human Gene  <br>Connectome  <br>v12.2015 | Biol_Dist | Gene pair AB |
| Biological Process similarity  <br>PMID: [10802651](http://pubmed.ncbi.nlm.nih.gov/10802651/), [18460186](http://pubmed.ncbi.nlm.nih.gov/18460186/) | Gene Ontology  <br>v2021-12 | BP_sim | Gene pair AB |
| Distance in an in-house developed Knowledge Graph  <br>PMID: [37644440](https://pubmed.ncbi.nlm.nih.gov/37644440/) | [BOCK  <br>v1.0](https://doi.org/10.5281/zenodo.7185680) | KG_dist | Gene pair AB |

## Confidence zones

With VarCoPP2.0 we have defined 99% and 99.9%confidence zones, delimited by the prediction threshold, which provide a **probability** of whether a particular combination predicted as candidate disease-causing, is actually a **True Positive (TP) result**. This indication can be useful for further evaluation and filtering of the predictions.

These confidence zones were created by testing neutral bi-locus combinations from the 1000 Genomes Project and obtaining the minimal prediction probability that gave 1% and 0.1% False Positives respectively. If a combination falls into either one of the two zones, a coloured indication will appear in the summary results.

  
**99%-confidence zone**

Requires VarCoPP score ≥ 0.743 (hg19) or ≥ 0.647 (hg38). If a digenic combination falls inside this zone, it has 99% probability of being a TP result.

  
**99.9%-confidence zone**

Requires VarCoPP score ≥ 0.891 (hg19) or ≥ 0.85 (hg38). If a digenic combination falls inside this zone, it has 99.9% probability of being a TP result.

