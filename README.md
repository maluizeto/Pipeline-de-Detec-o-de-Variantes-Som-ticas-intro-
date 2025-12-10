# Pipeline de Detecção de variante somática (intro)

Clonar o repositório com arquivos de exemplo

Baixar um repositório do GitHub contendo:
- BAM tumor
- BAM normal
- VCF gnomAD filtrado
- Scripts

```bash 
!git clone https://github.com/renatopuga/somatico.git
```
Baixar o cromossomo 9 de hg19
```bash 
!wget -c https://hgdownload.soe.ucsc.edu/goldenPath/hg19/chromosomes/chr9.fa.gz
```
Remover o "chr" do nome das sequências
```bash
!zcat chr9.fa.gz | sed -e "s/chr//g" > chr9.fa
```
```bash
!zcat chr9.fa.gz | head
```
```bash
!head chr9.fa
```
```bash
!sudo apt-get install samtools
```
```bash
!samtools
```
```bash
!samtools faidx chr9.fa
```
```bash
! cat chr9.fa.fai
```
```bash
!wget -c https://github.com/broadinstitute/gatk/releases/download/4.2.2.0/gatk-4.2.2.0.zip
```
```bash
!unzip gatk-4.2.2.0.zip
```
```bash
!./gatk-4.2.2.0/gatk
```
```bash
!apt-get update
!apt-get install openjdk-11-jdk -y
```
```bash
!./gatk-4.2.2.0/gatk CreateSequenceDictionary -R chr9.fa -O chr9.dict
```
```bash
!./gatk-4.2.2.0/gatk ScatterIntervalsByNs -R chr9.fa -O chr9.interval_list -OT ACGT
```
```bash
!ls
```
```bash
!cat chr9.dict
```
```bash
!samtools view -H somatico/normal_JAK2.bam | grep RG | cut -f6 | sed -e "s/SM://g"
```
```bash
./gatk-4.2.2.0/gatk Mutect2 \
 -R chr9.fa \
 -I somatico/tumor_JAK2.bam \
 -I somatico/normal_JAK2.bam \
 -normal WP044 \
  --germline-resource somatico/af-only-gnomad-chr9.vcf.gz \
	-O somatic.vcf.gz \
	-L chr9.interval_list
```
```bash
!zgrep -v "\##" somatic.vcf.gz
```
```bash
!zgrep "##" somatic.vcf.gz
```
```bash
!./gatk-4.2.2.0/gatk GetPileupSummaries \
	-I somatico/tumor_JAK2.bam \
	-V somatico/af-only-gnomad-chr9.vcf.gz \
	-L chr9.interval_list \
	-O tumor_JAK2.table
```
```bash
!head tumor_JAK2.table
```
```bash
!./gatk-4.2.2.0/gatk GetPileupSummaries \
	-I somatico/normal_JAK2.bam \
	-V somatico/af-only-gnomad-chr9.vcf.gz \
	-L chr9.interval_list \
	-O normal_JAK2.table
```
```bash
./gatk-4.2.2.0/gatk CalculateContamination \
	-I tumor_JAK2.table \
	-matched normal_JAK2.table \
	-O contamination.table
```
```bash
./gatk-4.2.2.0/gatk FilterMutectCalls \
	-R chr9.fa \
	-V somatic.vcf.gz \
	--contamination-table contamination.table \
	-O filtered.vcf.gz
```
```bash
!zgrep -v "##" filtered.vcf.gz
```
