# 김재진 교수님 신종 균주 assembly

총 2종의 균주에 대해 sequencing을 진행함.

* NS01: _Sphingomicrobium_ sp. GRR-S6-50
* NS02: _Halomonas_ sp. YJPS3-2

## Sequencing summary

Statistics | _Sphingomicrobium_ sp. GRR-S6-50 | _Halomonas_ sp. YJPS3-2
---- | ---- | ----
Total number of read pairs | 639,940 | 2,693,618
Total number of bases (Mbp) | 333.81 | 1,461.91

## Assembly summary

* Adapter trimmed with TrimGalore v0.6.6 with `--paired` option.
* Trimmed reads were assembled with SPAdes genome assembler v3.15.3 with `--isolate --cov-cutoff auto` parameters.

Statistics | _Sphingomicrobium_ sp. GRR-S6-50 | _Halomonas_ sp. YJPS3-2
---- | ---- | ----
Total assembly length (bp) | 2,333,284 | 3,662,638
Number of scaffolds | 4 | 25
Scaffold N50 (bp) | 2,321,309 | 427,846
Scaffold L50 | 1 | 3
GC ratio (%) | 63.30 | 68.12

## Assembly evaluation

* Genome completeness analysis with BUSCO v5.3.1
* Used lineage database is bacteria_odb10

Database | _Sphingomicrobium_ sp. GRR-S6-50 | _Halomonas_ sp. YJPS3-2
---- | ---- | ----
bacteria_odb10 | 100% | 99.2%

## Species evaluation

* 16S rRNA sequence was identified from the genome sequence using Rfam database (v14.7) and Infernal v1.1.2
  * Parameters: `cmscan --cut_ga --rfam --nohmmonly --tblout --fmt 2 --clanin Rfam.clanin Rfam.cm`
* Identified 16S rRNA sequence aligned against NCBI 16S rRNA database with NCBI [web-BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi)

### _Sphingomicrobium_

* Alignment with highest identity was to 16S rRNA of _Sphingomicrobium astaxanthinifaciens_ but genome sequence was not available.
* There is only 2 genomes from genus _Sphingomicrobium_ in NCBI.
* _Sphingomicrobium_ sp. GRR-S6-50 showed about 75% ANI with 2 _Sphingomicrobium_ genomes from NCBI.
* _Sphingomicrobium_ sp. GRR-S6-50 showed 71~74% ANI with 44 Sphingomonadaceae (family) reference complete genomes from NCBI.

### _Halomonas_

* Alignment with highest identity was to 16S rRNA of _Halomonas salina_ but genome sequence was not available.
* ANI score between _Halomonas_ sp. YJPS3-2 and _Halomonas halophila_ NBRC102604 (second higest identity) was about 91%.
