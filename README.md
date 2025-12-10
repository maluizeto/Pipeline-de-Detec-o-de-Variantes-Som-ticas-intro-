# Pipeline de Detecção de variante somática (intro)
```bash 
!git clone https://github.com/renatopuga/somatico.git
```
```bash 
!wget -c https://hgdownload.soe.ucsc.edu/goldenPath/hg19/chromosomes/chr9.fa.gz
```
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
```bash
```bash
```bash
