## Summary of the ONT sequencing

Feature | LAB60668 | LAB69 | LAB17
---- | ---- | ---- | ----
Number of reads | 920,512 | 300,135 | 177,829
Total bases (Mbp) | 3,017.0 | 1,850.0 | 1,115.5
Mean read length (bp) | 3,277.6 | 6,163.8 | 6,272.7
Mean read quality | 17.9 | 17.5 | 17.4

## Summary of the genome assembly and annotation

Feature | LAB60668 | LAB69 | LAB17
---- | ---- | ---- | ----
Total length (bp) | 2,048,909 | 2,077,559 | 2,077,645
Contig number | 1 | 1 | 1
Predicetd species | _L. reuteri_ | _L. fermentum_ | _L. fermentum_
Identified protein-coding genes | 1,950 | 1,924 | 1,923
Average gene length (aa) | 297.0 | 298.2 | 298.0
BUSCO completeness | 99.7% | 99.7% | 99.7%

* Genome annotation was performed by NCBI [Prokaryotic Genome Annotation Pipeline v6.6](https://github.com/ncbi/pgap).
* All 3 strains assembled into one complete circular genome with over 99% genome completeness (lactobacillales_odb10 dataset).
* Species was predicted with ANI analysis.

![image](https://github.com/logcossin/ForReport/assets/49052882/c4129b75-5675-4a01-8316-1288fa7391e5)

### Genome completeness analysis

* According to the BUSCO genome completeness analysis, all 3 strains have 1 fragmented/missing BUSCO gene.
* Further analysis of the 3 fragmented/missing genes was performed.

----
* _L. reuteri_ LAB60668 have analyzed to miss the [3'-5' exonuclease](https://v10.orthodb.org/?query=25336at186826) gene.
* BLAST alignment using the [3'-5' exonuclease](https://www.ncbi.nlm.nih.gov/protein/WP_012391483.1) gene seqeunce of _Limosilactobacillus fermentum_ in the BUSCO database resulted with no significant hits to the _L. reuteri_ genes in the NCBI database.
* The _L. reuteri_ species itself lacks the gene homologous to the 3'-5' exonuclease in the BUSCO database.

----
* _L. fermentum_ LAB69 and LAB17 have analyzed to have fragmented [Dihydrofolate reductase](https://www.orthodb.org/v10?query=61889at186826) gene.
* _L. fermentum_ WP_003683166.1 _L. plantarum_ WP_135293957.1 have lower scores, analyzed as fragmented but have full sequence.

## Virulence factor / Antibacterial resistance gene analysis

* Virulence factor analysis was performed by [VirulenceFinder v2.0.3](https://cge.food.dtu.dk/services/VirulenceFinder/) with all species selected.
* Antibacterial resistance gene analysis was performed by [ResFinder v4.4.1](http://genepi.food.dtu.dk/resfinder) with default parameters.
----

* No virulence factor or antibacterial resistance gene was found in all 3 strains.
