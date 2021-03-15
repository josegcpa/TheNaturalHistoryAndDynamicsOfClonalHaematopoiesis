# The Natural History of Clonal Haematopoiesis

## Motivation

This is the repository for [The Natural History of Clonal Haematopoiesis](). In this work, we investigate the fitness differences between genes, sites and individual clones using longitudinal sequencing data from >300 individuals between 54 and 103 years old.

## Code map

### Requirements

#### Software

* `R` 3.6.3 - other versions may work, but this was the version it was tested on
* `Rstudio` - to run the R notebooks
* `clonex` - a multi-purpose and efficient implementation of Fisher-Wright simulations. Available [here](https://github.com/josegcpa/clonex)

#### R library

`reticulate`,`greta`,`ggplot2`,`ggpubr`,`tidyverse`,`bayesplot`,`openxlsx`,`gtools`,`cowplot`,`ggsci`,`ggrepel`,`extraDistr`,`default`,`dendextend`,`ape`,`ggtree`,`grid`,`scatterpie`,`reghelper`,`phylodyn`,`survival`,`survminer`

### Accessing the analysis

1. [Estimating the technical overdispersion]()
2. [Validating this approach through Fisher-Wright simulations]()
3. [Growth rate coefficients and age at onset inference, possible associations with phenotype]()
4. [Investigating the historical growth effect and poor fits]()

### Running the analysis

*Please note that this entails installing your own version of `greta`, which is the package used for MCMC sampling, and the adequate alteration of paths in `vaf_dynamics_functions.R`*

*Please note this assumes that you are running this script from the root directory of this project*

*Notebooks with complete runs are already present above, but if one wants to run this locally the following steps can be taken:*

1. Technical overdispersion estimation
    1. Run `Notebook_Overdispersion.Rmd` (in `Rstudio`) - R notebook containing the overdispersion estimation from technical replicates.

2. Method validation (please note that, due to the stochastic nature of the simulations, results may difer slightly)
    1. Run `simulate_range.sh` (`sh simulate_range.sh`) - this will run a set of Fisher-Wright simulations with different driver fitness advantages and mutation rates. The `CLONEX_PATH` should be updated. As it is, the script will submit jobs to a LSF job scheduler - if no such job scheduler is available, one should adjust accordingly by removing the line containing `bsub`.
    2. Run `run_simulation.R` (`Rscript run_simulation.R`) - this will run the model that uses the Fisher-Wright simulations to validate our approach
    3. Run `Notebook_Simulations.Rmd` (in `Rstudio`) - R notebook containing the method validation using Fisher-Wright simulations

3. Data analysis - growth rate coefficient and age at onset inference, possible associations with phenotype
    1. Run `Scripts/run_model.R` (`Rscript Scripts/run_model.R`) - this runs the model that infers all growth rate coefficients
    2. Run `Notebook_GrowthCoefficients_AgeAtOnset_PossibleAssociations.Rmd` (in `Rstudio`) - this is the notebook containing the bulk of the analysis

4. Analysis of the historical growth effect and poor fits
    1. Run `Notebook_HistoricalGrowth_PoorFits.Rmd` (in `Rstudio`) - this runs analyses which factors - technical and biological - may be determinant of the difference between historical and inferred growth and a fit being poor (having one or more outlier)

5. Phylogenetic trees from single cell colonies, the determination of growth per year and age at onset from these trees and comparison with estimates from longitudinal data
    1. Run `Scripts/plot_tree.R` (`Rscript Scripts/plot_tree.R`) - this runs all of the aforementioned analysis and plots it as displayed in the manuscript

*Optional: run `Scripts/plots_for_initial_panel.R`*


