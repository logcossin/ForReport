# gDNA sequencing summary for Prof. Jae-Jin Kim

gDNA sequencing was performed with Oxford Nanopore MinION platform.

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

