# GSEA
R code for running a gene set enrichment analysis using missMethyl

## Install and load missMethyl
```r
source("https://bioconductor.org/biocLite.R")
biocLite("missMethyl")
biocLite("IlluminaHumanMethylation450kanno.ilmn12.hg19")
biocLite("GO.db")
install.packages("BiasedUrn")

library(limma)
library(minfi)
library(missMethyl)
library(IlluminaHumanMethylation450kanno.ilmn12.hg19)
```
## Load the data
You need 2 character vectors:
1) your list of top CpGs:
```r
mylist<-read.csv("/Volumes/gs8094/Documents/IEU work/AFAST/afast_dmrs/Mod1_DMRs_sig.csv", stringsAsFactors==FALSE)
mylist <- mylist$CPG.Label
```
2) a list of all CpGs on the array:
```r
load("\\ads.bris.ac.uk\filestore\MyFiles\Staff17\gs8094\Documents\work\ieu\data\useful_info_for_ewas/fdata_new.RData")
allcpgs <- fdata.new$TargetID
```
## Look for gene ontology (GO) term enrichment
```r
go.res <- gometh(sig.cpg=mylist, all.cpg=allcpgs, collection="GO")
topGO(go.res)
```
## Look for KEGG pathway enrichment
```r
kegg.res <- gometh(sig.cpg=mylist, all.cpg=allcpgs, collection="KEGG")
topGO(kegg.res)
```
