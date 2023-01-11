# Variant calling of _Clostridium_ sp. JS66

## breseq variant calling result validation with BCFtools

* [breseq Github Link](https://github.com/barricklab/breseq)
* [Variant calling with BCFtools](https://samtools.github.io/bcftools/howtos/variant-calling.html)
* `bcftools mpileup -d 1000000 -L 1000000 --threads 20 -f Clostridium_JS66.fasta -O u *.bam | bcftools call -mv -O b --ploidy 1 -o calls.bcf`
* `bcftools filter -i '%QUAL>=200 && INFO/DP>=100' -O v calls.bcf > calls_filter.vcf`

## Origin of the insert sequence

* 41 bp insertion `ATATGCAAATCCTAAAGTACCTCCAACTGCATAAGCACAAA`
* Exact same sequence was found in the genome at position 1,114,654-1,114,694 on the reverse strand

## Functional change of the inserted gene (CLJS66_01052)

* Original protein was split into two proteins at position 213
* First protein fragment contains Ferredoxin family domain
* Second protein fragment contains NADH:ubiquinone oxidoreductase domain
* Split protein might be fully functional or only the Ferredoxin domain could be functional
