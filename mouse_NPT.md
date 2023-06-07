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
+ 사용한 parameters: `--max-intronlen 150000`, other parameters default
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

Category | LogFC (Treated/Control) | Count
---- | ---- | ----
Total protein-coding genes | - | 22,244
Filtered (low expression) | - | 8,052
Upregulated | LogFC > 2 and P-value < 0.05 | 114
Not significant | \|LogFC\| <= 2 or P-value >= 0.05 | 13,900
Downregulated | LogFC < -2 and P-value < 0.05 | 178

### 5-1. Distribution of gene expression
![plot](https://github.com/logcossin/ForReport/assets/49052882/a5e9852b-8c05-43d6-b40d-6ddc2e9c31de)

+ Control 샘플의 logTPM 평균을 X축, NPT 처리 샘플의 logTPM 평균을 Y축으로 설정하고 scatterplot을 통해 유전자 발현량의 분포를 확인함.

![plot (1)](https://github.com/logcossin/ForReport/assets/49052882/23531cea-65cc-4605-a630-56ab7ca79001)

+ X축을 전체 샘플의 평균 logTPM으로, Y축을 logFC(Fold change)로 설정하여 유전자 분포를 확인함.

### 5-2 Heatmap of differentially expressed genes
![heatmap](https://github.com/logcossin/ForReport/assets/49052882/f62a9287-a5e0-4dd9-9b0a-9747a9216172)

+ logTPM 값을 이용해 그린 차등발현유전자 292개의 heatmap에서 각 샘플의 replicate끼리 clustering이 되는 것을 확인함.

## 6. Result

+ NPT 처리 시 발현량이 증가한 유전자 114개의 Gene Ontology (GO) 분석 결과, response to stress (GO:0006950)와 response to chemical (GO:0042221)가 P-value 하위 5개 안에 포함되어 있음을 확인함.
+ NPT 처리 시 발현량이 감소한 유전자 178개의 Gene Ontology (GO) 분석 결과, cilium movement (GO:0003341)와 axoneme (GO:0005930) 등 cilium 관련 GO들이 P-value 하위 5개 안에 포함되어 있음을 확인함.

