# Mouse RNA-seq analysis
## 1. Purpose
+ Mouse lung cell에 나프탈렌을 처리한 후 control group과 비교해 Differentially Expressed Genes (DEGs)를 확인함.

## 2. Data collecting
+ 실험 및 RNA 추출: 순천향대학교 순천향의생명연구원 김현택 교수님 연구실
+ Sequencing: [Marcrogen, Inc.](https://www.macrogen.com/ko/main)
+ 전체 sample은 8개로 control group, 나프탈렌을 처리한 group 각각 4개임.

Sample | Category | Total reads | Total bases (Gbp)
--- | --- | --- | ---
CON1 | Control | 67,025,882 | 6.8
CON2 | Control | 78,515,996 | 7.9
CON3 | Control | 67,985,654 | 6.9
CON4 | Control | 81,451,888 | 8.2
NPT1 | Naphthalene | 87,953,332 | 8.9 
NPT2 | Naphthalene | 78,694,240 | 7.9
NPT3 | Naphthalene | 61,675,176 | 6.2
NPT4 | Naphthalene | 65,466,094 | 6.6

+ Mouse reference genome으로는 NCBI의 GRCm39 (RefSeq accession: GCF_000001635.27)을 사용함.

## 3. Read adapter trimming & QC
+ TrimGalore (v0.6.10)를 사용해, read의 adapter trimming과 QC를 진행함.
+ Filtering 이후 남은 base가 모든 sample에서 99% 이상으로 read quality에 문제 없음.

## 4. Read alignment
+ NCBI reference genome을 대상으로 QC가 끝난 read를 HISAT2 (v2.2.1)를 사용해 read alignment를 진행함.
+ 사용한 parameters: --max-intronlen 150000, other parameters default
+ 모든 sample에서 95% 이상의 alignment rate을 보임.

Sample | Overall alignment rate
--- | ---
CON1 | 96.13%
CON2 | 97.52%
CON3 | 97.81%
CON4 | 96.67%
NPT1 | 96.70%
NPT2 | 97.12%
NPT3 | 97.06%
NPT4 | 97.04%

## 5. DEG analysis
+ R의 GenomicAlignments package (v1.30.0)를 사용해 gene 별로 align된 read의 raw count를 구함.
+ Raw count를 R의 edgeR package (v3.36.0)를 사용해 RPKM, Log2FC (Fold change), P-value 등의 값을 계산함. 
+ Protein-coding gene을 제외한, tRNA, rRNA, miRNA, lncRNA 등의 non-coding gene은 모두 제거함.

### 5.1 edgeR analysis
+ 아래 표는 Sample 1, 2의 유전자 발현량 기본 통계를 나타냄.

  * Raw count 
  
   | Statistics | Sample1_a raw count | Sample1_b raw count | Sample1_c raw count | Sample2_a raw count | Sample2_b raw count | Sample2_c raw count | Sample 1 mean raw count | Sample 2 mean raw count|
   | - | - | - | - | - | - | - | - | - 
   | Mean | 652.8 | 652.5 | 652.7 | 643.7 | 643.5 | 644.3 | 652.69 | 643.9
   | Min | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0
   | Max | 197,521 | 196,954 | 197,521 | 160,595 | 162,025 | 161,897 | 197,332 | 161,506
   | 1st Quarter | 13 | 13 | 14 | 16 | 16 | 16 | 13.67 | 16
   | Median | 107 | 106 | 106 | 113 | 112 | 112 | 106.33 | 113
   | 3rd Quarter | 502 | 503 | 502 | 505 | 505 | 506 | 501.67 | 506.4
   
   * RPKM

   | Statistics | Sample1_a RPKM | Sample1_b RPKM | Sample1_c RPKM | Sample2_a RPKM | Sample2_b RPKM | Sample2_c RPKM | Sample 1 mean RPKM | Sample 2 mean RPKM |
   | - | - | - | - | - | - | - | - | - 
   | Mean | 2.394 | 2.391 | 2.391 | 2.416 | 2.413 | 2.415 | 2.392 | 2.4145
   | Min | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0
   | Max | 1736.59 | 1718.83 | 1791.81 | 1853.94 | 1865.12 | 1904.55 | 1749.08 | 1874.54
   | 1st Quarter | 0.056 | 0.056 | 0.056 | 0.063 | 0.063 | 0.064 | 0.0575 | 0.065
   | Median | 0.298 | 0.298 | 0.297 | 0.305 | 0.309 | 0.309 | 0.298 | 0.308
   | 3rd Quarter | 1.266 | 1.266 | 1.270 | 1.274 | 1.271 | 1.268 | 1.272 | 1.273
   
+ 유전자 발현량 차이에 따라 유전자를 아래와 같이 분류함.
  * P-value가 0.005 이상인 유전자는 LogFC 값에 상관 없이 Non DEG로 분류함.

   | DEG category | LogFC (1,4-NQ treat/Control) | Count
   | - | - | -
   | Total | - | 32,843
   | Strongly upregulated | LogFC >= 3 | 176
   | Upregulated | 3 > LogFC >= 2 | 197
   | Slightly upregulated | 2 > LogFC >= 1 | 759
   | Non DEG | 1 > LogFC >= -1 or P-value > 0.005 | 31,402
   | Slightly downregulated | -1 > LogFC > -2 | 215
   | Downregulated | -2 >= LogFC > -3 | 36
   | Strongly downregulated | -3 >= LogFC | 58

### 5-1. Distribution of RPKM
![gitupload_rpkm](https://user-images.githubusercontent.com/97942772/193222648-de34e244-8319-4836-aaf2-5d33c1b8c9d5.png)

   + Sample1의 RPKM 값을 X축, sample2의 RPKM 값을 Y축으로 설정하고 scatterplot을 통해 분포를 확인함.
   + Sample 당 3개의 replicate의 평균값을 사용함.
   + RPKM 최대값(1,700 이상)에 비해, median은 sample1, sample2 각각 0.298, 0.308으로 낮음.
   + 따라서 X, Y축의 범위를 10까지만 제한하여 나타냄.
 
### 5-2. Distribution of Log RPKM
![logrpkm_upload](https://user-images.githubusercontent.com/97942772/193222622-7184fb5c-ffdc-46f1-afe6-61224cc560c0.png)

   + Sample1, sample2 RPKM의 로그 값 분포를 확인함. 
   + RPKM 값이 1 이하일 경우 Log RPKM 값은 음수가 되어 그래프를 통한 시각적 인식에 어려움이 있어 RPKM값에 1의 pseudocount를 더한 후 로그 값을 계산함.

### 5-3. MA plot
![maplot_upload](https://user-images.githubusercontent.com/97942772/193222596-ac88e06d-9613-4a62-8266-0c323623b344.png)

   + X축을 Sample 1과 2의 RPKM 평균의 로그 값(Log10, pseudocount 적용)으로, Y축을 LogFC(Log2)로 설정함.

### 5-4 Heatmap 
![heatmapfortriplate](https://user-images.githubusercontent.com/97942772/193222696-c1a6ee6f-2b77-423c-beaf-8f7fe60aa0ba.png)

   + RPKM를 이용해 그린 heatmap에서 각 샘플의 replicate끼리 clustering이 되는 것을 확인함.

## 6. Result
+ DEG 분석에서 LogFC의 절댓값이 3 이상인 유전자 중, 1,4-NQ과의 연관성이 과거 논문으로 알려진 유전자를 탐색함.
+ Strongly upregulated group에 포함된 hsp70.3, hsp70.1, hsp90aa1.2, dnaja (hsp40) 유전자가 human carcinoma A431 cell에서 1,4-NQ 처리 시 발현이 증가했다는 [연구 결과](https://www.sciencedirect.com/science/article/pii/S0891584916311492)가 있음.
+ 또한 strongly upregulated group인 [LOC103909982](https://www.ncbi.nlm.nih.gov/gene/103909982), pdcd4b-2, pdcd4b, [si:dkey-204l11.1](https://www.ncbi.nlm.nih.gov/gene/100006301), bbc3는 programmed cell death 또는 apoptosis 관련 유전자로 확인되었고, 1,4-NQ는 electron-accepting capability으로 인해 ROS (reactive oxygen species) 생산을 증가시켜 cell apoptosis를 유발한다는 [연구 결과](https://www.spandidos-publications.com/10.3892/mmr.2019.10500)가 있음.
+ 또한 upregulated group에서도 heat shock protein (HSP) 관련 유전자들인 dnajb1b, ahsa1a, dnajb2, hspa4a 등이 확인됨.
+ 따라서 이번 실험에서 확인한 1,4-NQ 처리 후 발견된 DEG들이 기존의 연구들과 유사한 경향성을 보이고 있다고 할 수 있음.
