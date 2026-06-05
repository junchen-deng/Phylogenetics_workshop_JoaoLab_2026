# Phylogenetics Workshop for beginners and non-bioinformaticists
This workshop aims to provide a general introduction to phylogenetics, including theories of molecular evolution, mathematical substitution models of sequence evolution, tree inference methods, and bootstrapping. The workshop consists of two parts: theory and practice. You can find the lecture in PowerPoint format inside this repository. 

------

The remaining are practices based on real sequencing data from various *Ophiocordyceps* fungi. This section provides a general pipeline of phylogenetic analysis, from sequence download, alignment, and visualisation, to tree inference and visualisation. To be able to complete the practice, you will need a computer and the following tools installed:  
* [AliView](http://www.ormbunkar.se/aliview/) -- Sequence aligner and alignment visualization tool
* [IQ-TREE](https://iqtree.github.io) -- Maximum-likelihood tree inference software. Choose the iqtree3 version for your PC system, and follow [the installation guide](https://iqtree.github.io/doc/Quickstart) 
* [FigTree](https://tree.bio.ed.ac.uk/software/figtree/) -- Tree visualisation tool. (This is optional. People also use the web tool [iTOL](https://itol.embl.de). We will introduce both tools in the practice.) 

------
# General introduction to the tasks
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
Our goal requires us to build a **rooted tree**, which can clearly reflect the relationships among taxa. Finding a proper root is often based on prior knowledge, meaning that you need to go through the literature on a larger phylogenetic scale to find the clade that is monophyletic to our target group (i.e., Ophiocordyceps).

Download the paper '**Sung et al. 2008.pdf**' in this repository, and check **Figure 2**, which shows a phylogeny of Hypocreales fungi. Which clade would be your best candidate for choosing an outgroup for Ophiocordyceps phylogeny?  

If you already have an answer, but you are still unsure, looking for a published Ophiocordyceps phylogeny might be a good option. Download the figure '**Zhuang et al. 2005 Figure 3.png**' in this repository, which shows an Ophiocordyceps phylogeny. Do you choose the same outgroup as they did (hint: *Tolypocladium* is equal to *Elaphocordyceps*)?   

# Part 4: Phylogenetic pipeline -- prepare your list of sequences and alignment
Because we want to know whether the JPMA317 is *Paraisaria amazonica*, we need to sample broadly and specifically, meaning that we need to collect sequences from multiple Ophiocordyceps clades and from multiple *Paraisaria amazonica* strains. 

Check the figure '**Zhuang et al. 2005 Figure 3.png**' again. How many Ophiocordyceps clades does it define? 

As mentioned above, literature often provides a list of accession numbers in the text or in the supplementary data. Then, you can use these numbers to look for sequences of interest in databases like NCBI GenBank. This is often time-consuming. Therefore, I have prepared a list of sequences for you. 

Download the files '**TEF.fna**' and '**rpb1.fna**' in this repository and examine the content. It includes JPMA317, three strains of *Paraisaria amazonica*, *O. ravenelii*, *O. sobolifera* and *O. longissima* (the *O. sobolifera* clade), *O. sphecocephala* and *O. nutans* (the *O. sphecocephala* clade), *O. sinensis* and *O. unilateralis* (the Zombie-ant fungi), and two outgroups *T. inflatum* and *T. ophioglossoide*, 

You might have noticed in Part 1 that the downloaded sequences often have a long header. I personally prefer to shorten it and replace all **spaces** with **underscores** to avoid troubles in some software. (**underscore** is your best friend when preparing text files!!!)  

Now let's do the alignment! We will use the tool **AliView**, which is great for visualising your list of sequences and alignment. 

1) Open **AliView**; copy and paste all sequences of '**TEF.fna**' and '**rpb1.fna**' in two separate windows.
> :warning: **Warning:** You can also drag the file onto the screen, but this will make you edit the original file. Always remember to keep the original file untouched! You don't want to look for the sequences again one by one from NCBI.)  
2) Play a bit with the options at the top of the panel. The most important option for our purpose is **nucleotide translation**.

<img width="433" height="230" alt="Screenshot 2026-06-05 at 13 04 23" src="https://github.com/user-attachments/assets/2b26ef48-8fd8-4e35-b7d2-668911e64ebe" />

3) Now, click the action '**Align**' and choose **Realign everything as Translated Amino Acids**. 
> :warning: **Warning:** You should always align nucleotide sequences as translated amino acids when working with protein-coding genes because this is biologically correct. Unfortunately, many studies failed to do this. In addition, sequences that you download or get from sequencing companies are not always free of stop codons and indels. Sometimes they can even be reversed! You need to manually fix them. When it comes to hundreds of sequences, this can be difficult and time-consuming to finish by hand. This is where bioinformatics shines. 

