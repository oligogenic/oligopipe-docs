# Result files

After the analysis is finished, you will TODO

## Metadata

## Discarded variants

The Job summary shows the information that you submitted in the Input page: the ID and Sex of the patient, the filtering settings and the variant input. It also shows how many of your variants remained after the filtering and annotation (and were used for predictions).  
  
By clicking on "Details...", you can display a breakdown of the discarded variants. It shows how many variants had an **invalid zygosity**, were **filtered out**, or had a **missing CADD score**. For each of those categories, it is possible to download a list of the variants in .txt file.

  

If you can share your variant data, don't hesitate to [send us](mailto:oligopipe@ibsquare.be?subject=Missing%20variants) the variants with missing CADD score so that we can try to add them to our database.

## Prediction results
### Raw results

### Gene pair table

With this section you can explore the gene pairs that are present in your data and rank them based on the content of candidate disease-causing variant combinations that have been predicted with [VarCoPP](#varcopp).

todo example pair table

This information is shown in a **gene pair table** that provides statistics on all gene pairs present in your data. The table is divided into the statistics on the percentage and number of pathogenic variant combinations for each pair, and the pathogenic score provided by VarCoPP among combinations of that pair, to get an idea of their severity.  
For further explanations on how this pathogenicity score is calculated, you can consult the [VarCoPP](varcopp.md) section on this Documentation page.

The table is initially ranked based on the following columns in descending order of importance:

1.  percentage of pathogenic combinations
2.  VarCoPP Score

  
### Digenic combinations table

With this section you can explore the results of the **digenic pathogenicity predictions** of [VarCoPP](varcopp.md) for all digenic variant combinations of your data.

TODO

## Prioritization results