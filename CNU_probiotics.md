# 전남대 probiotics Oxford Nanopore sequencing

* 전남대에서 보낸 94개의 probiotics sample 중 8개 sample에 대해 complete genome까지 완성을 요청함.

Sample No | Species | MinIon sequencing
---- | ---- | ----
1 | _Lactobacillus fermentum_ | X
9 | _Lactobacillus curvatus_ | O
20 | _Lactobacillus fermentum_ | O
30 | _Lactobacillus paracasei_ | O
38 | _Lactobacillus plantarum_ | O
39 | _Lactobacillus plantarum_ | O
46 | _Lactobacillus amylovorus_ | X
54 | _Enterococcus faecium_ | O

* Sample의 gDNA fragmentation 정도가 심한 sample 2개(1, 46번)를 제외하고 나머지 sample 6개에 대해 ONT sequencing을 진행함.

## Sequencing summary

* Basecalling by Guppy v6.0.1, basecalling model: super accurate

Statistics | 9 | 20 | 30 | 38 | 39 | 54
---- | ---- | ---- | ---- | ---- | ---- | ----
Total number of reads | 392,030 | 736,215 | 829,956 | 887,929 | 1,086,533 | 211,150
Total number of bases (Mbp) | 1,046.55 | 1,242.31 | 1,133.07 | 991.41 | 883.71 | 625.37
Mean read length (bp) | 2,669.6 | 1,697.4 | 1,365.2 | 1,116.5 | 813.3 | 2.961.7
Mean read quality | 14.1 | 14.1 | 13.9 | 13.8 | 13.8 | 14.3
Median read length | 981 | 877 | 590 | 687 | 532 | 1,231
Median read quality | 14.1 | 14.1 | 13.9 | 13.8 | 13.8 | 14.4
Read length N50 | 6,760 | 3,108 | 3,131 | 1,586 | 961 | 7,239

## Assembly summary (before polishing)

* Reads were assembled with flye genome assembler v2.9 with `--nano-hq <input_fastq> --scaffold -i 2` parameters.

Statistics | 9 | 20 | 30 | 38 | 39 | 54
---- | ---- | ---- | ---- | ---- | ---- | ----
Total assembly length (bp) | 2,312,371 | 2,077,212 | 3,203,638 | 5,453,564 | 3,331,610 | 2,654,777
Number of scaffolds | 62 | 1 | 9 | 4 | 7 | 3
Longest scaffold (bp) | 290,369 | 2,077,212 | 3,148,976 | 3,301,427 | 3,206,312 | 2,449,126
Scaffold N50 (bp) | 109,476 | 2,077,212 | 3,148,976 | 3,301,427 | 3,206,312 | 2,449,126
Scaffold L50 | 7 | 1 | 1 | 1 | 1 | 1
GC ratio (%) | 51.10 | 51.51 | 46.42 | 47.12 | 44.43 | 38.17

### Genome quality evaluation

* Genome completeness assession with BUSCO v5.3.1
* Used lineage database is bacteria_odb10

BUSCO result | 9 | 20 | 30 | 38 | 39 | 54
---- | ---- | ---- | ---- | ---- | ---- | ----
Complete, single-copy (%) | 91.1 | 91.1 | 96.8 | 12.9 | 98.4 | 92.7
Complete, duplicated (%) | 2.4 | 0.8 | 1.6 | 87.1 | 1.6 | 0.8

* Sample 38번의 duplicated BUSCO 비율 87%로 contamination이 의심됨.

![](../figure/lacto_ani.png)

* Sequencing을 진행한 probiotics 5종의 NCBI RefSeq reference genome을 포함하여 ANI 분석 결과 sample 38번은 _L. plantarum_ 과 _L. fermentum_ 의 mixture로 추정됨.
* Sample 9번은 _L. curvatus_ 가 아니라 _L. fermentum_ sample이 잘못 온 것으로 추정됨. Contamination은 없었음. Miseq short read만을 사용한 assembly은 _L. curvatus_ 로 확인되었음.

### Assembly summary with filtered reads

Statistics | 9 | 20 | 30 | 38 | 39 | 54
---- | ---- | ---- | ---- | ---- | ---- | ----
Read qulaity threshold | 16 | 16 | 15 | 15 | 14 | 15
Total assembly length (bp) | 2,077,506 | 2,077,297 | 3,245,984 | 5,454,248 | 3,356,684 | 2,655,203
Number of scaffolds | 1 | 1 | 9 | 4 | 8 | 3
Longest scaffold (bp) | 2,077,506 | 2,077,297 | 3,149,127 | 3,301,991 | 3,195,058 | 2,449,551
Scaffold N50 (bp) | 2,077,506 | 2,077,297 | 3,149,127 | 3,301,991 | 3,195,058 | 2,449,551
Scaffold L50 | 1 | 1 | 1 | 1 | 1 | 1
GC ratio (%) | 51.51 | 51.51 | 46.39 | 47.12 | 44.40 | 38.17
BUSCO (%) | 97.6 | 97.6 | 99.2 | 100(contam) | 100 | 96.8

