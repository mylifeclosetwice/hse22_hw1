# hse22_hw1
Here's my homework on BioInf minor in HSE 
### List of commands for server:
##### 1. Создаем ссылки на файлы:
ls /usr/share/data-minor-bioinf/assembly/* | xargs -tI{} ln -s {}
##### 2. Выбираем чтения:
seqtk sample -s426 oil_R1.fastq 5000000 > sub1.fastq 

seqtk sample -s426 oil_R2.fastq 5000000 > sub2.fastq 

seqtk sample -s426 oilMP_S4_L001_R1_001.fastq 1500000 > matep1.fastq

seqtk sample -s426 oilMP_S4_L001_R2_001.fastq 1500000 > matep2.fastq
##### 3. Оцениваем чтения  и создаем отчет:
mkdir fastqc

ls sub* matep* | xargs -tI{} fastqc -o fastqc {}

mkdir multiqc

multiqc -o multiqc fastqc
##### 4. Подрезаем чтения:
platanus_trim sub*

platanus_internal_trim matep*
##### 5. Удаляем исходники:
rm sub1.fastq

rm sub2.fastq

rm matep1.fastq

rm matep2.fastq
##### 6. Оцениваем подрезанные чтения  и создаем отчет:
mkdir fastqc_trimmed

ls sub* matep*| xargs -tI{} fastqc -o fastqc_trimmed {}

mkdir multiqc_trimmed

multiqc -o multiqc_trimmed fastqc_trimmed
##### 7. Собраем контиги
time platanus assemble -o Poil -f sub1.fastq.trimmed sub2.fastq.trimmed 2> assemble.log
##### 8. Собраем скаффолды
time platanus scaffold -o Poil -c Poil_contig.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 matep1.fastq.int_trimmed matep2.fastq.int_trimmed 2> scaffold.log
##### 9. Уменьшаем число промежутков
time platanus gap_close -o Poil -c Poil_scaffold.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 matep1.fastq.int_trimmed matep2.fastq.int_trimmed 2> gapclose.log
##### 10. Удаляем подрезанные чтения
rm sub*.trimmed matep*.int_trimmed

