# AnnotSV_benignAF_annotation
This repository introduced new annotation function added in AnnotSV since v3.1.3 version, now Taiwania3 had update to v3.2.2(latest version).

## AnnotSV official GitHub page and manual pdf link:
https://github.com/lgmgeo/AnnotSV.    
https://lbgi.fr/AnnotSV/Documentation/README.AnnotSV_latest.pdf.   

## Allele frequency data set and annotation threshold
### Database resources and input criteria
AnnotSV collected allele frequency from following database or studies:
* gnomAD
* ClinVar
* ClinGen
* DGV Gold Standard
* DDD
* 1000 genomes
* Ira M. Hall’s lab
* Children’s Mercy Research Institute 

AnnotSV divided SVs into four types: gain / loss / INS / INV ,which is based on their function effect or type.   
Finally, they combined all of the original databaseID, coordinate and allele frequency information into one bed file, which can be found in directories:      
```$ANNOTSV_PATH/share/AnnotSV/Annotations_Human/SVincludedInFt/BenignSV/GRCh37/```
```$ANNOTSV_PATH/share/AnnotSV/Annotations_Human/SVincludedInFt/BenignSV/GRCh38/```

Take ```benign_Gain_SV_GRCh37.sorted.bed``` file as an example:    
Column names are chromosome / start position / end position / databaseID / database coordinate / allele frequency

![截圖 2023-02-24 09 48 00](https://user-images.githubusercontent.com/87052008/221072049-76f86332-d0fc-44d1-a334-79eafe81184a.png)

### Annotation threshold
If query SVs had allele frequency annotation, they must meet the following conditions:
1. 100% overlapping breakpoint: To ensure the annotated variants had similar biological functional effect, query SVs need to have either exactly breakpoinot or breakpoint contain in database SVs, for example:      
* query SV: chr1_12345_12678 compare to database SV: chr1_12345_12678 --> exactly breakpoint --> AF annotation 
* query SV: chr1_12345_12678 compare to database SV: chr1_12300_12794 --> breakpoint contain in database SV --> AF annotation
* query SV: chr1_12345_12678 compare to database SV: chr1_12360_12490 --> partial overlap --> no AF annotation
* query SV: chr1_12345_12678 compare to database SV: chr1_12300_12659 --> partial overlap --> no AF annotation 

2. Benign allele frequency higher than threshold: Compare to pathogenic variants, benign variants may have higher allele frequency among population(tend to be common variant). AnnotSV defaultly set annotation threshold to be 0.01, which means that if query SV compare to one database record and also database AF is higher than 0.01 (=1%)(in default), it can have annotation output. If you want to change AF threshold, you can refer to option setting section. 

## Parameter/option setting and ouptut column interpretation
In default, AnnotSV can automatically include allele frequency annotation since v3.1.3. If you want to change annotation threshold, please add ```benignAF``` 
