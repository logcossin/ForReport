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
* Contain More than 2: more than 2 defect BUSCO gene statuses were found in genomes

# Incomplete BUSCO gene analysis

* Genomes with BUSCO completeness over 99% were filtered for further analysis
* Bacteria (105 genomes, 53 genes), Lactobacillales (148 genomes, 190 genes)

## Lactobacillales lineage

* 3 genes were analyzed as incomplete (Fragmented + Missing) in more than 2% of the 148 genomes

Gene | Incomplete genomes
---- | ----
ADP-dependent (S)-NAD(P)H-hydrate dehydratase (42919at186826) | 3
Dihydrofolate reductase (61889at186826) | 128
Glucose-6-phosphate isomerase (7599at186826) | 36

----
* ADP-dependent (S)-NAD(P)H-hydrate dehydratase gene is incomplete in strains SRCM103285 (GCF_004063515.1), KMB_612 (GCF_003346325.1), KMB_613 (GCF_003346315.1)
1. The gene is defined as pseudogene because of partial gene sequence and missing C-terminus in SRCM103285
2. The genes are 193 and 195 aa in KMB_612 and KMB_613, respectively. Which is much shorter than median protein length (280 aa).

![image](https://github.com/logcossin/ForReport/assets/49052882/b33e8895-de26-472c-ae18-5879559d6cdc)
![image](https://github.com/logcossin/ForReport/assets/49052882/81673fa7-44b0-4991-9a1c-f58b85058a3a)

The gene is located and separted into two contigs. Both genomes are consisted of more than 100 contigs.

# ANI analysis

![image](https://github.com/logcossin/ForReport/assets/49052882/5e7d0101-2693-4be8-a700-7bac4ec3e428)

* ANI analysis was performed using [pyani](https://github.com/widdowquinn/pyani) with default parameters
* *L. fermentum* genomes were mainly clustered into 4 groups
* Most of the genomes (157) were inside group 1 and 2 (>99% identity)
* Group 3 genomes (34) had 92~94% CheckM completeness
* Group 4 genomes (9) had 88~91% CheckM completeness and fragmented genome sequence (>100 contigs)
