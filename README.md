# Somatico
 
# Baixar o sratoolkit
 mkdir amostras
 cd amostras
 wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/3.0.0/sratoolkit.3.0.0-centos_linux64.tar.gz
 # descompactar o SRA
 tar xvfz sratoolkit.3.0.0-centos_linux64.tar.gz
 # montar diretorio organizado
 mkdir apps
 mv -v sratoolkit.3.0.0-centos_linux64 sratoolkit.3.0.0
 mv -v sratoolkit.3.0.0 apps
 cd apps
 cd sratoolkit.3.0.0/bin
# -------------------------------------
 # baixar a referenica do dna humano
 wget https://hgdownload.soe.ucsc.edu/goldenPath/hg19/bigZips/hg19.fa.gz
 descompactar e formar um .fa com o nome chr; zcat hg19.fa.gz | sed -e "s/chr//g" > hg19.fa
 # baixar o samtools
 sudo apt-get install samtools

 # fazer o index
 samtools faidx hg19.fa
 # baixar o GATK
 wget -c https://github.com/broadinstitute/gatk/releases/download/4.2.2.0/gatk-4.2.2.0.zip
 descompactar

 # com o vcf so e preciso marcar no annovar
 wget https://github.com/Varstation/POS-BIOINFO/raw/master/annovar/annovar.zip
 # baixar as bibliotecas de referecnia, CADD, SIFT e PolyPhen, refgene
perl annovar/annotate_variation.pl -buildver hg19 -downdb -webfrom annovar dbnsfp30a annovar/humandb/
perl annovar/annotate_variation.pl -buildver hg19 -downdb -webfrom annovar refGene annovar/humandb/
perl annovar/annotate_variation.pl -buildver hg19 -downdb -webfrom annovar avsnp147 annovar/humandb/
# Annotar as variantes do VCF com o ANNOVAR
perl annovar/table_annovar.pl -vcfinput  /workspace/Somatico/WP02.filtered.vcf \
annovar/humandb/ --dot2underline -buildver hg19 -out WP02_annotado.vcf -remove \
-protocol refGene,avsnp147,dbnsfp30a \
-operation g,f,f -nastring "."
# ver o que foi feito com eliminando os ##
cat dados/annovar/AMOSTRA01.hg19_multianno.vcf | grep -v "^##" | head

perl annovar/table_annovar.pl -vcfinput  /workspace/Somatico/WP006.filtered.vcf \
annovar/humandb/ --dot2underline -buildver hg19 -out WP006_annotado.vcf -remove \
-protocol refGene,avsnp147,dbnsfp30a \
-operation g,f,f -nastring "."
