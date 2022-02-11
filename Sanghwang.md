# 연구실 보유 상황버섯 균주의 ploidy 분석 결과

* 연구실에서 보유 중인 고려상황버섯(*Phellinus linteus*)과 장수상황버섯(*Phellinus baumii*) 균주의 ploidy 분석을 진행함.
* 두 균주의 현미경 상 균사 형태로는 고려상황버섯은 haploid, 장수상황버섯은 diploid로 추정됨.

## 고려상황버섯

* gDNA read data directory: /flareon/analysis2/Goryo_mushroom/reads_genome
* genome sequence directory: /flareon/analysis2/Goryo_mushroom/circos

![](./plot/goryeo.png)

* BUSCO 분석 결과 contamination (duplication)은 1.1%로 확인됨.
* 추가로 GenomeScope 분석 결과 확인되는 peak가 1개로 연구실에서 보유중인 고려상황버섯 균주는 haploid로 추정됨.

## 장수상황버섯

* 장수상황버섯은 gDNA read data는 확인되지 않고 RNA-seq read data만 /flareon/analysis2/Goryo_mushroom/reads_Jangsu에 존재함.
* genome sequence directory: /flareon/analysis2/Goryo_mushroom/circos

* BUSCO 분석 결과 contamination (duplication)은 8.8%로 연구실에서 보유중인 장수상황버섯 균주는 diploid로 추정됨.
* gDNA read data 확보 시 GenomeScope 분석 진행 예정.

----

* gDNA read data directory: /flareon/analysis2/Goryo_mushroom/reads_Jangsu
* 306호에서 보관 중인 mbn server HDD에서 장수상황버섯 gDNA read data를 flareon으로 옮겨 GenomeScope 분석을 진행함.

![](./plot/jangsu.png)

* GenomeScope plot에서 peak가 2개로 연구실에서 보유중인 장수상황버섯 균주는 diploid로 예상됨.