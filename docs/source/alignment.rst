#########################
Mapping and Variant Calling
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

.. code-block:: console

	#map
	#bwa mem <ref.fa> <in.1.fq> <in.2.fq> > <in.sam>
	bwa mem /mnt/disks/data/data/arabidopsis/ref/GCF_000001735.4_TAIR10.1_genomic.fasta ERR3407466.0.1.fq ERR3407466.0.2.fq > ERR3407466.0.sam
	
	
	#sort
	samtools sort -O bam ERR3407466.0.sam -o ERR3407466.0.sorted.bam
	
	#index
	samtools index ERR3407466.0.sorted.bam
	
	#View file
	
	samtools view ERR3407466.0.sorted.bam | less
	
	#get stats
	
	samtools flagstat ERR3407466.0.sorted.bam
	
	
.. code-block:: console 

	20066 + 0 in total (QC-passed reads + QC-failed reads)
	0 + 0 secondary
	66 + 0 supplementary
	0 + 0 duplicates
	19824 + 0 mapped (98.79% : N/A)
	20000 + 0 paired in sequencing
	10000 + 0 read1
	10000 + 0 read2
	19538 + 0 properly paired (97.69% : N/A)
	19726 + 0 with itself and mate mapped
	32 + 0 singletons (0.16% : N/A)
	110 + 0 with mate mapped to a different chr
	45 + 0 with mate mapped to a different chr (mapQ>=5)
	
	
samtools idxstats for getting statistics on  mapping to indivdual chromosomes

.. code-block:: console
	samtools idxstats ERR3407466.0.sorted.bam
	
	##output
	##(output is from different file here, just for an example)	
	NC_003070.9     30427671        839272  1088
	NC_003071.7     19698289        712864  1010
	NC_003074.8     23459830        941245  1178
	NC_003075.7     18585056        608362  706
	NC_003076.8     26975502        800847  990
	NC_037304.1     367808  78101   80
	NC_000932.1     154478  1057097 1075
	*       0       0       66320


Visualization. 
After mapping, we visualize them using some softwares. IGV is a popular one. We can use the IGV within console and direct to X11 window. IGV also has web application.

Variant Calling

The alignments are then subject to variant calling. There are several open-source programs to call the variants. We will use samtools/bcftools to call variants. 

.. code-block:: console
	
 bcftools mpileup -a "AD,DP" -f /mnt/disks/data/data/arabidopsis/ref/GCF_000001735.4_TAIR10.1_genomic.fasta \
 ERR3407466.afurampur.4099.0.sam.bam..chr1.10000.sorted.bam \
 ERR3407466.afurampur.4099.1.sam.bam.sorted.bam.chr1.10000.bam \
 | bcftools call -mv -Ov -o test.vcf


selected ouput

.. code-block:: console

	#CHROM  POS     ID      REF     ALT     QUAL    FILTER  INFO    FORMAT  ERR3407466.afurampur.4099.0     ERR3407466.afurampur.4099.1
	NC_003070.9     2993    .       C       A       10.7169 .       DP=11;SGB=-0.516033;RPB=1;MQB=1;MQSB=0.974597;BQB=1;MQ0F=0;ICB=0.3;HOB=0.125;AC=1;AN=4;DP4=3,5,1,0;MQ=60        GT:PL:DP:AD     0/1:45,0,154:5:4,1      0/0:0,12,141:4:4,0
	NC_003070.9     4261    .       C       A       17.8336 .       DP=6;SGB=-0.516033;RPB=1;MQB=1;MQSB=1;BQB=1;MQ0F=0;ICB=0.3;HOB=0.125;AC=1;AN=4;DP4=2,2,1,0;MQ=60        GT:PL:DP:AD     0/1:51,0,66:3:2,1       0/0:0,6,75:2:2,0
	NC_003070.9     5124    .       C       A       3.75538 .       DP=7;SGB=-0.516033;RPB=1;MQB=1;MQSB=1.01283;BQB=1;MQ0F=0;ICB=0.3;HOB=0.125;AC=1;AN=4;DP4=3,3,0,1;MQ=60  GT:PL:DP:AD     0/0:0,15,174:5:5,0      0/1:35,0,35:2:1,1
	NC_003070.9     6324    .       taaaa   tAaaaa  164     .       INDEL;IDV=6;IMF=1;DP=9;VDB=0.371445;SGB=-1.03866;MQSB=0.974597;MQ0F=0;AC=4;AN=4;DP4=0,0,5,4;MQ=60       GT:PL:DP:AD     1/1:71,9,0:3:0,3        1/1:120,18,0:6:0,6
	NC_003070.9     6723    .       A       G       7.61464 .       DP=5;SGB=-0.516033;RPB=1;MQB=1;BQB=1;MQ0F=0;ICB=0.3;HOB=0.125;AC=1;AN=4;DP4=2,0,1,0;MQ=60       GT:PL:DP:AD     0/0:0,6,90:2:2,0        0/1:41,3,0:1:0,1
	NC_003070.9     7398    .       G       T       5.01731 .       DP=14;SGB=-0.516033;RPB=1;MQB=1;MQSB=0.964642;BQB=1;MQ0F=0;ICB=0.3;HOB=0.125;AC=1;AN=4;DP4=6,4,1,0;MQ=60        GT:PL:DP:AD     0/0:0,12,104:4:4,0      0/1:39,0,174:7:6,1
