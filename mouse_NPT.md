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
+ 모든 sample에서 96% 이상의 높은 alignment rate을 보임.

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
+ Subread package(v2.0.6)의 featureCounts 프로그램을 사용해 gene 별로 align된 read count를 계산함.
+ Used parameters: `featureCounts -a mm39_RefSeq_exon.txt --countReadPairs -B -C -p`
+ R의 edgeR package(v3.42.0)를 사용해 DEG (차등발현유전자) 분석을 진행함.
+ Protein-coding gene이 아닌, tRNA, rRNA, miRNA, lncRNA 등의 non-coding gene은 분석 대상에서 제외함.

### 5.1 edgeR analysis
+ 유전자 발현량 차이에 따라 유전자를 아래와 같이 분류함.
  * P-value가 0.005 이상인 유전자는 LogFC 값에 상관 없이 Non DEG로 분류함.

Category | LogFC (Treated/Control) | Count
---- | ---- | ----
Total protein-coding genes | - | 22,244
Filtered (low-expression) | - | 8,052
Upregulated | LogFC > 2 | 178
Not significant | \|LogFC\| <= 2 or P-value > 0.05 | 13,900
Downregulated | LogFC < -2 | 114

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

