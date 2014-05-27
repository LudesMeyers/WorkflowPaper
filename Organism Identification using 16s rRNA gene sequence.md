#Organism Identification using 16s rRNA gene sequence
In a classroom or undergraduate research setting the project may not have a particular bacterial species in mind. In this case it is necessary to screen the 16S Sanger sequencing results for possible genome sequencing candidates.  We recommend starting with BLAST results, then continuing onto the Genomes Online Database (GOLD), and simply Google searching.  In many cases it will be handy to also build a phylogenetic tree to aid in identification since the BLAST results may not be sufficiently informative.

##BLAST 16S rDNA sequence
Begin by navigating to the Standard Nucleotide BLAST at NCBI:

http://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastn&PAGE_TYPE=BlastSearch&LINK_LOC=blasthome

Paste in your Sanger consensus sequence.  We recommend checking the box to exclude Uncultured/environmental sample sequences since these will not be informative for identification. Be sure the nucleotide collection (nr/nt) is selected under database and click the BLAST button.

##Interpreting the results
Depending on the quality of the Sanger sequencing and the particular bacteria sequenced, the BLAST results can range from definitive to relatively uninformative. Examples of both are discussed below.

1. In FigureX, it is not necessary to build a phylogenetic tree for further identification. All of the top hits are either Kocuria rosea or Kocuria sp, have e-values of 0.0, perfect query coverage, and 99% to 100% identity. In this case, proceed to "Using GOLD".
2. In FigureX the results are much more ambiguous. The results show more than 99% identity to multiple species within multiple genera. In this case, proceed to "Making a Phylogenetic Tree", before using GOLD.

##Using GOLD (the Genomes Online Database)
Go to: http://genomesonline.org/cgi-bin/GOLD/index.cgi

Click the search button on the left side of the page and you should be taken to a page that looks like the screen shot displayed in FigureX.

Fill out the blue Organism Information (Organism Name) section, with information about your microbe from BLAST and click submit search.  We usually search for only the genus to get a sense for how well that genus is represented in the database and which species are present. FigureX shows an example screen shot of the results for "Lysinibacillus." FigureX is zoomed in on the lower results window. In this case there are two sequenced strains of Lysinibacillus fusiformis, and one of Lysinibacillus sphericus. A couple other species are "incomplete". A choice of how to proceed in light of this information will depend on the goals of the project. Some "incomplete" projects will never progress and some could already be on their way to publication.

If you have relatively ambiguous identification results (e.g. you think you have some sort of Lysinibacillus but aren't sure which species) it could be worthwhile to perform an alignment of your 16S sequence with those from genomes already in Genbank.

##Align 16S Sequences using Align Sequences Nucleotide BLAST
First locate the 16S sequences of the genome you'd like to compare to, in FigureX, we searched the NCBI Nucleotide database for "lysinibacillus fusiformis 16S gene ZB2".

http://www.ncbi.nlm.nih.gov/nuccore/

Click on the sequence of interest, then click on the "FASTA" link to get the sequence in FASTA format. Now navigate to the "Align Sequences Nucleotide BLAST" page:

http://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE_TYPE=BlastSearch&BLAST_SPEC=blast2seq&LINK_LOC=align2seq

Paste in the two 16S rDNA sequences and click on the "BLAST" button. In FigureX the identity was 98% over 87% of the query. Unless the primers used for both your sequence and the sequence you are comparing to were amplified with the same primers, the query coverage will not be 100%.  A low identity can be the result of poor sequence quality or taxonomic distance. 

A choice of whether to sequence an organism based on these results depends on the project goal. For example an identity of 100% suggests that at least at the 16S level, the candidate organism is very similar to what is already in the database. However, many organisms vary greatly in gene content between strains and an additional genome may still be informative. There is also significant debate over what level of relatedness at the 16S level should be used to determine the difference between species, or if this is even a relevant question \cite{Chan_2012}\cite{Drancourt_2005}\cite{Hanage_2006}\cite{Stackebrandt_2002}.

