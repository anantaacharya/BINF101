#########################
Sequence Alignment
#########################
Preparing
----------
Copy the files from data folder to your analysis folder

``head -n 40000 /mnt/disks/data/data/arabidopsis/fastq/fasterq.tmp.afurampur.4099/ERR3407466.afurampur.4099.1.1>ERR3407466.1.1.fq``

``head -n 40000 /mnt/disks/data/data/arabidopsis/fastq/fasterq.tmp.afurampur.4099/ERR3407466.afurampur.4099.1.2>ERR3407466.1.2.fq``

Be sure to use a different file by different person. ie, 0.1. 0.2; 1.1,1.2; 2.1,2.2 etc

basic stats
-----------
count sequences

``grep "^@" ERR3407466.1.1.fq | wc -l``

fastqc
---------

``fastqc ERR3407466.1.1.fq``

Use winscp to download the .html alongwith .zip file and inspect it.
 
-Is it preoblematic?
-does it contain adaptors?

We may need to trip the adaptor sequences, which is not covered here today. 

Mapping
---------
There are multiple programs to map short reads to reference genome. We will use bwa. 

``bwa``

.. code-block:: console

	Program: bwa (alignment via Burrows-Wheeler transformation)
	Version: 0.7.17-r1188
	Contact: Heng Li <lh3@sanger.ac.uk>

	Usage:   bwa <command> [options]

	Command: index         index sequences in the FASTA format
			 mem           BWA-MEM algorithm
			 fastmap       identify super-maximal exact matches
			 pemerge       merge overlapping paired ends (EXPERIMENTAL)
			 aln           gapped/ungapped alignment
			 samse         generate alignment (single ended)
			 sampe         generate alignment (paired ended)
			 bwasw         BWA-SW for long queries

			 shm           manage indices in shared memory
			 fa2pac        convert FASTA to PAC format
			 pac2bwt       generate BWT from PAC
			 pac2bwtgen    alternative algorithm for generating BWT
			 bwtupdate     update .bwt to the new format
			 bwt2sa        generate SA from BWT and Occ

	Note: To use BWA, you need to first index the genome with `bwa index'.
		  There are three alignment algorithms in BWA: `mem', `bwasw', and
		  `aln/samse/sampe'. If you are not sure which to use, try `bwa mem'
		  first. Please `man ./bwa.1' for the manual.


Before mapping reference genome needs to be indexed using

``bwa index <ref.fa>``

However, We already have a indexed reference genome. So, you can skip this for course. 
ref genome is 

``/mnt/disks/data/data/arabidopsis/ref/GCF_000001735.4_TAIR10.1_genomic.fasta``

mapping the paired end reads can be done by using the following command. Be sure to replace the texts within <> with approproiate names. 

.. code-block:: sh
	bwa mem <ref.fa> <in.1.fq> <in.2.fq> > <in.sam>
 
