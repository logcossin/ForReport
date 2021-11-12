## Bdellovibrio Genome Polishing

### Description

* Target genome: *Bdellovibrio bacteriovorus* mother strain (109J WT:JWT), mutant strain(109J KNR)
* Sequencing method: Nanopore long read sequencing, polished with Illumina short reads
* Reference genome: *Bdellovibrio bacteriovorus* strain 109J (NCBI accession: NZ_CP007656)

### Genome Polishing

* Genome polishing
  * Genome assembly from previous long read sequencing result was polished with short reads
  * Genome polishing was done by *Pilon*

* Gene annotation
  * Gene annotation was done by *Prodigal*
  * Functional annotation were done by comparining genes to reference genome's annotation
  * *BLASTP* was performed between reference and WT/KnR proteins, WT/KnR proteins with over 99% percent identitiy to reference genes were annotated with reference gene's function

Feature | Reference | WT | WT polished | KnR | KnR polished
---- | ---- | ---- | ---- | ---- | ----
Total assembly length | 3,830,427 | 3,836,685 | 3,837,019 | 3,836,591 | 3,836,926
Number of contigs | 1 | 1 | 1 | 1 | 1
Number of genes | 3,606 | 3,632 | 3,766 | 3,636
Genome completeness (*BUSCO*) | 96.0% | 95.2% | 96.0% | 92.7% | 96.0%

### Variant calling

* Variant calling
  * Variant calling was done by *MUMmer*
  * nucmer script was run between reference genome and WT/KnR and between WT and KnR strain
  * Variant information was reported from nucmer result by show-snps script
  * show-snps result was converted to vcf extension file
  * VCF file can be opened by *IGV* genome browser
