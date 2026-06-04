# Phylogenetics Workshop for beginners and non-bioinformaticists - João's Lab - 20260608
This workshop aims to provide a general introduction to phylogenetics, including theories of molecular evolution, mathematical substitution models of sequence evolution, tree inference methods, and bootstrapping. The workshop consists of two parts: theory and practice. You can find the lecture in PowerPoint format inside this repository. 

------

The remaining are practices based on real sequencing data from various *Ophiocordyceps* fungi. This section provides a general pipeline of phylogenetic analysis, from sequence download, alignment, and visualisation, to tree inference and visualisation. To be able to complete the practice, you will need a computer and the following tools installed:  
* [AliView](http://www.ormbunkar.se/aliview/) -- Sequence aligner and alignment visualization tool
* [FigTree](https://tree.bio.ed.ac.uk/software/figtree/) -- Tree visualisation tool. (This is optional. People also use the web tool [iTOL](https://itol.embl.de). We will introduce both tools in the practice.) 

------
# General Introduction to the tasks
Recently, we sequenced a fungal strain labelled as '*Paraisaria amazonica*'; *Paraisaria* is a genus within *Ophiocordyceps*. Our goal is to verify its identity (i.e. if the species is indeed as labelled). This is usually achieved by taxonomic assignment with BLAST tools and phylogenetic reconstruction. We will practice both here.  

# Part 1: BLAST (Basic Local Alignment Search Tool)
BLAST is a tool to compare biological sequences (DNA, RNA, and proteins) against a reference database, such as NCBI GenBank, to find regions of similarity. It allows you to have a quick look at the overall identity of your sequences. Here, we have two nuclear marker genes, TEF and rpb1, sequenced for the strain JPMA317. 

1) Download the files JPMA317_TEF.fna and JPMA317_rpb1.fna from this repository. 
2) Go to [NCBI BLAST webpage](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastn&PAGE_TYPE=BlastSearch&BLAST_SPEC=&LINK_LOC=blasttab&LAST_PAGE=blastx). Use your favourite text editor to open the files and copy and paste the sequence into the box. You can stack the two genes together or run them separately.
3) Then click the BLAST button at the bottom. The run should be finished in seconds.

Try to explore the results a bit. What are the top hits? Are they expected? Can you find any records of *Ophiocordyceps* fungi (hint: *Hirsutella* and *Paraisaria* are both within Ophiocordyceps)? Any differences between the results of two markers genes? Why such differences? Can we make any conclusions from these results?    


