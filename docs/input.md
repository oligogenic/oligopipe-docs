The variant input
=================
As command-line argument:
```bash
Variant input:
  -vcf VARIANTS_VCF, --variants-vcf VARIANTS_VCF
                        The patient's VCF file, can be compressed.
  -tsv VARIANTS_TSV, --variants-tsv VARIANTS_TSV
                        Tab-delimited text file containing the patient's variants to analyse (chrom/pos/ref/alt/zygosity).
  -hg {hg19,hg38}, --genome-build {hg19,hg38}
                        The genome assembly to which the positions of your variants correspond.
  -s patient_sex, --patient-sex patient_sex
                        The sex of the patient (defaults to U = undetermined).
```
In the config YAML:
```yaml
patient_info:
   # possible values: M, F, U (undetermined) or empty
  sex:

variant_input:
  # choose one of both input types
  vcf_file:
  tsv_file:
  genome_build:   # hg19 or hg38
```

`oligopipe` accepts a list of variants from a single individual only, as it creates all possible variant combinations 
between pairs assuming that these belong to the same individual.

You can provide either Single Nucleotide Variants (SNVs) or small insertions/deletions (indels).


Types of input files
--------------------

There are two different types of variant input that you can use to upload your data: either a [variant list](#delimitedfile) or a [VCF file](#vcffile).

### 1. Tab-delimited variant list

Each line should contain **tab- or space-delimited** information for one variant, in the corresponding order:
**chromosome, position, reference allele, alternative allele, zygosity**. 

The zygosity values should be either '**Heterozygous**' or '**Homozygous**'. During the analysis, `oligopipe` automatically converts X-linked variants in males as Hemizygous.

No headers are needed.

### 2. VCF file


Alternatively, you can submit a VCF file (version 4.2) with your variants.
> **NOTE:** The file can also be compressed either with **zip, gzip, bzip2** or **xz**.

`oligopipe` requires as minimum the presence of:

* the **#Header Line**: #CHROM POS ID REF ALT etc... 
      

* the columns **CHROM, POS, ID, REF, ALT, FORMAT, SAMPLE_NAME** (patient information column containing values corresponding to the FORMAT field).  
      
    
* the **genotype (GT)** field for each variant at the FORMAT and SAMPLE_NAME columns. We use GT to define the zygosity of the variant and to pick the correct alternative allele if there are multiple ones (separated by commas) in ALT.  
    In case variants with GT: 0/0 ; 0|0 ; ./. ; . are present, these are discarded from the analysis. Allele combinations only consisting of alternative alleles (e.g. GT: 1/2 or 3/2) are handled as two separate heterozygous variants.

Any other meta-information lines on the top of the file or any extra columns and fields (e.g. QUAL, INFO, etc.) can be present, but `oligopipe` will ignore them.

> **NOTE:** if your VCF contains information for **several individuals**, you should separate the information of each individual in **different VCF files** and run them individually.

You can also download test VCFs to use with `oligopipe` from the [ORVAL input page](https://orval.ibsquare.be/input).

Variant types
-------------

You can either submit **Single Nucleotide Variants (SNVs)** or **small insertions/deletions (indels)**. Other types of variants (e.g. CNVs) can be present in your list, but they will not be included in the analysis.

Specifically for indels, you can submit your variants in either one of the two different ways that are shown for a particular variant example (the VCF file can contain more columns).

  

|     | Tab-delimited list | VCF file |
| --- | --- | --- |
| Example with dashes | 16 3254468 CTT - Heterozygous | 16 3254468 . CTT - PASS GT 1/0 |
| Example without dashes | 16 3254467 CCTT C Heterozygous | 16 3254467 . CCTT C PASS GT 1/0 |

Genome version
--------------

At the moment `oligopipe` accepts and annotates variants using either the **GRCh37/hg19** or the **GRCh38/hg38** human genome assembly.

We do not make conversions of genomic coordinates from different genome versions. In case you need to convert your variants, you are encouraged to use tools like the [UCSC](http://genome.ucsc.edu/cgi-bin/hgLiftOver), [Ensembl](https://www.ensembl.org/Homo_sapiens/Tools/AssemblyConverter?db=core) and [NCBI](https://www.ncbi.nlm.nih.gov/genome/tools/remap) assembly converters.

Patient information
-------------------

Except from the variant list, you should also provide (if available) the sex information of the patient, i.e. if the person is a **male** (M) or a **female** (F).

`oligopipe` handles differently X-linked variants in males (**hemizygous** variants) compared to females, and therefore this information is important in order to provide better predictions.
