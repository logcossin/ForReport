# gDNA sequencing summary for Prof. Jae-Jin Kim

gDNA sequencing was performed with Illumina Miseq platform.

* Library preparation, sequencing: Xiaoyue Xu
* Genome assembly, QC: Bogun Kim

## Sequencing summary

Statistics | YJP1-3 | GRR-S3-23 | GRR-SB-33
---- | ---- | ---- | ----
Total number of reads | 15,382 | 69,870 | 23,404
Total number of bases (Mbp) | 311.7 | 647.7 | 492.8
Mean read length (bp) | 20,263.5 | 9,270.0 | 21,054.8
Mean read quality score | 13.8 | 14.6 | 13.9

## Assembly summary

* Reads with quality score over threshold value were filtered to generate genome with high completeness.
* Reads were assembled with [Flye genome assembler](https://github.com/fenderglass/Flye) v2.9.2 with `--nano-hq --iterations 2` parameters.
* [Medaka](https://github.com/nanoporetech/medaka) v1.7.2 was used to correct errors in the draft genome assembly with `r941_min_sup_g507` model.
* All 3 strains resulted in complete circular genome.
* Genome completeness assession with [BUSCO](https://busco.ezlab.org/) v5.3.1 with lineage database bacteria_odb10.

Statistics | YJP1-3 | GRR-S3-23 | GRR-SB-33
---- | ---- | ---- | ----
Read quality score threshold | 14 | 15 | 14
Total assembly length (bp) | 3,163,819 | 3,610,406 | 3,320,675
Number of contigs | 1 | 1 | 1
Contig N50 (bp) | 3,163,819 | 3,610,406 | 3,320,675
Contig L50 | 1 | 1 | 1
GC ratio (%) | 45.83 | 33.74 | 69.98
Genome coverage | 47x | 77x | 75x
Genome completeness (%) | 98.4 | 97.6 | 98.4

## 16S rRNA sequence based species evaluation

* 16S rRNA sequence was identified from the genome sequence using [barrnap](https://github.com/tseemann/barrnap) v0.9 with default parameters.
* Identified 16S rRNA sequence aligned against NCBI 16S rRNA database with NCBI [web-BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi)

### YJP1-3

* Alignment with 16S rRNA sequence of _Leeuwenhoekiella aestuarii_, _Cellulophaga algicola_, and _Leeuwenhoekiella nanhaiensis_ showed the TOP3 highest identity but sequence identity were all around 90%.

### GRR-S3-23

* Alignment with 16S rRNA sequence of _Tenacibaculum aiptasiae_ showed highest identity (97.57%).

### GRR-SB-33

* Alignment with 16S rRNA sequence of _Jannaschia seosinensis_ showed highest identity (97.91%).
