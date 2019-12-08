#########################
Sequence Alignment (Blast/Pairwise/MSA)
#########################
Blast with commandline
-------------------------


blastn -db nt -query FAW.fasta -remote -outfmt 6 -out out.blast





Pairwise Sequence Alignment
------------------------------






Multiple sequence alignment
---------------------------------------

Make sure you are in your students folder. 
Copy the multi-fasta file

``cp /mnt/disks/data/students/ananta/msa/Acanthaster_planci_Gnomon.fsa .``

Insepect the file 
use commands learned earlier on basic unix. 

``grep "^>" Acanthaster_planci_Gnomon.fsa``

output:

.. code-block:: console

	>gnl|GNOMON|17969.m Partial model predicted by Gnomon on Acanthaster planci unplaced genomic scaffold, OKI-Apl_1.0 oki_scaffold1752, whole genome shotgun sequence (NW_019093106.1)
	>gnl|GNOMON|70594930.m Model predicted by Gnomon on Acanthaster planci unplaced genomic scaffold, OKI-Apl_1.0 oki_scaffold1731, whole genome shotgun sequence (NW_019093085.1)
	>gnl|GNOMON|18113.m Partial model predicted by Gnomon on Acanthaster planci unplaced genomic scaffold, OKI-Apl_1.0 oki_scaffold1727, whole genome shotgun sequence (NW_019093081.1)
	>gnl|GNOMON|130719778.m Model predicted by Gnomon on Acanthaster planci unplaced genomic scaffold, OKI-Apl_1.0 oki_scaffold1726, whole genome shotgun sequence (NW_019093080.1)
	>gnl|GNOMON|65528162.m Model predicted by Gnomon on Acanthaster planci unplaced genomic scaffold, OKI-Apl_1.0 oki_scaffold1702, whole genome shotgun sequence (NW_019093056.1)
	>gnl|GNOMON|85684402.m Model predicted by Gnomon on Acanthaster planci unplaced genomic scaffold, OKI-Apl_1.0 oki_scaffold1690, whole genome shotgun sequence (NW_019093044.1)
	>gnl|GNOMON|65753714.m Model predicted by Gnomon on Acanthaster planci unplaced genomic scaffold, OKI-Apl_1.0 oki_scaffold1685, whole genome shotgun sequence (NW_019093039.1)
	>gnl|GNOMON|22673.m Partial model predicted by Gnomon on Acanthaster planci unplaced genomic scaffold, OKI-Apl_1.0 oki_scaffold1684, whole genome shotgun sequence (NW_019093038.1)
	>gnl|GNOMON|11409.m Partial model predicted by Gnomon on Acanthaster planci unplaced genomic scaffold, OKI-Apl_1.0 oki_scaffold1657, whole genome shotgun sequence (NW_019093011.1)
	>gnl|GNOMON|22945.m Partial model predicted by Gnomon on Acanthaster planci unplaced genomic scaffold, OKI-Apl_1.0 oki_scaffold1640, whole genome shotgun sequence (NW_019092994.1)

Again, therese are several programs to perform multiple sequence alignment. We will use muscle. 

muscle has multiple alignment output formats and we will be using -msf for easy visualization.

`` muscle -in Acanthaster_planci_Gnomon.fsa -out Acanthaster_planci_Gnomon.m.fsa -msf``

selected output is as below. 

.. code-block:: console

	gnl|GNOMON|130719778.m    C......... .......... .......... .......... ...ATGGAG.
	gnl|GNOMON|22945.m        TTCGACGTGC ACCGGGGCGG CCCTCCTACT CGTTGGGGCG CACCACCCGG
	gnl|GNOMON|70594930.m     TGGGCTCATC TTCTAGCATC ......ACTG CCCTGATACG CGAAAGCAG.
	gnl|GNOMON|65753714.m     C......... .TCTGAAATG .......... ....GAGACG ATTCTGCAGA
	gnl|GNOMON|22673.m        T.CATGCAAG AGCATGAAGG TGTGAACCAT CC..GATCAG CTATGCCAG.
	gnl|GNOMON|85684402.m     T...TTCGCT GTTTGGAAGG GAACCTCTTT CACAAGGCAG ATAGGGAAAT
	gnl|GNOMON|65528162.m     TGAGCCGAAT GCCTAAGAAG ......ACTG CTTTCAGCGG ..ATGGCAG.
	gnl|GNOMON|11409.m        C.....CAGC CACGAGGAAG AGCTTCAAGA TGTTGGGCAG CAACAGCAGC
	gnl|GNOMON|17969.m        T......... .......... .......... ..TTGAAGAG GAACAGT...
	gnl|GNOMON|18113.m        T........G ATTCAGGAGG CCGGTGACGG TCCGGGGGAT GAAGAGGAAC

