# hse22_hw1
Here's my homework on BioInf minor in HSE 
### List of commands for server:
##### 1. Создаем ссылки на файлы:
ls /usr/share/data-minor-bioinf/assembly/* | xargs -tI{} ln -s {}
##### 2. Выбираем чтения
seqtk sample -s426 oil_R1.fastq 5000000 > sub1.fastq \n
seqtk sample -s426 oil_R2.fastq 5000000 > sub2.fastq \n
seqtk sample -s426 oilMP_S4_L001_R1_001.fastq 1500000 > matep1.fastq
seqtk sample -s426 oilMP_S4_L001_R2_001.fastq 1500000 > matep2.fastq
