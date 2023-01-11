# Mutation identification of CO2 adaptive laboratory evolved _Clostridium_ sp. JS66 strain

## Description

* Wild type _Clostridium_ sp. JS66 was adapted on CO 70% to improve CO tolerance and consumption resulting in strain ALE CO70.
* Adaptive laboratory evolution (ALE) on CO2 using strain ALE C070 resulted in ALE CO2 strain.
* Mutation identification on the ALE CO2 strain against the WT _Clostridium_ sp. JS66 using the breseq analysis pipeline showed a 41bp insertion at the NADH reductase gene (CCP7_01065) locus. (Validated with Sanger sequencing)

## Variant calling result validation with BCFtools

* Variant calling with [BCFtools (v1.15.1)](https://github.com/samtools/bcftools) was performed to validate results from [breseq (v0.37.1)](https://github.com/barricklab/breseq)
* [Bowtie2 (v2.4.5)](https://github.com/BenLangmead/bowtie2) was used to align sequenced reads to the reference genome with the `--local` parameter.
* Variant calling was performed using the command below:
  * `bcftools mpileup -d 1000000 -L 1000000 -a FORMAT/AD,FORMAT/DP,INFO/AD -f Clostridium_JS66.fasta -O u *.bam | bcftools call -mv -O b --ploidy 1 -o calls.bcf`
  * `bcftools filter -i '%QUAL>=200 && INFO/DP>=100' -O v calls.bcf > calls_filter.vcf`
* Results from breseq and BCFtools were mostly same, except some insertions in the intergenic regions only identified by BCFtools (highlighted yellow in the Excel file).

## Origin of the inserted sequence at the CCP7_01065 locus

* Inserted sequence: `ATATGCAAATCCTAAAGTACCTCCAACTGCATAAGCACAAA`
* Manual BLASTn search of the insert sequence in the _Clostridium_ sp. JS66 wild type genome resulted in 1 hit.
* Exact same sequence was found in the JS66 genome at position 1,114,654-1,114,694 (reverse strand), which is 34 bases downstream from the insertion site.

## Protein sequence change of the NADH reductase gene (CCP7_01065)

![image](https://user-images.githubusercontent.com/49052882/211787926-ef91540f-2935-4a2a-aa6d-485bcdb3e7ce.png)

* Original protein sequence (601 amino acids) was split into two at position 213.
* First protein fragment contains the Ferredoxin family domain.
* Second protein fragment contains the NADH:ubiquinone oxidoreductase domain.
* Two possible scenarios for the gene's function:
  1. Split protein is fully functional as original NADH reductase gene
  2. Only the Ferredoxin domain is functional
