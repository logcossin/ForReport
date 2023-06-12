## Assemble genome sequence with Oxford Nanopore long-reads

Tutorial for genome assembly using ONT reads.

### 1. Installing required softwares

```
cd $HOME
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh

conda update conda
conda create -y -n ont
conda activate ont
conda install -c conda-forge -c bioconda flye medaka
```

### 2. Basecalling

* ONT 시퀀싱 진행 시 MinKNOW 프로그램이 생산하는 read는 fast basecalling model을 사용한 것으로, read quality가 낮아 basecalling을 다시 해야함.

1. Sequencing 데이터가 있는 `flareon` 서버 접속.
```
Windows: Xshell 등 프로그램 사용
Ubuntu: 터미널에서 ssh 아이디@flareon.korea.ac.kr 입력 후 비밀번호 입력
```

2. `leafeon` 서버에 결과물 저장할 폴더 생성.
```
cd /leafeon/analysis1/아이디
mkdir 폴더명1
```

3. ONT fast5 파일을 `leafeon` 서버로 이동.
```
cd /flareon/analysis5/minion_reads
# 탭으로 자동완성 가능
cd 결과폴더/no_sample/날짜/fast5_pass
# 시퀀싱에 사용한 barcode 폴더만 이동
scp -r barcode## 아이디@leafeon.korea.ac.kr:/leafeon/analysis1/폴더명1
```

4. 
