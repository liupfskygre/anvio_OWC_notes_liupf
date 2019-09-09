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

#
anvi-display-contigs-stats contigs.db

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
