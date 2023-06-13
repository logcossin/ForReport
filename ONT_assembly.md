## Assemble genome sequence with Oxford Nanopore long-reads

Tutorial for genome assembly using ONT reads.

### 1. Installing requirements using conda

```
cd $HOME
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh

conda update conda
conda create -y -n ont
conda activate ont
conda install -c conda-forge -c bioconda nanofilt nanostat flye
```

### 2. Basecalling

* ONT 시퀀싱 진행 시 MinKNOW 프로그램이 생산하는 read는 fast basecalling model을 사용한 것으로, read quality가 낮아 basecalling을 다시 해야함.

1. Sequencing 데이터가 있는 `flareon` 서버 접속.
```
Windows: Xshell 등 프로그램 사용
Ubuntu: 터미널에서 ssh 아이디@flareon.korea.ac.kr 입력 후 비밀번호 입력
```

2. `leafeon` 서버에 결과물 저장할 폴더 생성.
```퍄 잭  
cd /leafeon/analysis1/아이디
mkdir 폴더명1
```

3. ONT fast5 파일을 `leafeon` 서버로 이동.
```
cd /flareon/analysis5/minion_reads
# 탭으로 자동완성 가능
cd 결과폴더/no_sample/날짜/fast5_pass
# 시퀀싱에 사용한 barcode 폴더만 이동
scp -r barcode## 아이디@leafeon.korea.ac.kr:/leafeon/analysis1/아이디/폴더명1
```

4. Guppy 이용해 basecalling 진행.
```
cd /leafeon/analysis1/아이디/폴더명1
guppy_basecaller -i barcode## -s barcode##_output -c config파일 --chunks_per_runner 65 -x 'cuda:0'
```
* 사용한 flow cell, sequencing kit 버전마다 사용해야 되는 config 파일이 다름.

Flow cell | Prefix
---- | ----
FLO-MIN106 | dna_r9.4.1_
FLO-MIN111 | dna_r10.3_
FLO-MIN114 | dna_r10.4.1_

Sequencing kit | Suffix
---- | ----
SQK-OOO108 | 450bps_sup.cfg
SQK-OOO109 | 450bps_sup.cfg
SQK-OOO110 | 450bps_sup.cfg
SQK-OOO112 | e8.1_sup.cfg
SQK-OOO114 | e8.2_260bps_sup.cfg<br>e8.2_400bps_sup.cfg<br>e8.2_400bps_5khz_sup.cfg

* 사용한 kit 버전은 시퀀싱 결과 폴더 내 final_summary 파일에서 확인 가능.

5. flye 이용해 genome assembly 진행.
```
cat barcode##_output/pass/* > barcode##.fastq





