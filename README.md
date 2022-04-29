# Somatico
 
# Baixar o sratoolkit
 mkdir amostras
 cd amostras
 wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/3.0.0/sratoolkit.3.0.0-centos_linux64.tar.gz
 ## descompactar o SRA
 tar xvfz sratoolkit.3.0.0-centos_linux64.tar.gz
 ## montar diretorio organizado
 mkdir apps
 mv -v sratoolkit.3.0.0-centos_linux64 sratoolkit.3.0.0
 mv -v sratoolkit.3.0.0 apps
 cd apps
 cd sratoolkit.3.0.0/bin
