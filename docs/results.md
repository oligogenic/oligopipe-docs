# Result files
When you launch a pipeline with `oligopipe`, it will show logs and write results to different files.
We offer a few options for managing those outputs. 


As command-line argument:
```bash
Output:
  -dir output_path, --outdir output_path
                        Output directory (defaults to working directory).
  -pre prefix, --prefix prefix
                        Optional prefix for the output files, use for example the patient ID.
  -f, --force           Force re-using an output directory, which may overwrite files.
  -v, --verbose         Show debug logs
  
  # For prioritize option only
  -N, --nb-top-ranked   The number of top-ranked combinations to retain (default = 100).
```
In the config YAML:
```yaml
output:
  dir:
  prefix:
```

Below is a description of the different result files.
## Results for every run
### Metadata

A JSON file containing metadata about the pipeline run:

* Inputs and input settings (filters, gene panel ...)
* Output statistics
    - Number of gene pairs
    - Number of variant combinations
    - Number of analysed variants, i.e. those that were **not discarded**

### Discarded variants
Variants can be discarded from the analysis [for different reasons](preprocess.md#variant-exclusion).

A .txt file is created with a list of variants for each of the following categories:

* Invalid zygosity
* Filtered out variants
* Missing variants; i.e. the CADD score for these variants is missing from our database.

    > NOTE:
    > If you can share your variant data, don't hesitate to [send us](mailto:oligopipe@ibsquare.be?subject=Missing%20variants) the variants with missing CADD score so that we can try to add them to our database.

## Prediction results
### Raw results
A JSON file `predictions_with_annotations.json` containing predictions as well as the annotated features for each variant, gene and variant combination.

### Gene pair table
The previous JSON is used to produce a table (`predicted_gene_pairs.tsv`) providing statistics on all gene pairs present in your data. 
The table contains the statistics on the percentage and number of pathogenic variant combinations for each pair, 
and the median pathogenic score provided by VarCoPP among combinations of that pair, to get an idea of their severity.  

For further explanations on how this pathogenicity score is calculated, you can consult the [VarCoPP](varcopp.md) section.

  
### Digenic combinations table
From the raw results we also create a table (`predicted_variant_combinations.tsv`) with all digenic variant combinations and their predictions.

## Prioritization results

### Raw results
A JSON file `predictions_with_annotations.json` containing predictions as well as the annotated features for each variant, gene and variant combination.

### Digenic combinations table
From the raw results we also create a table (`prioritized_variant_combinations.tsv`) with the top N digenic variant 
combinations and their scores and ranks.