<img width="390" height="365" alt="Screenshot 2026-06-05 at 13 16 53" src="https://github.com/user-attachments/assets/5fd053cc-c333-427e-8940-78219f6eac89" />

4) Examine the alignment. How satisfied are you? The core region is aligned well, but you might have noticed the long tails at the ends and some misaligned regions. The length difference is because people often amplify only part of the marker gene as the barcode, but genes extracted from genomes are often in full length. The misalignment can be due to sequencing errors. It is recommended to trim them. There are tools (e.g., trimal) that can help to trim alignments, but you can do it manually for a few genes.

The goal of trimming is to reduce the errors and enrich the phylogenetically informative regions, which means to remove large misalignments and low-density regions (i.e., tails; regions retained by only a small percentage of samples (<60%)). I would do the following: 

For TEF:
<img width="902" height="209" alt="Screenshot 2026-06-05 at 21 11 47" src="https://github.com/user-attachments/assets/51dc7df5-fcf5-4d27-bfa7-8819d10b1607" />
<img width="910" height="212" alt="Screenshot 2026-06-05 at 21 13 44" src="https://github.com/user-attachments/assets/70b24c71-c00d-4011-be3a-bd26f18f4f97" />

For rpb1: 
<img width="1055" height="225" alt="Screenshot 2026-06-05 at 15 43 36" src="https://github.com/user-attachments/assets/353cdf06-fb31-4102-8a53-bd077589ed23" />
<img width="1074" height="212" alt="Screenshot 2026-06-05 at 15 45 36" src="https://github.com/user-attachments/assets/0d10c505-b832-41c6-8a44-282421942c4a" />

> :bulb: **Tip:** Tree inference algorithms are often quite robust. They allow a few percentages of errors and low-density regions. The output tree topologies are often similar (you can keep the untrimmed version and run another tree in the next steps). However, the impact can be amplified in a small dataset of a few genes. The best practice is to remove them. Sometimes, errors may occur only in some region within a single sequence. You can often spot it in the alignment, and you should try to trim it from this sequence. 

An example of one erroneous region in one sequence (indicated by the yellow arrow), which doesn't look right:
<img width="1307" height="520" alt="Screenshot 2026-06-05 at 16 09 33" src="https://github.com/user-attachments/assets/325abff0-fa79-477b-94e8-d7c85a2b7627" />

5) Save the trimmed alignments as **TEF_trimmed.fna** and **rpb1_trimmed.fna**. You can also download these two files from this repository.

> :bulb: **Tip:** In AliView, you can ask it to use any tools that you prefer to perform the alignment. Go to AliView '**Settings**' and the tab '**Align ALL program**'. You can provide the command line and path to any tools that you installed. By default, AliView uses **MUSCLE** for the alignment. I personally prefer **MAFFT**.

# Part 5: Phylogenetic pipeline -- tree inference (including gene concatenation, partition, model selection, and bootstrapping) 


bin/iqtree3 -p workshop --prefix Ophio_nucl -m MFP+MERGE -B 1000 --alrt 1000

