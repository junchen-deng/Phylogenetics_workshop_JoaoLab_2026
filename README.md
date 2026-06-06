# Phylogenetics Workshop for beginners and non-bioinformaticists
This workshop aims to provide a general introduction to phylogenetics, including theories of molecular evolution, mathematical substitution models of sequence evolution, tree inference methods, and bootstrapping. The workshop consists of two parts: theory and practice. You can find the lecture in PowerPoint format inside this repository.  

The remaining are practices based on real sequencing data from various *Ophiocordyceps* fungi. This section provides a general pipeline of phylogenetic analysis, from sequence download, alignment, and visualisation, to tree inference and visualisation. To be able to complete the practice, you will need a computer and the following tools installed:  
* [AliView](http://www.ormbunkar.se/aliview/) -- Sequence aligner and alignment visualization tool
* [IQ-TREE](https://iqtree.github.io) -- Maximum-likelihood tree inference software. Choose the iqtree3 version for your PC system, and follow [the installation guide](https://iqtree.github.io/doc/Quickstart) 
* [FigTree](https://tree.bio.ed.ac.uk/software/figtree/) -- Tree visualisation tool 

------
# General introduction to the tasks
Recently, we sequenced a fungal strain labelled as '*Paraisaria amazonica*'; *Paraisaria* is a genus within *Ophiocordyceps*. Our goal is to verify its identity (i.e. if the species is indeed as labelled). This is usually achieved by taxonomic assignment with BLAST tools and phylogenetic reconstruction. We will practice both here.  

# Part 1: BLAST (Basic Local Alignment Search Tool)
BLAST is a tool to compare biological sequences (DNA, RNA, and proteins) against a reference database, such as NCBI GenBank, to find regions of similarity. It allows you to have a quick look at the overall identity of your sequences. Here, we have two nuclear marker genes, TEF and rpb1, sequenced for the strain JPMA317. 

1) Download the files JPMA317_TEF.fna and JPMA317_rpb1.fna from this repository. 
2) Go to [NCBI BLAST webpage](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastn&PAGE_TYPE=BlastSearch&BLAST_SPEC=&LINK_LOC=blasttab&LAST_PAGE=blastx). Use your favourite text editor to open the files and copy and paste the sequence into the box. You can stack the two genes together or run them separately.
3) Then click the BLAST button at the bottom. The run should be finished in seconds.

Go through the results. What are the top hits? Are they expected? Can you find any records of *Ophiocordyceps* fungi (hint: *Hirsutella* and *Paraisaria* are also part of Ophiocordyceps)? Any differences between the results of the two marker genes? Why such differences? Can we draw any conclusions from these results?    

# Part 2: Phylogenetic pipeline -- sequence download from GenBank
You might have some uncertainties about the identity of the strain JPMA317 after performing the BLAST search in part 1. This reflects the limitation of using the BLAST search alone for taxonomic assignment. Even though *Paraisaria amazonica* is a strain that has been sequenced many times, the BLAST search sometimes cannot tell. Just pretend that we don't know the 'truth' and let's move on to build a tree instead.

Remember that our goal is to find the placement of the strain JPMA317 in the genus Ophiocordyceps, and we assume that the species is *Paraisaria amazonica*. Let's check if someone else has sequenced this species by searching for the phrase '**Paraisaria amazonica**' in [GenBank](https://www.ncbi.nlm.nih.gov). Check the records under '**Nucleotide**'. What do you see?

Now, locate the first record of the gene TEF from the search. The first one on my search list is the one with the accession number MF416509. To find the sequence, simply click the **FASTA** icon under the record and then copy, paste and save it to a text file. In most cases, you would need to extract more than one sequence. To batch download the records, select the boxes on the left of the ones you are interested in, click '**Send to**' on the top right, choose '**Complete Record**', '**File**', format '**FASTA**', and then click '**Create File**'. If no boxes were checked, this action will download all the records listed.  