## Assembly summary (after short-read polishing)

* 기존의 Miseq sequenced short-read를 사용하여 genome polishing을 진행함.
* Sample 9번은 ANI 분석에서 가장 가까운 것으로 확인된 sample 20번의 read를 사용함.
* 완성된 assembly에서 길이가 가장 긴 scaffold 1개만 추출함.

Statistics | 9 | 20 | 30 | 38 | 39 | 54
---- | ---- | ---- | ---- | ---- | ---- | ----
Total assembly length (bp) | 2,077,621 | 2,077,416 | 3,149,225 | 3,301,852 | 3,195,089 | 2,450,003
GC ratio (%) | 51.51 | 51.51 | 46.48 | 44.53 | 44.62 | 38.34
BUSCO (%) | 98.4 | 98.4 | 99.2 | 100 | 100 | 98.4

* 대부분의 sample에서 BUSCO score가 향상되었고, 길이가 가장 긴 scaffold만 사용해도 BUSCO는 변하지 않았음.
* 가장 긴 scaffold를 제외한 나머지 scaffold를 NCBI web-BLAST hit으로 확인함
* Sample 38번, 54번에서는 plasmid sequence hit만 확인됨
* Sample 30번, 39번에서는 짧은 scaffold에서 genome sequence hit도 확인됨

## Assembly assessment
### Sample 20 (_L. fermentum_)

* Complete circular genome (only 1 contig)
* Number of fragmented BUSCO sequences after polishing: 2

#### Chorismate synthase (981870at2)

* Aromatic amino acid 생합성 관련 유전자
* NCBI reference sequence 대비 start codon upstream으로 약 100 aa 정도가 짧음

![](../figure/20_1.png)

* Start codon 인근에서 deletion으로 frame shift가 일어남
* Miseq read alignment에서는 deletion된 base가 확인되지 않음
* 일부 ONT read alignment에서 deletion된 base가 확인됨. (Insertion (purple bar), gap)

#### 50S ribosomal protein L11 (1702697at2)

* NCBI reference sequence 대비 start codon upstream으로 약 35 aa 정도가 짧음

![](../figure/20_2.png)

* Upstream에서 start codon ATG가 GTG로 바뀌는 point mutation을 확인
* GTG는 bacterial alternative start codon 중 하나임

### Sample 38  (_L. plantarum_)

* Miseq read로 assemble한 genome sequence에서는 contamination이 확인되지 않음
* ONT read로 assemble한 genome sequence에서 _L. fermentum_ 과의 contamination이 확인됨
* Total contig number: 4, all circular sequences
* Genome sequence로 추정되는 contig 2개의 길이는 각각 3.30 Mb, 2.08 Mb임
* 3.30 Mb 길이 contig만 사용한 BUSCO 결과는 complete 100%로 확인됨 (only 1 duplicated)
* 2.08 Mb 길이 contig만 사용한 BUSCO 결과는 complete 97.2%로 확인됨 (3 fragmented)
* 나머지 길이가 짧은 contig 2개: NCBI BLASTN highest query coverage hit
  * contig_3: _Lactiplantibacillus plantarum_ strain CACC 558 plasmid p1CACC558 (CP048023.1, 84% query coverage, 99.49% identity)
  * contig_3: _Lactiplantibacillus plantarum_ strain LP3 plasmid pLB302 (CP017068.1, 100% query coverage, 99.88% identity)

### Sample 54 (_E. faecium_)

* Total contig number: 3, all circular sequences
* Longest contig: _E. faecium_ gDNA sequence
* 나머지 contig 2개: NCBI BLASTN highest query coverage hit
  * contig_2: _Enterococcus faecium_ strain E1077 plasmid pE1077-217 (MT074686.1, 87% query coverage, 99.53% identity)
  * contig_3: _Enterococcus faecium_ strain E843xGE-1-TC1 plasmid pE843-TC-200 (CP081503.1, 73% query coverage, 99.67% identity)
* Number of fragmented BUSCO sequences after polishing: 2

#### Phosphopantothenoylcysteine decarboxylase (1346419at2)

* Coenzyme A (CoA) 생합성 관련 유전자 (coaC)
* OrthoDB의 bacterial coaC의 median length는 403 aa, _Enterococcus_ 의 coaC median length는 249 aa

![](../figure/54_1.png)

* _E. faecium_ 의 coaC는 183 aa으로 길이가 더 짧기 때문에 BUSCO가 fragmented sequence로 판단했다고 추정됨

#### Ribosome silencing factor (1990650at2)

* NCBI reference sequence 대비 start codon upstream으로 30 aa 정도가 짧음

![](../figure/54_2.png)

* Upstream start codon에서 ATG가 ATC로 바뀌는 point mutation을 확인
* _E. coli_ 에서 낮은 확률로 ATC(AUC)가 alternative start codon으로 사용된다는 연구 결과가 있음. [논문](https://doi.org/10.1093/nar/gkx070)
* Miseq과 ONT read alignment에서는 mutation site에 이상이 발견되지 않음

