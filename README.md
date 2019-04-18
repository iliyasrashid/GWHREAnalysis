# GWHREAnalysis

################ Written by Iliyas Rashid on Apr.18, 2019 #############
Rashid et, al. (2019). Genome-wide comparative analysis of HIF binding sites in Cyprinus carpio for in silico identification of functional hypoxia response elements. 
########################################################### 
DESCRIPTION
All in house Perl scripts for performing different analytical activities and data compilation for genome wide Hypoxia Response Element (HRE) mining in C. carpio and performed comparative analysis with HIF Binding Sites (HBS) of the hypoxia response genes of human and zebrafish.
####################################### 
Removal of unwanted genes
1.	Program ‘HKgeneMapper.pl’ uses human housekeeping (HK) genes as reference and matches the gene symbols with Common carp and zebrafish separately. Further, the program produces the list of matched gene symbol of common carp (HK) and gene symbol list of zebrafish (HK).
2.	Program 'BlastParse.pl' aligned all mRNA of common carp with 'DrHKdb' that is a blast dataset of mRNA of HK genes of zebrafish. The program generates a list of HK GeneID in common carp.
3.	List of HK GeneID obtained from symbol match and alignments are presently placed in placed '/home/iliyas/GenomeWideHRE/GenomicIDsList' with file name 'MapedSymbHKGeneList_commmoncarp.txt' and 'AlignedHKGeneList_commmoncarp.txt' respectively.
4.	Merge both files into 'AllHKGid_CommonCarp.txt' and program 'GenomicAccList.pl' uses the file 'AllHKGid_CommonCarp.txt' for producing ‘extracted genes (EG)’ IDs (by removing (Un)on chromosome, mitochondrion genes and HKG). 
#######################################
 Data collection and preparation
5.	Working path is '/home/iliyas/GenomeWideHRE/' or set your own working path and change path in every program accordingly
6.	Download the gene summary information by uploding IDs of extracted genes (EG) of Cyprinus carpio from the Gene database using NCBI's Entrez search
7.	Program 'GenomicAccList.pl' uses downloaded gene summary files of each species for removing additional gene information (HK gene, Un and mitogenes) from files and generates lists of absolute 'GeneIDs' and (GenomicIDs) genomic accession IDs in the subdirectory 'GenomicIDsList' inside working path.
8.	Uploads Genomic Accession list of species in NCBI's Batch Entrez and Download the corresponding genomic sequences of species and put in subdirectory 'DownloadedGenome'.
9.	Program 'ParseGenomicFileGBnFASTA.pl' explodes individual genomic sequences from downloaded genomic files in the subdirectory 'GenomicIDsList' inside working path. 
######################################
 Upstream parse
10.	Now run program 'UpstreamParse.pl' for parsing the upstream sequences of all reported gene (filterd gene IDS produced by 'GenomicAccList.pl') species wise in a separate folder '/home/iliyas/GenomeWideHRE/upstream'.
 ###################################### 
HRE Mining
11.	Run # perl HREFinder.pl Cyprinus_carpio_upstream_31466.fasta
######################################
 Meta-Analysis of HREFinder Result
12.	Now run 'DatabaseCreation.pl' for tables creation of 'carphre' database
13.	A program 'PositionEvaluate.pl' uses mined HRE file ‘Cyprinus_carpio_upstream_31466_AllMinedHRE.txt' (ie. an output file of HREFinder.pl) file to evaluate localization coordinates on the genomic sequences for gene, upstream, 30 nt long HRE sub-string, HRE motif, HAS motif, and Ebox motif. Further, it populates all evaluated information along with gene information into two tables 'genesummary' and 'upstreaminfo' of the 'carphre' database.
14.	Run program 'MotifClust.pl' for obtaining separate files of gene IDs for (i)All genes of this study,(ii) All HRE,(iii) All HAS,(iv)All E-box for producing Venn diagram using Venny program. This program provides input file to Venny for clustering results.
15.	Run program 'MemeAnalysisDataset.pl' for generating 100 nt long of either side of HRE from upstream sequences for MEME analysis. 
######################################
Comparative analysis with zebrafish
16.	HIF binding sites were identified in 737 differentially expressed genes against hypoxia in a genome wide analysis in Zebrafish ('File1_DifferentialyExpressed' ie. supplementary file 1 of article PubMed ID: 26559940).
17.	Results of this study are available as each entry with UniGene Identifiers.
18.	Perl program 'UniGene2GeneID.pl' uses both (i) result file and (ii) UniGene dataset of D.rerio placed in the working directory for extracting the GeneID for those reported gene.
19.	Now repeats steps of data collection like using gene IDs to download gene summary, genomic sequences, exploding genomic sequences chromosome wise
20.	Parse upstream sequence, mine HRE and perform meta-analysis, and result uploads into database. 
######################################
 Comparative analysis with HIG
21.	Identify the hypoxia inducible genes by scholarly research article
22.	Now repeats steps of data collection like using gene IDs to download gene summary, genomic sequences, exploding genomic sequences chromosome wise
23.	Parse upstream sequence, mine HRE and perform meta-analysis.
24.	Run HsCc_ComparativeAnalysis.pl This program performs comparative analysis between mRNA of hypoxia inducible genes (HIG) of human and mRNA of all protein coding genes of common carp. and stores result into database
25.	Run GeneratesHumanHIGinfotable.pl for generating HIG information along with computed information of upstream and HRE site. 
