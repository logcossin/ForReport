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
* Contain More than 2: more than 2 defect BUSCO gene statuses were found to that marker gene

# Incomplete BUSCO gene analysis

* Genomes with BUSCO completeness over 98% (bacteria) and 99% (lactobacillales) were sampled for further analysis
* Bacteria (160 genomes, 53 genes), Lactobacillales (148 genomes, 190 genes)

## Bacteria lineage

* 2 genes were analyzed as incomplete (Fragmented + Missing) in more than 2% of the 160 genomes

Gene | Incomplete genomes
---- | ----
Ribosomal protein L35 (2046660at2) | 160
Chorismate synthase (981870at2) | 39

----
* Ribosomal protein L35 was fragmented in every 160 genomes analyzed
* The length of *L. fermentum* genes (65 aa) is the same as median bacterial gene length in [OrthoDB](https://v10-1.orthodb.org/?query=2046660at2).
* BUSCO marker gene completeness is assessed by HMM profile align scores and length and if found to be fragmented, the BUSCO matches have proper scores but not the alignment lengths to the BUSCO profile.
* The profile alignment length of genes (22 aa) is below the threshold (33 aa) to be defined as complete.

----
* Chorismate synthase (aroC) is analyzed missing in 39 genomes.
* All 39 genomes have the chorismate synthase pseudogene in result of frameshift, nonsense mutation.

![image](https://github.com/logcossin/ForReport/assets/49052882/392fcd0e-4b04-471c-aee9-362f6c10c3d8)

* Example of framshifted aroC gene in *L. fermentum* 779_LFER (GCF_001077025.1)

![image](https://github.com/logcossin/ForReport/assets/49052882/2af3aadd-18a4-497f-88da-40b2a2401214)

* Example of aroC gene in *L. fermentum* AF15-40LB (GCF_003464285.1) with internal stop codon

## Lactobacillales lineage

* 3 genes were analyzed as incomplete (Fragmented + Missing) in more than 2% of the 148 genomes

Gene | Incomplete genomes
---- | ----
ADP-dependent (S)-NAD(P)H-hydrate dehydratase (42919at186826) | 3
Dihydrofolate reductase (61889at186826) | 128
Glucose-6-phosphate isomerase (7599at186826) | 36

----
* ADP-dependent (S)-NAD(P)H-hydrate dehydratase is incomplete in strains SRCM103285 (GCF_004063515.1), KMB_612 (GCF_003346325.1), KMB_613 (GCF_003346315.1)
1. The gene is defined as pseudogene because of partial gene sequence and missing C-terminus in strain SRCM103285
2. The genes are 193 and 195 aa in strain KMB_612 and KMB_613, respectively. Which is much shorter than median protein length (280 aa).

![image](https://github.com/logcossin/ForReport/assets/49052882/b33e8895-de26-472c-ae18-5879559d6cdc)
![image](https://github.com/logcossin/ForReport/assets/49052882/81673fa7-44b0-4991-9a1c-f58b85058a3a)

* Example of fragmented NAD(P)H-hydrate dehydratase in *L. fermentum* KMB_613. Arrows indicate the end of each contig.
* The gene is located and separted into two contigs.

----
* Dihydrofolate reductase is analyzed fragmented in most of the *L. fermentum* genomes.
* The average length of genes analzyed as complete (166.6 aa) or fragmented (166.8 aa) is almost the same.
* The average alignment length of genes analzyed as complete (75.4 aa) was higher than fragmented (59.0 aa).

----
* Glucose-6-phosphate isomerase is analyzed fragmented in 21 genomes and missing in 15 genomes.
* The average length of genes analzyed as complete (427.7 aa) was higher than fragmented (303.1 aa).
* All fragmented genes from 21 genomes were located at the edge of the contigm, leading to truncated sequences.
* Genomes analyzed as missing gene had gene sequences truncated near the middle or on both ends (too short), the [PGAP](https://github.com/ncbi/pgap) defined them as pseudogenes.

## Automatic detection of incomplete BUSCO genes in the genome

* Incomplete BUSCO genes could be found due to reasons below:
1. Gene truncation by mutation (frameshift, nonsense)
2. Gene located at the edge of the contig
3. Gene deletion
4. Short alignment length to the BUSCO HMM profile
5. Genome misassembly

* BUSCO lineage dataset provides consensus ancestral sequences for marker genes. [#](https://busco.ezlab.org/busco_userguide.html#lineage-datasets)
* TBLASTN (protein to translated nucleotide) search with the consensus sequence as query could be used to identify gene fragments in the genome sequence.

TBLASTN Hit | Result
---- | ----
Multiple hits in the region side by side | Gene trucation
Hit at the end of contigs | Gene located at the edge of the contig
No hit | Gene deletion
Multiple hits from regions at different contigs (edge X) | Genome misassembly

* The genomic region with match could be analyzed to find the reason of incomplete marker genes.
* Comparing the length of fragmented and complete genes could be used to identify whether the fragmented gene is actually trucated or it is due to short BUSCO HMM model alignment length.

# ANI analysis

![image](https://github.com/logcossin/ForReport/assets/49052882/5e7d0101-2693-4be8-a700-7bac4ec3e428)

* ANI analysis was performed using [pyani](https://github.com/widdowquinn/pyani) with default parameters
* *L. fermentum* genomes were mainly clustered into 4 groups
* Most of the genomes (157) were inside group 1 and 2 (>99% identity)
* Group 3 genomes (34) had 92~94% CheckM completeness
* Group 4 genomes (9) had 88~91% CheckM completeness and fragmented genome sequence (>100 contigs)
