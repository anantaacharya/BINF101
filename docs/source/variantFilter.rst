#########################
Variant filtering
#########################

The variants from the prvious chapter can be and should be filtered, reformatted for many downstream applications. `vcftools` is a commonly used program to filter the vcfs. 

Please refer to VCFTOOLS manual (https://vcftools.github.io/man_latest.html) for complete look. We will only practice some commonly used options. 

``vcftools --vcf ERR3407466.0.6.vcf --remove-indels --min-allele 2 --max-allele 2 --recode ``

Please keep looking on manual and explore. Some ideas

1. remove indels
2. keep only biallelic SNPS
3. keep only chromosome 1
4. Keep SNPs from first 10000 bases of chromosome 1
5. calculate average depth of coverage
6. calcualate alleleic depth for all loci, all sample
7. Filter with max and min allele frequency of 0.1 and 0.9


