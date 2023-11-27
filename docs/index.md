# Oligopipe documentation

> Click on a header on the panel above to get directed to the different main sections of this documentation

[oligopipe](https://pypi.org/project/oligopipe/) is a Python package for the discovery of **candidate disease-causing variant combinations**, aiming to aid in 
uncovering the causes of **oligogenic diseases** (_i.e._ diseases caused by variants in a small number of genes). 
This tool integrates innovative **machine learning methods** for combinatorial variant pathogenicity prediction developed
at the [Interuniveristy Institute of Bioinformatics in Brussels](https://ibsquare.be).

It is available as a **CLI** that takes arguments (see `--help`) either directly or via a YAML configuration file.

### What can you do with `oligopipe`?
The CLI tool currently contains three modules:

```bash
Commands:
  Run oligopipe {command} -h to get detailed help

  {predict,prioritize,config}
    predict             Run a VarCoPP prediction
    prioritize          Run a prioritization analysis with HOP -- under construction
    config              Show the template config file
```

The **PREDICT** and **PRIORITIZE** modules both [take in your variant data](input.md), 
[preprocess](preprocess.md) it according to your submitted settings, and either [predict with VarCoPP](varcopp.md) 
or [prioritize with HOP](hop.md) the candidate pathogenic variant combinations in any gene pair.

With **CONFIG** you can show a template for the input config YAML which can be used instead of / in combination with 
the command-line arguments. The latter will always get priority if both are given for a specific argument.
  
### Important note
The results of these pipelines are based on **predictive tools.** They are provided for research, 
educational and informational purposes only and the pathogenicity predictions should be subject to further scientific and clinical investigation.  
It is **not in any way** intended to be used as a substitute for professional medical advice, diagnosis, treatment or care.
