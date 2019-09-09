## this is a markdown file of my notes learning anvio

## metagnomcis workflow

**one example using 
**Aug_M1_C1_D3_megahit_metabat.266**

**creating a contigs_database contigs.fa, **

```
#on my mac, 
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/anvio_refine_MAGs
cd Aug_M1_C1_D3_megahit_metabat.266

#example
# Aug_M1_C1_D3_megahit_metabat.266.fa
#creat
anvi-gen-contigs-database -f Aug_M1_C1_D3_megahit_metabat.266.fa -n 'Aug_M1_C1_D3_megahit_metabat.266'


#skip hmm prifle
$ anvi-run-hmms -c contigs.db

#
anvi-display-contigs-stats contigs.db


#??? bam files on the way
for sample in `cat SAMPLE_IDs`; do anvi-init-bam $sample-RAW.bam -o $sample.bam; done

#profile
$ anvi-profile -c contigs.db --blank-profile -o ./Aug_M1_C1_D3_megahit_metabat.266_blank -S Aug_M1_C1_D3_megahit_266 -W

$ anvi-interactive -p Aug_M1_C1_D3_megahit_metabat.266_blank/PROFILE.db -c contigs.db
#

$ anvi-import-collection binning_results.txt -p SAMPLES-MERGED/PROFILE.db -c contigs.db --source "SOURCE_NAME"
# find examples here https://github.com/merenlab/anvio/tree/master/anvio/tests/sandbox/example_files_for_external_binning_results

# I need to have a collection???
anvi-summarize -p Aug_M1_C1_D3_megahit_metabat.266_blank/PROFILE.db -c contigs.db -o Aug_M1_C1_D3_megahit_metabat_266_refine
```

**binnning but with 10 samples coverage files**


```
#pwd, put all metaG16 names in the txt file
/home/projects/Wetlands/2018_sampling/OWC_metaG_megahit
OWC_metaG16_link_list.txt


#keep only mapped reads with outm= <file> or mappedonly=f +out= <file>
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_Methanogens_MAGs248_db28June2019/dRep_methanogens_28June2019/dereplicated_genomes

screen -S liu_mapping

for file in $(cat /home/projects/Wetlands/2018_sampling/OWC_metaG_megahit/OWC_metaG16_link_list.txt)

do 
echo $ $file
bbmap.sh ref=Aug_M1_C1_D3_megahit_metabat.266.fa in=/home/projects/Wetlands/2018_sampling/OWC_metaG_megahit/$file.fq.gz xmtag=t ambiguous=random outm=$file_Aug_M1_C1_D3_megahit_metabat.266.bam threads=6 -Xmx50g 

samtools sort -@ 6 $file_Aug_M1_C1_D3_megahit_metabat.266.bam > $file_Aug_M1_C1_D3_megahit_metabat.266_sorted.bam

rm $file_Aug_M1_C1_D3_megahit_metabat.266.bam

done

```
