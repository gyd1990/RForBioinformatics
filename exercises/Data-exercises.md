


# Some R data manipulation and plotting exercises

We are going to use a few small datasets to practice our R skills and see what we can learn about the datasets themselves.  These exercises are meant to let you explore and I do not provide answers for all exercises.  You can discuss with your colleagues and with instructors.  Not all exercises have only one best answer.

## Iris data

The _Iris_ data represent the famous (Fisher's or Anderson's) iris data set gives the
measurements in centimeters of the variables sepal length and
width and petal length and width, respectively, for 50 flowers
from each of 3 species of iris.  The species are _Iris setosa_,
_versicolor_, and _virginica_.

To get started, we can load the data using:


```r
data(iris)
```

1\. Use your R skills to learn a little about the size and structure of the iris data.  Consider using `head`,`tail`,`dim`,`nrow`,`class`.



2\. Get some summary statistics for the dataset.  Consider tools like `summary`, `mean`, `median`, `sd`, `IQR`. 



3\. Use some plots to investigate the relationships between the variables.



4\. Quantify the relationships between the quantitative variables.



5\. Bonus: Use the randomForest package to predict the flower species based on the data.



 
## Ensembl Genes using biomaRt

### Background

In recent years a wealth of biological data has become available in public
data repositories. Easy access to these valuable data resources and firm
integration with data analysis is needed for comprehensive bioinformatics
data analysis. The biomaRt package, provides an interface to a growing
collection of databases implementing the BioMart software suite (http://
www.biomart.org). The package enables retrieval of large amounts of data
in a uniform way without the need to know the underlying database schemas
or write complex SQL queries. Examples of BioMart databases are Ensembl,
Uniprot and HapMap. These major databases give biomaRt users direct
access to a diverse set of data and enable a wide range of powerful online
queries from R.

In this exercise, we are going to use the [biomaRt Bioconductor package](`biocurl('biomaRt')`) to get a 
dataset with biologically-related data to play with using the dplyr and ggplot2 
packages.

### Getting started

The biomaRt package is a Bioconductor package, so we need to install it before we can use it.


```r
source('http://bioconductor.org/biocLite.R')
biocLite('biomaRt')
```

Before we can use the package, we need to actually load it into our R session.


```r
library(biomaRt)
```

### Connecting to a biomaRt

The next step is to connect to a Biomart database.  While this looks a little magical, the biomaRt vignette shows examples and the help pages can be used to get details on how to do this.  In this case, I'll simply supply the code for you.


```r
ensembl = useMart("ensembl",dataset="hsapiens_gene_ensembl")
```

### Executing the Biomart Query

While biomaRt can be used for many purposes, we are using it here as an easy way to get information about genes. I want to get the following information back from biomart:

- Ensembl Gene ID
- HUGO Gene Symbol
- Gene Description
- Number of transcripts
- chromosome
- strand
- GC %
- Gene type
- Status (novel or known)
- phenotype description

Again, we'll simply use the code below.  The details can be sought from the documentation.


```r
genes = getBM(mart=ensembl,attributes=c("ensembl_gene_id",
                                         "description",
                                         "chromosome_name",
                                         "strand",
                                         "percentage_gc_content",
                                         "transcript_count",
                                         "gene_biotype",
                                         "status",
                                         "hgnc_symbol",
                                         "phenotype_description"))
```

- Exercise: Investigate the structure of the `genes` object using functions such as `class`, `dim`, `colnames`, `summary`, etc.
- Exercise: What is the range of the `percentage_gc_content`? How could you visualize this range of values effectively?

- Exercise: What are the possible categories for the `gene_biotype` column?  How many genes fall into each category?

- Exercise: Filter the `genes` data to include only those on the positive strand.

- Exercise: Use `ggplot2` to make a boxplot of GC content for each different type of `gene_biotype`.


## Behavioral Risk Factor Surveillance System

You have been given a dataset that represents basic measurements of people over time.  Explore the data interactively to learn about trends or other features of interest in the data.  

To load the data:


```r
brfss = read.csv("http://watson.nci.nih.gov/~sdavis/tutorials/IntroToR/BRFSS-subset.csv")
```

- Exercise: Explore the data in any way that you like, including plots, summaries, and data manipulations.  
- Exercise, create a function that takes a vector of weights (in kg) and heights (in cm) and returns the Body Mass Index (BMI). 

http://www.cdc.gov/healthyweight/assessing/bmi/adult_bmi/index.html#Interpreted


# Session Info

```r
sessionInfo()
```

```
## R version 3.2.1 (2015-06-18)
## Platform: x86_64-apple-darwin13.4.0 (64-bit)
## Running under: OS X 10.10 (Yosemite)
## 
## locale:
## [1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8
## 
## attached base packages:
## [1] stats4    parallel  stats     graphics  grDevices utils     datasets 
## [8] methods   base     
## 
## other attached packages:
##  [1] biomaRt_2.23.5           randomForest_4.6-10     
##  [3] gplots_2.16.0            ShortRead_1.25.8        
##  [5] GenomicAlignments_1.3.28 Rsamtools_1.19.35       
##  [7] GenomicRanges_1.20.3     GenomeInfoDb_1.3.13     
##  [9] Biostrings_2.35.11       XVector_0.7.4           
## [11] IRanges_2.2.1            S4Vectors_0.6.0         
## [13] BiocParallel_1.1.13      BiocGenerics_0.14.0     
## [15] nycflights13_0.1         ggplot2_1.0.1           
## [17] BiocStyle_1.5.3          knitr_1.8               
## [19] Rgitbook_0.9            
## 
## loaded via a namespace (and not attached):
##  [1] gtools_3.4.1         reshape2_1.4         knitcitations_1.0.6 
##  [4] lattice_0.20-31      colorspace_1.2-4     base64enc_0.1-2     
##  [7] XML_3.98-1.1         DBI_0.3.1            RColorBrewer_1.0-5  
## [10] foreach_1.4.2        plyr_1.8.1           stringr_0.6.2       
## [13] zlibbioc_1.13.1      munsell_0.4.2        gtable_0.1.2        
## [16] hwriter_1.3.2        caTools_1.17.1       codetools_0.2-11    
## [19] memoise_0.2.1        evaluate_0.5.5       labeling_0.3        
## [22] latticeExtra_0.6-26  Biobase_2.27.1       AnnotationDbi_1.30.1
## [25] proto_0.3-10         Rcpp_0.11.6          KernSmooth_2.23-14  
## [28] scales_0.2.4         checkmate_1.5.0      formatR_1.0         
## [31] gdata_2.13.3         sendmailR_1.2-1      brew_1.0-6          
## [34] BatchJobs_1.5        fail_1.2             digest_0.6.8        
## [37] BBmisc_1.8           RJSONIO_1.3-0        grid_3.2.1          
## [40] bibtex_0.4.0         tools_3.2.1          bitops_1.0-6        
## [43] RCurl_1.95-4.3       RSQLite_1.0.0        RefManageR_0.8.63   
## [46] MASS_7.3-40          lubridate_1.3.3      httr_0.6.1          
## [49] iterators_1.0.7
```



