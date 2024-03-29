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
* `<괄호>` 안에 있는 부분은 실제 이름으로 변경해서 사용.

1. Sequencing 데이터가 있는 `flareon` 서버 접속.
```
Windows: Xshell 등 프로그램 사용
Ubuntu: 터미널에서 ssh 아이디@flareon.korea.ac.kr 입력 후 비밀번호 입력
```

2. `leafeon` 서버에 결과물 저장할 폴더 생성.
```
# 아이디 부분 개인 서버 아이디로 변경
ssh <아이디>@leafeon.korea.ac.kr
cd /leafeon/analysis1/<아이디>
# 결과 폴더명 원하는 이름으로 변경
mkdir <output_folder_name>
```

3. ONT fast5 파일을 `leafeon` 서버로 이동.
```
cd /flareon/analysis5/minion_reads
# 탭으로 자동완성 가능
cd <결과폴더>/no_sample/<날짜>/fast5_pass
# 사용한 barcode 폴더만 이동, ## 부분 바코드 숫자로 변경
scp -r barcode## 아이디@leafeon.korea.ac.kr:/leafeon/analysis1/<아이디>/<output_folder_name>
```

4. Guppy 이용해 basecalling 진행.
```
ssh 아이디@leafeon.korea.ac.kr
cd /leafeon/analysis1/<아이디>/<output_folder_name>
# GPU 사용량 확인
nvidia-smi
# 다른 사람이 GPU 사용중일 시, chunks_per_runner 값 낮춰서 사용
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

* 예시: FLO-MIN106, SQL-NBD112-24 사용 = dna_r9.4.1_e8.1_sup.cfg
* 사용한 kit 버전은 시퀀싱 결과 폴더 내 final_summary 파일에서 확인 가능.

### 3. Assembly
1. flye 이용해 genome assembly 진행.
```
cat barcode##_output/pass/* > barcode##.fastq
# Read 통계 확인
NanoStat --fastq barcode##.fastq
# CPU 사용량 확인, q 눌러서 htop 나올 수 있음
htop
# 현재 사용중인 CPU 확인해 -t 숫자 조절
flye --nano-hq barcode##.fastq -o barcode## -i 2 -t <CPU 수>
```

2. High quality read만 사용하여 assembly.
```
NanoFilt -q 12~15 barcode##.fastq > barcode##_q##.fastq
flye --nano-hq barcode##_q##.fastq -o barcode##_q## -i 2 -t <CPU 수>
```

* 높은 퀄리티 read만 사용할 경우 보통 genome 품질도 좋아지나 직접 assembly 진행하여 확인 필요.
* 일반적으로 세균은 genome coverage (depth) 30~40x 정도까지도 complete genome assembly 가능.

3. Assembly QC
```
# Install BUSCO
conda create -n busco -c conda-forge -c bioconda busco=5.4.7
conda activate busco
# 앞에 (busco) 뜨는지 확인
busco -m genome -i <assembly FASTA 파일> --out <output_name> --out_path <output_folder> -c <CPU 수> -l <lineage>
```

* BUSCO는 특정 taxonomy lineage의 genome에서 1개씩 보존되어 있는 single-copy ortholog 유전자를 사용하여 genome의 completeness를 확인하는 프로그램임.
* Lineage는 세균은 bacteria, 균류는 fungi 사용, `busco --list-datasets` 입력 시 가능한 모든 lineage 볼 수 있음.

4. Assembly polishing

* Short-read를 이용한 polishing은 이 튜토리얼에서 다루지 않음.

```
# Install requirements
conda activate ont
conda install -c conda-forge -c bioconda racon medaka minimap2

# Align read to the assembly
minimap2 -x map-ont -o <output>.paf -t <CPU 수> <assembly FASTA 파일> <read FASTQ 파일>

# racon
racon -t <CPU 수> <read FASTQ 파일> <output>.paf <assembly FASTA 파일> > <assembly_racon>.fasta

# medaka, -m 값은 다른 flow cell 쓰면 변경해야 됨
medaka_consensus -i <read FASTQ 파일> -d <assembly_racon>.fasta -o <medaka_output> -m r941_e81_sup_g514 -t <CPU 수>

# Genome 품질 개선됐는지 확인
busco -m genome -i <medaka_output>/consensus.fasta --out <output_name> --out_path <output_folder> -c <CPU 수> -l <lineage>
```

### 4. Annotation
