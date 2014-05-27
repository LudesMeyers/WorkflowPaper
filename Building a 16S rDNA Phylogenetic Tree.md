#Building a 16S rDNA Phylogenetic Tree

What _is_ this thing? At this point, you have an organism in pure culture, but you don't know what it is. If you found a creature crawling on the ground and
wanted to identify (or classify) it, you might look at it's morphology and ask what it most _looks_ like. If it has six legs, you might guess it's some kind of
insect. If it has hard outer wings folded over its back, you might guess that it's some kind of beetle. If it also had antler-style horns on its head, you might
guess that it's some kind of stag beetle. If you don't have enough information available to guess what kind of stag beetle you have, then you have reached the
limit of *taxonomic resolution* for your creature. 

With an unknown microbial species, the best way to identify it is to sequence one of its genes (most people
use the 16S rRNA gene) and ask what _it_ most looks like. With animal classification, the key features to examine are things like legs and wings and horns; with microbial
classification, the key features to examine are the nucleotides in different positions in a DNA sequence. Fortunately, we have computer programs to help us make
sense of the DNA sequence information. Our preferred approach to classifying microbial species is to place an unknown sequence in the context of a
phylogenetic tree of known sequences. Building a phylogenetic tree from a 16S rRNA sequence is fairly straightforward, but the interpretation of the tree can be
a bit of an art. Here, we attempt to guide you through both. However, some complicated cases will require consultation with an expert in the field of
phylogenetics or systematics.

The outline of the workflow is to use the Ribosomal Database Project (RDP) to generate an alignment of the sequence with close relatives and an outgroup,
following by cleanup of the RDP headers, tree-building with FastTree and viewing/interpretation of the tree using Dendroscope.

##Obtain an RDP alignment

The goal of this section is to obtain a 16S alignment from RDP that can be used to build a tree. This procedure has the added benefit of providing an independent verification of the taxonomic assignment of your sequence based on the BLAST results.

1. Go to rdp.cme.msu.edu 
2. Create an account 
3. Click on my RDP/login 
4. Upload the fasta file containing your 16s sequence 
5. Assign it a group name (this is what the program will label your sequence/organism). Choose this carefully since that will be the name on the final tree. 
6. Click the "+" next to the sequence, to add it to your cart
7. Click on CLASSIFIER at the top of the page
8. Click on "Do Classification With Selected Sequences" button. This will show you a hierarchical view of the classification of your sequence (from Phylum to Genus.) You will use this information to navigate to other sequences that you want to include in your alignment that you will use to build your phylogenetic tree. For example, Figure X shows the hierarchy for the _Tatumella_ 16S sequence. 
8. Click on BROWSERS. We recommend openining BROWSERS in a new tab so that you can keep the hierarchy information handy.
9. Click on "Isolates" to select only isolates for further analysis.  Then click "Browse"
10. Click on the + sign next to "Archaea outgroup." This will add an Archaeal sequence to your cart, which will be used to root your phylogenetic tree.
11. If using the example sequence provided, click on "Proteobacteria", then Gammaproteobacteria, then "Enterobacteriales", then Enterobacteriaceae. This will take you to the Genus Tatumella, which currently has over 69 species in it. If the genus you are working with has too many sequences to analyze easily (for example, _Bacillus_ currently has >26000,) one way to reduce this number is to exclude the uncultured taxa in the database. To do this, scroll down to the Data Set Options and click on the "Isolates" button. Click "Refresh" and you will see that there are fewer sequences in the Genus. To reduce this number further, click on the "Type" Strain button. As a worst-case scenario, you will need to manually select a subset of organisms to include in your alignment.
12. Click on the + sign next to **genus** Tatumella to add all of those sequences to your cart.
13. Click on "Sequence Cart" and confirm that your uploaded sequence, the outgroup sequence, and all of the other sequences you'd like to include in your tree are displayed.
14. Click on "download," leave the download options as the defaults (fasta, aligned, uncorrected ,) and then click on the appropriate download button. Save the file and then rename it to something informative.

##Clean up the RDP taxon names

The RDP alignment will have taxon names that most of the downstream software tools will not tolerate because they consist of special text characters. So, we have written a little Perl script (CleanupRDP.pl) that will remove those special characters and replace them with underscores. This script will be included in the data download from github. To run CleanupRDP.pl, first move it to your Applications folder. Then, in a Terminal window, navigate to the directory that contains the RDP alignment that you've just downloaded. Then, type:

    perl /Applications/CleanupRDP.pl -i RDP_alignment.fa -o RDP_alignemnt_clean.fa

##Building the Tree with FastTree 
Go to http://www.microbesonline.org/fasttree/#Install
and download the FastTree.c program by right clicking on it and saving the link to your Applications folder. To compile the software, navigate to your Applications folder in a Terminal window:

    cd /Applications
Then, type:

    gcc -O3 -finline-functions -funroll-loops -Wall -o FastTree FastTree.c -lm

FastTree requires a gcc compiler. If your attempt to compile FastTree fails, this is the most likely reason. You can download and install the gcc compiler from Xcode here https://developer.apple.com/downloads/index.action?q=xcode

In order to download Xcode you will need to register as a developer with Apple which takes only a couple of minutes. After you register, click on the apple next to "Developer" at the top of the page. Then, click on the Xcode download link, which will ultimately take you to the Mac App Store, where you can follow the instructions to install Xcode. Once it is installed, open the program and open preferences (under the Xcode tab). Click on the downloads option and install the command line tools. 

Once you have successfully downloaded and installed Xcode and the command line tools, return to your Applications folder in a Terminal window and type again:

    gcc -O3 -finline-functions -funroll-loops -Wall -o FastTree FastTree.c -lm
    
Now, you should have a working version of FastTree. To build your tree, using the cleaned up RDP alignment, type:

    /Applications/FastTree -nt RDP_alignemnt_clean.fa > tree_file.tre 

The output name ends in ".tre" to ensure that it will be recognized by Dendroscope.

##Viewing the Tree in Dendroscope
Download and install Dendroscope.
http://ab.inf.uni-tuebingen.de/software/dendroscope/

You will need to obtain a license here
http://www-ab2.informatik.uni-tuebingen.de/software/dendroscope/register/

Enter the license number into Dendrosope and then you can open your phylogenetic tree from the File menu to view it.

Once the tree is visible, the first step is to re-root the tree to the outgroup. Expand the tree by clicking the expansion button (labeled in Figure X), then scroll through the tree to locate the outgroup. Click on the beginning of the taxa name, to select it, and reroot the tree by going to edit and selecting re-root.

We recommend viewing the tree as a phylogram which can be accomplished by clicking on the phylogram button (labeled in Figure X). From this tree it should be possible to determine the phylogenetic placement of the candidate sequence, and in some cases to give it a name with more certainty than a simple BLAST search.  Below are examples of a relatively informative tree and a relatively uninformative tree:

TI
 
In tree shown above (genus Brachybacterium), our sample of interest from an assembly is "Brachybacterium muris UCD-AY4" \cite{Lo_2013}. It falls within a clade where every named member has the same name "Brachybacterium muris", and this name does not occur elsewhere on the tree. Hence, we were confident enough to name our sample as that species. In other words, this sequence falls within a well-supported (note 0.999 bootstrap support,) monophyletic clade of _Brachybacterium muris_.
 
In the tree shown above (genus Microbacterium) our species of interest is Microbacterium sp. str. UCD-TDU \cite{Bendiks_2013}. In contrast to the Brachybacterium example, here our species falls within a poorly defined clade containing multiple species. In this case we did not assign a species name to this isolate.
