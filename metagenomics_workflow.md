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

#profile: --blank-profile
$ anvi-init-bam Aug_M1_C1_D1.reads_Aug_M1_C1_D3_megahit_metabat.266_sorted.bam -o Aug_M1_C1_D1.reads_Aug_M1_C1_D3_megahit_metabat.266_index.bam

$ anvi-profile -c contigs.db -i Aug_M1_C1_D1.reads_Aug_M1_C1_D3_megahit_metabat.266_index.bam  -o ./Aug_M1_C1_D3_megahit_metabat.266_blank -S Aug_M1_C1_D3_megahit_266 -W --cluster-contigs

$ anvi-interactive -p Aug_M1_C1_D3_megahit_metabat.266_blank/PROFILE.db -c contigs.db 
#



//$ anvi-import-collection binning_results.txt -p SAMPLES-MERGED/PROFILE.db -c contigs.db --source "SOURCE_NAME"
# find examples here https://github.com/merenlab/anvio/tree/master/anvio/tests/sandbox/example_files_for_external_binning_results

#import collection from outside
anvi-import-collection -C Aug_M1_C1_D3_megahit_metabat_collection -p Aug_M1_C1_D3_megahit_metabat.266_blank/PROFILE.db -c contigs.db Aug_M1_C1_D3_megahit_metabat_contigs.list --contigs-mode

#list collections (old ones, anvi-script-get-collection-info)
 anvi-estimate-genome-completeness -p Aug_M1_C1_D3_megahit_metabat.266_blank/PROFILE.db -c contigs.db --list-collections
#* Aug_M1_C1_D3_megahit_metabat_collection (1 bins, representing 286 items).


#anvi-interactive -p Aug_M1_C1_D3_megahit_metabat.266_blank/PROFILE.db -c contigs.db -C Aug_M1_C1_D3_megahit_metabat_collection


# I need to have a collection???
anvi-summarize -p Aug_M1_C1_D3_megahit_metabat.266_blank/PROFILE.db -c contigs.db -o Aug_M1_C1_D3_megahit_metabat_266_refine -C Aug_M1_C1_D3_megahit_metabat_collection

$ anvi-refine -p Aug_M1_C1_D3_megahit_metabat.266_blank/PROFILE.db -c contigs.db -C Aug_M1_C1_D3_megahit_metabat_collection -b Aug_M1_C1_D3_megahit_metabat_266
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
echo $file
echo ${file}_Aug_M1_C1_D3_megahit_metabat.266.log
bbmap.sh ref=Aug_M1_C1_D3_megahit_metabat.266.fa in=/home/projects/Wetlands/2018_sampling/OWC_metaG_megahit/${file}.fq.gz xmtag=t ambiguous=random outm=${file}_Aug_M1_C1_D3_megahit_metabat.266.bam threads=6 -Xmx50g &> ${file}_Aug_M1_C1_D3_megahit_metabat.266.log
echo "1"
samtools sort -@ 6 ${file}_Aug_M1_C1_D3_megahit_metabat.266.bam > ${file}_Aug_M1_C1_D3_megahit_metabat.266_sorted.bam
rm ${file}_Aug_M1_C1_D3_megahit_metabat.266.bam
done

```
#pkill -u liupf
```
bbmap.sh ref=Aug_M1_C1_D3_megahit_metabat.266.fa in=/home/projects/Wetlands/2018_sampling/OWC_metaG_megahit/Aug_M1_C1_D1.reads.fq.gz xmtag=t ambiguous=random outm=Aug_M1_C1_D1.reads_Aug_M1_C1_D3_megahit_metabat.266.bam threads=6 -Xmx50g &> Aug_M1_C1_D1.reads_Aug_M1_C1_D3_megahit_metabat.266.log
```

