# gDNA sequencing summary for Prof. Jae-Jin Kim

gDNA sequencing was performed with Illumina Miseq platform.

* Library preparation, sequencing: Xiaoyue Xu
* Genome assembly, QC: Bogun Kim

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
Longest scaffold (bp) | 2,321,309 | 539,688
Scaffold N50 (bp) | 2,321,309 | 427,846
Scaffold L50 | 1 | 3
GC ratio (%) | 63.30 | 68.12

## Genome quality evaluation

* Genome completeness assession with BUSCO v5.3.1
* Used lineage database is bacteria_odb10

Database | _Sphingomicrobium_ sp. GRR-S6-50 | _Halomonas_ sp. YJPS3-2
---- | ---- | ----
bacteria_odb10 | 100% | 99.2%

* Genome contamination assession with CheckM v1.1.3

Feature | _Sphingomicrobium_ sp. GRR-S6-50 | _Halomonas_ sp. YJPS3-2
---- | ---- | ----
Marker lineage | c__Alphaproteobacteria (UID3305) | c__Gammaproteobacteria (UID4444)
Completeness | 99.48 | 99.93
Contamination | 1.23 | 0.48

## 16S rRNA sequence based species evaluation

* 16S rRNA sequence was identified from the genome sequence using Rfam database (v14.7) and Infernal v1.1.2
  * Parameters: `cmscan --cut_ga --rfam --nohmmonly --tblout --fmt 2 --clanin Rfam.clanin Rfam.cm`
* Identified 16S rRNA sequence aligned against NCBI 16S rRNA database with NCBI [web-BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi)
* [ANI raw data](./rawdata/ANI_analysis_rawdata.zip) in excel format.

### _Sphingomicrobium_ sp. GRR-S6-50

* Alignment with 16S rRNA sequence of _Sphingomicrobium astaxanthinifaciens_ showed highest identity but genome sequence was not available.
* _Sphingomicrobium_ sp. GRR-S6-50 showed about 75% Average Nucleotide Identity (ANI) with 2 _Sphingomicrobium_ genomes from NCBI. (GCF_014195685.1, GCF_019264355.1)
* _Sphingomicrobium_ sp. GRR-S6-50 showed 71~74% ANI with 44 Sphingomonadaceae (family) complete reference genomes from NCBI.

### _Halomonas_ sp. YJPS3-2

* Alignment with 16S rRNA sequence of _Halomonas salina_ showed highest identity but genome sequence was not available.
* _Halomonas_ sp. YJPS3-2 showed 72.5~91.4% ANI with 94 _Halomonas_ reference genomes from NCBI.
* ANI between _Halomonas_ sp. YJPS3-2 and _Halomonas halophila_ NBRC102604 (second higest rRNA sequence identity) was about 91%.
