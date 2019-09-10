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
```

#run hmm prifle
```
$ anvi-run-hmms -c contigs.db
```

#display contigs stats
```
anvi-display-contigs-stats contigs.db
```

**Profiling BAM files**
#init sorted bam file to generate bai
```
ls -1 *sorted.bam > sorted_bam.txt
$ for sample in $(cat sorted_bam.txt); do anvi-init-bam $sample -o "${sample%.*}"_index.bam; done

#profile: --blank-profile, in case we do not have bam file but just want to view the genome
```

#profile
```
$ anvi-init-bam Aug_M1_C1_D1.reads_Aug_M1_C1_D3_megahit_metabat.266_sorted.bam -o Aug_M1_C1_D1.reads_Aug_M1_C1_D3_megahit_metabat.266_index.bam

$ 
for bam in *_index.bam
do 
anvi-profile -c contigs.db -i $bam  -o ./"${bam%.*}" -T 2 -W
done

#--cluster-contigs
#-W

```

merge profle.db
```
anvi-merge */PROFILE.db -o Aug_M1_C1_D3_megahit_metabat_266_merged -c contigs.db --sample-name Aug_M1_C1_D3_megahit_metabat_266 -W 

#if we do not want to have CONCOCT binning, use --skip-concoct-binning
```

#activae view
```
#without collection
$ anvi-interactive -p Aug_M1_C1_D3_megahit_metabat_266_merged/PROFILE.db -c contigs.db 

#with concoct collection
$ anvi-interactive -p Aug_M1_C1_D3_megahit_metabat_266_merged/PROFILE.db -c contigs.db -C CONCOCT
#
```

#summarize bins
```
anvi-summarize -p Aug_M1_C1_D3_megahit_metabat_266_merged/PROFILE.db -c contigs.db -C CONCOCT
```

#use the refine 
```
anvi-refine -p Aug_M1_C1_D3_megahit_metabat_266_merged/PROFILE.db -c contigs.db -C CONCOCT -b Bin_1
```

#save after refine and then do re-summary

``` 
```
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

**do mapping**
```
for the binning step, we have the data for binnning but with only 10 samples coverage files
we need to do mapping with all 16 samples anyway, to first calcualte the relative abundance, then do the refineM of bins
```
**one example**
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

**mapping 16 metaG to all dRep mags**
```
for file in $(cat /home/projects/Wetlands/2018_sampling/OWC_metaG_megahit/OWC_metaG16_link_list.txt)
do 
echo $file
for MAGs in $(dRep_methanogens_prefix)
do
echo ${MAGs}
bbmap.sh ref=${MAGs}.fa in=/home/projects/Wetlands/2018_sampling/OWC_metaG_megahit/${file}.fq.gz xmtag=t ambiguous=random outm=${MAGs}_${file}.bam threads=6 -Xmx50g &> ${MAGs}_${file}.log
echo "1"
samtools sort -@ 6 ${MAGs}_${file}.bam > ${MAGs}_${file}.sorted.bam
rm ${MAGs}_${file}.bam
done
```