<img width="573" height="432" alt="Screenshot 2026-06-04 at 16 54 41" src="https://github.com/user-attachments/assets/d057fc59-e6cb-49d4-bbb9-1673bd362d80" />

> :bulb: **Tip:** When searching through literature for sequence information, you will often find the accession number (e.g., MF416509) of each sequence. You can easily batch download hundreds of GenBank records with a list of accession numbers. For this purpose, you will need bioinformatics tools, which are out of the scope of this workshop.

# Part 3: Phylogenetic pipeline -- choose the root and taxa
Our goal requires us to build a **rooted tree**, which can clearly reflect the relationships among taxa. Finding a proper root is often based on prior knowledge, meaning that you need to go through the literature on a larger phylogenetic scale to find the clade that is monophyletic to our target group (i.e., Ophiocordyceps).

Download the paper '**Sung et al. 2008.pdf**' in this repository, and check **Figure 2**, which shows a phylogeny of Hypocreales fungi. Which clade would be your best candidate for choosing an outgroup for Ophiocordyceps phylogeny?  

If you already have an answer, but you are still unsure, looking for a published Ophiocordyceps phylogeny might be a good option. Download the figure '**Zhuang et al. 2005 Figure 3.png**' in this repository, which shows an Ophiocordyceps phylogeny. Do you choose the same outgroup as they did (hint: *Tolypocladium* is equal to *Elaphocordyceps*)?   

# Part 4: Phylogenetic pipeline -- prepare your list of sequences and alignment
Because we want to know whether the JPMA317 is *Paraisaria amazonica*, we need to sample broadly and specifically, meaning that we need to collect sequences from multiple Ophiocordyceps clades and from multiple *Paraisaria amazonica* strains. 

Check the figure '**Zhuang et al. 2005 Figure 3.png**' again. How many Ophiocordyceps clades does it define? 

As mentioned above, literature often provides a list of accession numbers in the text or in the supplementary data. Then, you can use these numbers to look for sequences of interest in databases like NCBI GenBank. This is often time-consuming. Therefore, I have prepared a list of sequences for you. 

Download the files '**TEF.fna**' and '**rpb1.fna**' in this repository and examine the content. It includes JPMA317, three strains of *Paraisaria amazonica*, *O. ravenelii*, *O. sobolifera* and *O. longissima* (the *O. sobolifera* clade), *O. sphecocephala* and *O. nutans* (the *O. sphecocephala* clade), *O. sinensis* and *O. unilateralis* (the Zombie-ant fungi), and two outgroups *T. inflatum* and *T. ophioglossoide*. 

> :bulb: **Tip:** You might have noticed in Part 1 that the downloaded sequences often have a long header. I personally prefer to shorten it and replace all **spaces** with **underscores** to avoid troubles in some software. (**underscore** is your best friend when preparing text files!!!)  

Now let's do the alignment! We will use the tool **AliView**, which is great for visualising your list of sequences and performing the alignment. 

1) Open **AliView**; copy and paste all sequences of '**TEF.fna**' and '**rpb1.fna**' in two separate windows.
> :warning: **Warning:** You can also drag the file onto the screen, but this will make you edit the original file. Always remember to keep the original file untouched! You don't want to look for the sequences again one by one from NCBI.)  
2) Play a bit with the options at the top of the panel. The most important option for our purpose is **nucleotide translation**.

<img width="433" height="230" alt="Screenshot 2026-06-05 at 13 04 23" src="https://github.com/user-attachments/assets/2b26ef48-8fd8-4e35-b7d2-668911e64ebe" />

3) Now, click the option '**Align**' and choose **Realign everything as Translated Amino Acids**. 
> :warning: **Warning:** You should always align nucleotide sequences as translated amino acids when working with protein-coding genes because this is biologically correct. Unfortunately, many studies failed to do this. In addition, sequences that you download or get from sequencing companies are not always free of stop codons and indels. Sometimes they even need to be reversed! You need to manually fix them. When it comes to hundreds of sequences, this can be difficult and time-consuming to finish by hand. This is where bioinformatics shines. 

