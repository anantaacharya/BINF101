############
Preparing environment and installing tools
############

We will be setting up the computing environment in Google Compute. Other cloud services such as Azure or AWS can also be set up.
For the purpose of this class we have set up with minimal compute resource and storage. For most bioinformatics projects, the resources may not be enough. We can always expand if we need to, thanks to the cloud. 

 
Start Google cloud compute engine
 
Connecting to Google Compute
============================
Linux/Macbook: Terminal
Windows: use putty 

Putty: Please download putty from https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html. Make sure you have the right version. The host address, password and key file will be shared differently. 

For file transfer:
==================
Winscp: https://winscp.net/eng/index.php

Preparing the environment
=========================

suggest Conda environment for easy install

Install miniconda
=================

 ``wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh``
 ``bash Miniconda3-latest-Linux-x86_64.sh``

 ``conda config --add channels bioconda``
 ``conda config --add channels conda-forge``

 ``source /home/ananta/.bashrc``

Install Bioinformatics softwares
================================

blast, bwa, samtools, vcftools, 

 
 ``conda install ``

activate conda for individiual users:
=====================================
use this or add it on bashrc


 ``. "/home/ananta/miniconda3/etc/profile.d/conda.sh"``


