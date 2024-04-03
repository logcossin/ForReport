# BUSCO analysis summary

* Data used for analysis: *Limosilactobacillus fermentum* 200 RefSeq genomes (Downloaded 24/03/25)
* Used BUSCO analysis lineages: Bacteria, Lactobacillales (Lactic Acid Bacteria) with default parameters

Dataset | Bacteria | Lactobacillales
---- | ---- | ----
Total genes | 124 | 402
Fully Complete | 71 | 212
Contain Duplicated | 4 | 4
Contain Fragmented | 13 | 27
Contain Missing | 28 | 118
Contain More than 2 | 8 | 41

* Fully Complete: all analyzed genomes have complete BUSCO gene
* Contain XXX: at least one genome have XXX BUSCO gene
* Contain More than 2: more than 2 incomplete BUSCO gene statuses were found in genomes

# ANI analysis

![image](https://github.com/logcossin/ForReport/assets/49052882/5e7d0101-2693-4be8-a700-7bac4ec3e428)

* ANI analysis was performed using [pyani](https://github.com/widdowquinn/pyani) with default parameters
* *L. fermentum* genomes were mainly clustered into 4 groups
* Most of the genomes (157) were inside group 1 and 2 (>99% identity)
* Group 3 genomes (34) had 92~94% CheckM completeness
* Group 4 genomes (9) had 88~91% CheckM completeness and fragmented genome sequence (>100 contigs)
