# Accessory-scripts
In this folder you will find scripts that are helpful for your long non-coding RNA identification workflow. Below is a description of the job each script performs.


## Modify_gff_coordinates.sh
This script will extend or shorten the gene coordinates found within the genome annotation file that you use in Evolinc. This is useful if you want to change the distance from a gene that you use to annotate a long non-coding RNA as an "intergenic" lncRNA. Currently, Evolinc says that anything not overlapping the 5' or 3' UTRs of a gene is "intergenic", but you may want to make it so that only lncRNAs that are > 500 bp away from a gene are called intergenic. You can use Modify_gff_coordinates.sh to do this.

Run Modify_gff_coordinates.sh like this:

bash Modify_gff_coordinates.sh -g /path/to/GTF/to/modify -v /distance/to/add/to/gene -d /identifier/of/type/of/loci/to/modify

The -v flag will add the same amount to the 5' and 3' ends (i.e., 500bp). You can also use a negative value to make the regions smaller.
The -d flag tells the script which types of loci to look at (i.e., gene, mRNA, GENE, CDS, etc). This is typically found in the 3rd column of your GTF/GFF/GFF3 file.


## clean_fasta_wrapper.sh
This is a simple script to clean up genome FASTA headers. Sometimes headers will contain illegal characters (i.e., "gi|", or pipes) that cause Evolinc to fail. This is just a quick way of cleaning those headers.

Run clean_fasta_wrapper.sh like this:
bash clean_fasta_wrapper.sh -i path/to/input/genome/FASTA -o name/of/cleaned/genome/FASTA


## merge_multiple_gtfs.sh
Have you run Evolinc many times on a lot of different tissues and want to generate a final updated genome annotation file (GTF) and FASTA of lincRNAs for your species of interest? This script accomplishes that by searching through a folder and all of its subdirectories to find the updated.GTF from each Evolinc run. It then merges all of those GTFs into one Final_updated.gtf alongside the known genes for that species. It also generates a FASTA file containing all the lincRNA sequences. Importantly, the Evolinc output GTFs can all have the same name as long as they are in unique sub-directories. For instance, within the folder "Evolinc_output" you can have the sub-directories "Evolinc_output\Run_1\lincRNA.updated.gtf" and "Evolinc_output\Run_2\lincRNA.updated.gtf". Both lincRNA.updated.gtf files will be recognized and merged into one in the end. This is useful if you have many analyses that you would like to merge into one annotation file. The FASTA sequence file can be used directly with Evolinc-II.

Run merge_multiple_gtfs.sh like this:
bash merge_multiple_gtfs.sh -d /parent/directory/all/of/your/Evolinc/output/folders/are/within -g genome/used/to/run/Evolinc -o original/annotation/file/used/with/Evolinc
