Frequently Asked Questions
==========================

If answers to your questions are not provided in this section and no information about your question is mentioned in the Documentation page, you can [contact us](mailto:oligopipe@ibsquare.be).

## General FAQ
**Can I include variants from multiple patients in my input?**  
**No**, the analysis should be **restricted to a single individual only**, as `oligopipe` creates all possible variant combinations from your variant list assuming that they belong to the same person.  
If you want to analyse multiple patients, you should separate their variants in different files and explore them individually.
*** 
**Is there a specific input format for the insertions and deletions?**  
`oligopipe` accepts different types of variant format for the insertions and deletions, involving dashes or not.  
You can consult the [Variant Types](input.md#variant-types) section for a detailed explanation.
*** 

**What types of digenic combinations does `oligopipe` create?**  
`oligopipe` creates all possible di-allelic, tri-allelic and tetra-llelic variant combinations between any gene pair present in your data, including heterozygous compound variants in one of the two genes. Tetra-llelic combinations with four heterozygous variants (two in each gene) are not created, as these combinations were absent from our training set.  
For a detailed explanation, you can consult the [Creating digenic combinations](preprocess.md#creating-digenic-variant-combinations) section.
***

**Not all of the expected output files are generated, since no variant combinations are left after preprocessing. What should I do?**  

You can check the following steps to explore possible solutions:

* Check whether the selected genome version is correct. `oligopipe` can annotate variants using the **GRCh37/hg19 or GRCh38/hg38 genome version**, see the [Genome version](input.md#genome-version) section for more details.
* Try to relax your variant or gene filtering options, especially the option for keeping intronic and synonymous variants.
* Ensure that you have more than one gene present in your data. `oligopipe` makes variant combinations between **gene pairs**, so it requires the presence of at least two different genes in your data.
* If you have submitted a small number of variants, these variants may have been excluded from the analysis during the annotation process. For example, the CADD score for those variants may be missing, and as this score is important for the predictions, variants without an annotated CADD score are excluded from the analysis. A detailed list of all possible cases where your variants may be excluded is presented in the [Variant Exclusion](preprocess.md#variant-exclusion) section.

If you have checked the previous steps and you still experience issues, you can [send us an email](mailto:oligopipe@ibsquare.be).
***
**SOME variants of my initial submission are missing from the results**  

* Please check the variant and/or gene filtering options you have selected during your submission, as these play an important role on the absence of some of your variants in the analysis. The variant filtering options offered by `oligopipe` are **automatically pre-selected** during the submission, unless you unselect them.
* Make sure that the variant information and format you provided is correct for all variants. In case you copy-pasted a variant list using the box panel, make sure that the zygosity values are not misspelled (**Heterozygous** or **Homozygous** zygosity values are accepted), see also the [tab-delimited variant list](input.md#1-tab-delimited-variant-list) section.
* Otherwise, some variants may have been excluded from your analysis during the data annotation process. You can consult the [Variant Exclusion](preprocess.md#variant_exclusion) section for a detailed description of such cases.

  
For more information regarding our filtering options and the data annotation process, you can consult the [Data Filtering and Annotation](preprocess.md) section.
***
**I am pretty sure that a variant is supposed to be mapped to a specific gene (according to my knowledge or the gene panel I provided), but I see another gene name instead in the results.**  

This can happen for the following reasons:

* The gene symbol present at the gene panel file is not the official HGNC gene symbol. During annotation we only use the official HGNC gene symbols, and thus, we will display this symbol instead of the one that you provided.
* The position of the variant for that gene overlaps with other genes. In this tricky situation, we have to choose one gene to continue with predictions. We have developed a set of priority rules for that (see the [Gene annotation](preprocess.md#1-gene-annotation) section). Therefore, there is a chance that we have assigned this variant to another gene instead. Unfortunately, it is not possible to re-assign it to your favourite gene manually and we can potentially do changes in our database for that only during major `oligopipe` updates. Please note that **you shouldn't change that gene name for the variant in the results, as some prediction features are gene-specific**.  
    If you think that this mapping is definitely wrong, you can [send us an email](mailto:oligopipe@ibsquare.be).

## Specific to prediction with VarCoPP
**Is there a limit on the number of variants I can analyse?** 

In general, we **highly recommend** the use of variants from up to **300 genes**, as well as the application of the [variant filtering procedure](preprocess.md#1-variant-filtering) that is provided with `oligopipe`, in order to limit the amount non-relevant combinations that will be tested.  
  
***
## Specific to prioritization with HOP