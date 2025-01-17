# tRomics (!!! under development !!!)

<!-- badges: start -->
[![](https://img.shields.io/badge/doi-10.3390/ijms21134727-yellow.svg)](https://doi.org/10.3390/ijms21134727)
[![R CMD Check via {tic}](https://github.com/kapsner/tromics/workflows/R%20CMD%20Check%20via%20{tic}/badge.svg?branch=master)](https://github.com/kapsner/tromics/actions)
[![linting](https://github.com/kapsner/tromics/workflows/lint/badge.svg?branch=master)](https://github.com/kapsner/tromics/actions)
[![test-coverage](https://github.com/kapsner/tromics/workflows/test-coverage/badge.svg?branch=master)](https://github.com/kapsner/tromics/actions)
[![codecov](https://codecov.io/gh/kapsner/tromics/branch/master/graph/badge.svg)](https://codecov.io/gh/kapsner/tromics)
<!-- badges: end -->

`tRomics` is an R package that provides a Shiny web application for integrative *in silico* analysis for deciphering global transcriptome profiling data. It was developed as part of the publication "Integrative bioinformatics analyses of global transcriptome data decipher novel molecular insights into cardiac anti-fibrotic therapies" (Fuchs, Kreutzer et al.) which is currently under review in International Journal of Molecular Sciences. 

# Installation

You can install *tRomics* with the following commands in R:

```r
install.packages("remotes")
remotes::install_github("kapsner/tromics")
```
# Start shiny application

To start `tRomics`, just run the following command in R. A browser tab should open displaying the web application. Alternatively you can type the URL "localhost:3838/" in your browser.

To run the analyses, please click on the button *Load example data* on the web application's dashboard.

```r
library(tRomics)
launch_app()
```
# General information
Before you use this web application you should get familiar with the general functionality of the DESeq2 method (https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0550-8) since the whole analysis approach is based on it. Please check the vignette provided for DESeq2 (https://bioconductor.org/packages/release/bioc/vignettes/DESeq2/inst/doc/DESeq2.html), especially in terms of the correct design for your comparisons. This first version of the web application covers basic group comparisons. 

# Example files

The example files were created by Fabian Kreutzer and Jan Fiedler from IMTTS, MH Hannover. These example data are integrated into this web application and can there directly be loaded by clicking the button 'Load example data'.
The data are also available via this R package:  

* mRNA:
  - Count data: [count_data.csv](inst/example_data/count_data.csv)
  - Meta data: [metadata.csv](inst/example_data/metadata.csv)
* miRNA:
  - Count data: [miRNA_counts.csv](inst/example_data/miRNA_counts.csv)
  - Meta data: [miRNA_metadata.csv](inst/example_data/miRNA_metadata.csv)

# Exprected input file structure
* The app works based on two input files (Compare example file):
  - Countdata: a comma-separated text file that contains raw read counts. These files can be generated by raw read mapping with several established pipelines or packages such as RSubread. Each 
  line represents a gene   and the row names have to be Ensembl-IDs. Each column represents one         sample. 
  - Metadata: a comma-separated text file that contains information about the samples. Each row         contains the info for one sample and the rownames have to match the column names from the countdata   file. The columns can contain several information about the samples (e.g. treatment, donor, group).

# Data import
 
- Use the browse buttons to upload a csv-file containing metadata on the left and one file containing count data on the right. Progress bars will let you keep track of the upload process. It is also possible to use the example data provided within the web application by selecting one datatype and clicking "Load example data". Two RNA-Seq datasets are included in the app that contain raw read counts and sample data. For further information about the sample data and material and methods, please check the publication mentioned above.

- After successfully uploading your data you will be able to view it below the upload section for a final check.

- Next you have to select a variable your samples will be grouped by. That is usually a certain treatment or cell-type. In case of the provided datasets it's myocardial slices from the rat treated with different drugs and one control group. Each group has three replicates.
  
- Now you have to define the design formula. For more details on this task, please check the DESeq2 vignette.

- After confirming the design formula, press "Preprocess data". Now you have to decide the number of genes plotted in the heatmap. The web application automatically sorts the selected number of genes by variance, applies basic clustering and generates a heatmap with figure legend.
  
- After clicking the "Start analysis" button, you will be redirected to the Visualization tab, where the automatically generated plots for data exploration are shown. The plots are generated according to the standard approach taken from the DESeq2 vignette. Every plot can be downloaded in png-format using the buttons above each figure. Click "Start analysis" to continue

# Visualization

- After clicking the "Start analysis", you will be redirected to the "Visualization tab", where the automatically generated plots for data exploration are shown. The plots are generated according to the standard approach taken from the DESeq2 vignette. Every plot can be downloaded in png-format using the buttons above each figure. 

# DEG analysis
  
- To analyze your data for differential expression, use the navigation area on the upper left part to switch to the DEG analysis tab.

- All possible contrasts generated from your selected grouping variable are shown in the upper right corner. Select all needed objectives. Note that the sample group mentioned second in an comparison functions as the reference. This is important for interpreting the resulting lists.
  
- After selecting at least one comparison you can decide wether to add Entrez IDs and gene symbols to your result list. Please only check this box if you dataset is already annotated with ENSEMBL IDs without version numbers, otherwise this will cause an error withing the web application.

- Select the matching Annotation source for the organism included in your data. In case of the example data it is org.Rn.eg.db because it's rat data. Check documentation of the Annotation.Dbi package to make sure you select the right annotation package.
  
- Use "Start DEG analysis" to start.

- The web application will automatically return the calculated result list for DEG analysis as described in the documentations of DESeq2 function "results". You can either browse the list within the web application or download it in csv-format via the button above.
    
- A volcano plot of DEG results is also generated and can be saved with the button above.

# More Infos

- about CLEARLY: [https://www.transcanfp7.eu/index.php/abstract/clearly.html](https://www.transcanfp7.eu/index.php/abstract/clearly.html)
- about MIRACUM: [https://www.miracum.org/](https://www.miracum.org/)
- about the Medical Informatics Initiative: [https://www.medizininformatik-initiative.de/index.php/de](https://www.medizininformatik-initiative.de/index.php/de)
- about Shiny: https://www.rstudio.com/products/shiny/
- RStudio and Shiny are trademarks of RStudio, Inc.
