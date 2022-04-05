# 김재진 교수님 신종 균주 assembly

총 2종의 균주에 대해 sequencing을 진행함.

* NS01: _Sphingomicrobium_ sp. GRR-S6-50
* NS02: _Halomonas_ sp. YJPS3-2

균주의 genus 정보는 김재진 교수님 연구실 유연재 학생을 통해 받음.

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
N50 (bp) | 2,321,309 | 427,846
L50 | 1 | 3
GC ratio (%) | 63.30 | 68.12

## Assembly evaluation

* Genome completeness analysis with BUSCO v5.3.1
* sphingomonadales_odb10 for _Sphingomicrobium_, oceanospirillales_odb10 for _Halomonas_

* _Sphingomicrobium_ sp. GRR-S6-50 completeness: C:92.3%[S:92.0%,D:0.3%],F:0.4%,M:7.3%,n:1018	
* _Halomonas_ sp. YJPS3-2 completeness: C:99.8%[S:99.8%,D:0.0%],F:0.2%,M:0.0%,n:619

## Species evaluation

* 16S rRNA sequence was identified from the genome sequence using Rfam database (v14.7) and Infernal v1.1.2
  * Command: `cmscan --cut_ga --rfam --nohmmonly --tblout --fmt 2`
* Identified 16S rRNA sequence aligned against 16S rRNA database with NCBI web-BLAST

### _Sphingomicrobium_

* Alignment with highest identity was to 16S rRNA of _Sphingomicrobium astaxanthinifaciens_ but genome sequence was not available.
* There is only 2 genomes from genus _Sphingomicrobium_ in NCBI.
* _Sphingomicrobium_ sp. GRR-S6-50 showed about 75% ANI with 2 genomes from NCBI.

### _Halomonas_

* Alignment with highest identity was to 16S rRNA of _Halomonas salina_ but genome sequence was not available.
* ANI score between _Halomonas_ sp. YJPS3-2 and _Halomonas halophila_ NBRC102604 (second higest identity) was about 91%
