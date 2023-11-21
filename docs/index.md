# Oligopipe documentation

Click on a header on the panel above to get directed to the main sections of this documentation

## Summary


`oligopipe` is a Python package for the prediction  candidate disease-causing variant combinations, aiming to aid in uncovering the causes of **oligogenic diseases** (_i.e._ diseases caused by variants in a small number of genes). 
This tool integrates innovative **machine learning methods** for combinatorial variant pathogenicity prediction.

### What can you do with `oligopipe`?

SUBMIT AND FILTER YOUR VARIANTS

You can submit the variants of a single individual either as a [variant list](input.md##1-tab-delimited-variant-list) 
or a [VCF file](input.md#2-vcf-file).  
You can also [filter](preprocess.md#data-filtering) your variants based on their Minor Allele Frequency (MAF), their position in the gene and/or based on a specific gene panel of your choice.

PREDICT CANDIDATE DISEASE-CAUSING VARIANT COMBINATIONS

With `oligopipe` you can predict candidate pathogenic variant combinations in any gene pair present in your data with
[VarCoPP](varcopp.md).

  

>**NOTE:** The results of this pipeline are based on **predictive tools.** They are provided for research, educational and informational purposes only and the pathogenicity predictions should be subject to further scientific and clinical investigation.  
It is **not in any way** intended to be used as a substitute for professional medical advice, diagnosis, treatment or care.

* * *