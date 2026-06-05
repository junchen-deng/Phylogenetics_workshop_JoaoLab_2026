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

Try to explore the results a bit. What are the top hits? Are they expected? Can you find any records of *Ophiocordyceps* fungi (hint: *Hirsutella* and *Paraisaria* are both within Ophiocordyceps)? Any differences between the results of the two marker genes? Why such differences? Can we draw any conclusions from these results?    

# Part 2: Phylogenetic pipeline -- sequence download from GenBank
You might have some uncertainties about the identity of the strain JPMA317 after performing the BLAST search in part 1. This reflects the limitation of using the BLAST search alone for taxonomic assignment. Even though *Paraisaria amazonica* is a strain that has been sequenced many times, the BLAST search sometimes cannot tell. Just pretend that we don't know the 'truth' and let's move on to build a tree instead.

Remember that our goal is to find the placement of the strain JPMA317 in the genus Ophiocordyceps, and we assume that the species is *Paraisaria amazonica*. Let's check if someone has sequenced this species by searching for the phrase '**Paraisaria amazonica**' in [GenBank](https://www.ncbi.nlm.nih.gov). Check the records under '**Nucleotide**'. What do you see?

Now, locate the first record of the gene TEF from the search. The first one on my search list is the one with the accession number MF416509. To find the sequence, simply click the **FASTA** icon under the record and then copy, paste and save it to a text file. In most cases, you would need to extract more than one sequence. To batch download the records, select the boxes on the left of the ones you are interested in, click '**Send to**' on the top right, choose '**Complete Record**', '**File**', format '**FASTA**', and then click '**Create File**'. If no boxes were checked, this action will download all the listed records.  

<img width="573" height="432" alt="Screenshot 2026-06-04 at 16 54 41" src="https://github.com/user-attachments/assets/d057fc59-e6cb-49d4-bbb9-1673bd362d80" />

> :bulb: **Tip:** When searching through literature for sequence information, you will often find the accession number (e.g., MF416509) of each sequence. You can batch download hundreds of GenBank records with a list of accession numbers. For this purpose, you will need bioinformatics tools, which are out of the scope of this workshop.

# Part 3: Phylogenetic pipeline -- choose the root and taxa
Our goal requires us to build a **rooted tree**, which can clearly reflects the relationships among taxa. Finding a proper root is often based on prior knowledge, meaning that you need to go through the literature on a larger phylogenetic scale to find the clade that is monophyletic to our target group (i.e., Ophiocordyceps).

Download the paper '**Sung et al. 2008.pdf**' in this repository, and check **Figure 2**, which shows a phylogeny of Hypocreales fungi. Which clade would be your best candidate for choosing a outgroup for Ophiocordyceps phylogeny?  



