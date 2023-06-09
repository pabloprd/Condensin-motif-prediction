# Condensin motif prediction using neural networks


# Introduction
Our goal was to find the motifs that are related to binding condensin (a protein) within some sequences in yeast using a convolutional neural network. To do this we had to identify condensin peaks (when condensin is the most highly active in the cell). ChIP-seq accomplished this by using an antibody against a condensin subunit. Cells are crosslinked with formaldehyde for protein-DNA interaction stabilization and then fragmented into smaller pieces. These pieces containing the condensin subunit are then immunoprecipated using an antibody against the subunit of interest. These fragments are then sequenced and the reads are mapped to the reference genome to generate a genome-wide map of condensin occupancy.

This data was collected from both Log (active) and Quiescent (dormant) cells. In this intial set of files, we were provided ChIP-seq peaks (called by MACS2) in both the log and quiescent cell state.


For the ChIP-seq peak calls, there are files in two formats, .narrowPeak and .bed. The .bed is much more straightforward but the .narrowPeak gives more information about the location of the entire peak (not just the summit of the peak, but also the length).

For .narrowPeak, the columns are: chromosome #, chromosome start position, chromosome end position, name, score, strand (not included in our data), enrichment value, p value, q value, peak (the distance of peak summit from chromosome start).

For .bed, the columns are:
chromosome #, chromosome start position of peak summit, chromosome end position of peak summit, name, p value.



# Process

We used the neural network and methods from the Basset paper: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4937568/

This convolutional neural network and its associated methods were modified for our project involving condensin. The summary of the process is as follows: We read our input files (the ChiP-seq data provided by Dr. Swygert) and modified the format (by padding them) so the CNN would be able to accept them. From there we created training, validation, and testing datasets. We trained the models on different motif lengths to decide which one would be the best.

The Convolutional neural network used for this project ultimately defines whether what you input (after the model is trained) is a motif or not. But what we did based on the Basset paper was to extract the motifs from each filter of the CNN. This gave us a list of probable Condensin motifs. 


# Conclusions
We found no similarities bewteen the sequences we found and the sequences generated by a popular motif predictor in MEME-CHiP. However, we measured motif occurrences and locations as well. We observed that chromosomes 4,8, and 12 were where the most motifs were found. We then visualized the motif locations in IGV alongside .bed files containg domain boundaries (specific region in genome that marks transition between adjacent domains), for the purpose of determining if sequence domains were at all related to motif locations. In the chromosomes with the highest occurence of condensin motifs (4 and 12) we found extremely high relatedness between the domains and the motifs. 


# Footnote 
This project was done mostly over google drive with collaborators: Jonathon Yallop and Soumik Ghosh. The condensin ChiP-seq data was created by Dr. Swygert of Colorado State Univeristy. This github repository is currently unifinished as of June 7th 2023, since many of the source files used to generate the Juypter notebook were not efficiently organized due to time constraints. Currently working on uploading neccessary files to have a working and sourceable repository. For now, Master_final_project.ipynb shows the output of our working jupyter notebook. 
