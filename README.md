HaploCount script- Analysis of viral haplotypes in deep sequencing data
==================================
Description
--------------------
The HaploCount script accepts a BAM file as the input. An epitope haplotype is considered, provided it is present in a single contiguous read sequence. Briefly, aligned forward and reverse reads are drawn from the BAM file using samtools. Reads are filtered with fastx toolkit based on a threshold of phred quality of 30 for >95% bases in a read. Reads are translated in all reading frames with transeq tool of the EMBOSS package and the correct reading frames are selected with HMMER based on a user provided training dataset of sequences. The translated reads thus selected are aligned with Muscle and the epitopes are extracted using extractalign tool of the EMBOSS package. Epitope sequence frequencies are calculated and reported. The applications of the script include but are not limited to, continuous viral bNAb epitopes, CD4/CD8 T-cell epitopes and active sites of enzymes. The applicability can be extended to study variation in any stretch of DNA sequence where proximate residues are expected to interact and therefore position specific variation data may not be enough to derive biologically relevant conclusions. 

Dependencies and installation
--------------------
HaploCountV1.sh script by itself does not require any installation, it should work on any machine that can run a bash script. The dependencies include:-
1) fastx toolkit (http://hannonlab.cshl.edu/fastx_toolkit/)
2) samtools (http://www.htslib.org/)
3) EMBOSS package (The European Molecular Biology Open Software Suite) (http://emboss.sourceforge.net/)
4) Muscle aligner (http://www.drive5.com/muscle/)
5) HMMER (http://www.hmmer.org/)

The HaploCountV1.sh has been tested in the following environment-
GNU bash version 4.3.11(1)
fastx toolkit v0.0.13
Samtools v1.3.1-33-gb25695b (using htslib 1.3.1-48-g1c6cf22)
EMBOSS:6.6.0.0
Muscle v3.8.31
HMMER v3.1b2

Following installation of all the dependencies, update paths.sh file with installation paths of each tool. A path for an hmm profile generated based on the sequences alignment of the region of interest needs to be added as well. 

To make the script executable before usage:-
$ chmod +x HaploCountV1.sh    

Usage
--------------------
./HaploCountV1.sh -p paths.sh -b BAMFile.bam -l RegionList.txt -o OutputTag

Additional option -h brings up the above mentioned usage format.
paths.sh file is provided with the script. Update all the paths of the tools installed with an additional path for hmm profile of region of interest.
BAMFile.bam input read alignment map, should not contain any unmapped reads.
RegionList.txt file provided with the script defines the region of interest. The file contains 4 columns viz, epitope name, epitope start wrt the reference sequence used in BAM, epitope end wrt the reference used in BAM and the amino acid sequence of the epitope respectively.
The output tag defines the prefix that will be added to all the resulting files.

There are several dependency tool parameters described in the script comments that can be manually modified according to user requirements.
Test data has been provided along with the script. To be used following modification of path.sh in the test folder as follows:-

./HaploCountV1.sh -b TestData/Test.bam -p TestData/paths.sh -l TestData/haplolist.txt -o Test   

Expected output
--------------------
A directory with the tag name will be created. The directory should contain two files per epitope mentioned in the haplolist.txt file. File 1- Readstats file containing read statistics at different filtration and analysis stages. File 2- Haplotype file containing 3 columns viz, Haplotype sequence, % frequency and number of reads for that haplotype.

--------------------
Written by: Jyoti Sutar <jyoti.sutar92@gmail.com>  
Dept. of Biochemistry and Virology  
National Institute for Research in Reproductive Health (ICMR), Mumbai, India