<img width="390" height="365" alt="Screenshot 2026-06-05 at 13 16 53" src="https://github.com/user-attachments/assets/5fd053cc-c333-427e-8940-78219f6eac89" />

4) Examine the alignment. How satisfied are you? Are there any well-aligned regions? You might have noticed the long tails at the ends and some misaligned regions. The length difference is because people often amplify only part of the marker gene as the barcode, but genes extracted from genomes are often in full length. The misalignment can be due to sequencing errors. It is recommended to trim them. There are tools (e.g., [trimAl](https://vicfero.github.io/trimal/)) that can help to trim alignments, but you can do the same thing manually for a few genes.

The goal of trimming is to reduce the errors and enrich the phylogenetically informative regions, which means to remove large misalignments and low-density regions (i.e., tails; regions retained by only a small percentage of samples). I would do the following: 

For TEF:
<img width="902" height="209" alt="Screenshot 2026-06-05 at 21 11 47" src="https://github.com/user-attachments/assets/51dc7df5-fcf5-4d27-bfa7-8819d10b1607" />
<img width="910" height="212" alt="Screenshot 2026-06-05 at 21 13 44" src="https://github.com/user-attachments/assets/70b24c71-c00d-4011-be3a-bd26f18f4f97" />

For rpb1: 
<img width="1055" height="225" alt="Screenshot 2026-06-05 at 15 43 36" src="https://github.com/user-attachments/assets/353cdf06-fb31-4102-8a53-bd077589ed23" />
<img width="1074" height="212" alt="Screenshot 2026-06-05 at 15 45 36" src="https://github.com/user-attachments/assets/0d10c505-b832-41c6-8a44-282421942c4a" />

> :bulb: **Tip:** Tree inference algorithms are often quite robust. They allow a few percentages of errors and low-density regions. The output tree topologies are often similar (If you have time, you can keep the untrimmed version and run another tree in the next steps). However, the impact can be amplified in a small dataset of a few genes. The best practice is to remove them. Sometimes, errors may occur only in some region within a single sequence. You can often spot it in the alignment, and you should try to trim it from this sequence. 

An example of one erroneous region in one sequence (indicated by the yellow arrow), which doesn't look right:
<img width="1307" height="520" alt="Screenshot 2026-06-05 at 16 09 33" src="https://github.com/user-attachments/assets/325abff0-fa79-477b-94e8-d7c85a2b7627" />

5) Save the trimmed alignments as **TEF_trimmed.fna** and **rpb1_trimmed.fna**. You can also download these two files from this repository.

> :bulb: **Tip:** In AliView, you can ask it to use any aligners that you prefer. Go to AliView '**Settings**' and the tab '**Align ALL program**'. You can provide the command line and path to any tools that you have installed. By default, AliView uses **MUSCLE** for the alignment. I personally prefer **[MAFFT](https://mafft.cbrc.jp/alignment/server/index.html)**.

# Part 5: Phylogenetic pipeline -- tree inference (with gene concatenation, gene partition, model selection, and bootstrapping) and a bit of bioinformatics
We have everything ready for the tree! We will use the tool **IQTREE** for this purpose.  

1) Within the IQTREE installation folder, create a new folder named '**data**' and put both **TEF_trimmed.fna** and **rpb1_trimmed.fna** inside (It's only to make it easy for everyone. But if you understand a bit more of bioinformatics, you can have this new folder anywhere with any names)
  
2) Follow the [the IQTREE installation guide](https://iqtree.github.io/doc/Quickstart), open the Command Prompt window (Run the **Terminal** app in Mac and '**cmd**' in Windows), go to the IQTREE installation folder (Use '**cd**'), and run the following command. ('**data**' indicates the folder where we put the data. It is indeed the path to this folder. If you have your data stored somewhere else, you need to provide the full path.) 

```
bin/iqtree3 -p data --prefix Ophio_nucl -m MFP+MERGE -B 1000 --alrt 1000
```

To understand what each argument does, run '**bin/iqtree3 --help** ' in the Prompt window. We have two genes, and each of them likely fits with a different model. Therefore, it is best to treat them separately (i.e., **partition by gene**). **-p** usually takes in a partition file. However, IQTREE can do the partition automatically if you input a data folder. This is what we are doing here. **--prefix** sets the prefix to the names of all output files. **-m** sets the model. **MFP** automatically determines the best-fit model by testing all available models (i.e., **Model Selection**), and **MERGE** merges partitions to increase model fit (i.e., if multiple partitions fit similar models, treating them as one may be better). **-B** enables Ultra-fast bootstrapping and **--alrt** enables SH-aLRT bootstrapping.   

If you have time, you can run IQTREE on a single alignment, TEF or rpb1, and compare the results later. The command is like this: 

```
bin/iqtree3 -s PATH_TO_THE_ALIGNMENT --prefix Ophio_nucl -m MFP -B 1000 --alrt 1000
```

> :bulb: **Tip:** There are many different ways of partitioning your alignment (e.g., partition by codon). In this case, you will need to prepare your own partition file and include both **-s** (for data) and **-p** (for partition). Note that we use two types of bootstraps. It is recommended because they use different algorithms to calculate the value, and the Ultrafast bootstrapping is often overconfident. You would be confident with a clade if SH-aLRT >= 80% and UFboot >= 95%. Read more [here](https://iqtree.github.io/doc/Frequently-Asked-Questions).  

# Part 6: Phylogenetic pipeline -- tree visualisation 
If IQTREE runs successfully, it will produce a long series of logs on the screen. The output files are generated in the location where you run IQTREE. In our case, this will be the IQTREE installation folder. You can also find the output of the run I did under the folder **IQTREE_result** in this repository. 

Launch the software **FigTree**. Go to **File**, **Open...**. Choose to open the file **Ophio_nucl.treefile**, which stores the tree in **Newick** format. In the pop-up window, set the name to **bootstrap**. Select the branch leading to the two outgroups and click **Reroot** on the top panel. Go to **Trees** on the left panel, tick the box of **Order nodes** and select **decreasing**. Go to **Tip labels** and increase the **Font size** as you want. Tick the box of **Branch Labels**. Choose **bootstrap** for **Display** and increase the font size a bit. Now the tree should look prettier. Go to **File**, **Export PDF...** to save your tree for future editing. (This tree is also inside the folder **IQTREE_result** in this repository under the name **Ophio_nucl.pdf**)

Take a look at the tree. Where is JPMA317? Is this what you expected? Compare the topology of other taxa with the Ophiocordyceps tree in the figure '**Zhuang et al. 2005 Figure 3.png**. Are they similar? Look at the bootstrap numbers. Are you confident with this topology?

> :bulb: **Tip:** Other output files contain information about model selection and the tree itself. For example, you will find out which bootstrap number represents which bootstrapping method in the file **Ophio_nucl.iqtree**. The number at the bottom of the tree (e.g., 0.04) indicates the estimated number of nucleotide substitutions per site. It is one way to calculate the **genetic distance** between two taxa.  

> Additionally, there are other free tools to visualise the tree, such as the website [iTOL](https://itol.embl.de). It may provide more functions than FigTree. But I often just save the tree in PDF and use a vector image editor, such as [Inkscape](https://inkscape.org), to do further editing. 

# Additional resources for nerds
[DTU Computational Molecular Evolution course](https://teaching.healthtech.dtu.dk/22115/index.php/22115_-_Computational_Molecular_Evolution#Week_1_(February_4):_Introduction_to_evolutionary_theory_and_population_genetics._Models_of_growth,_selection_and_mutation)  
[Free book 'Phylogenetics in the Genomic Era'](https://inria.hal.science/PGE/page/table-of-contents)

Author: Junchen Deng  
Date: 2026 June 08



