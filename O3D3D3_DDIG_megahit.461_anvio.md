## this is a markdown file of my notes learning anvio

## metagnomcis workflow

**one example using 
**O3D3D3_DDIG_megahit.461**

**creating a contigs_database contigs.fa, **

```
#on my mac, 
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/anvio_refine_MAGs
cd O3D3D3_DDIG_megahit.461

#example
# O3D3D3_DDIG_megahit.461.fa
#creat
anvi-gen-contigs-database -f O3D3D3_DDIG_megahit.461.fa -n 'O3D3D3_DDIG_megahit.461'
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
$ 
for bam in *_index.bam
do 
anvi-profile -c contigs.db -i $bam  -o ./"${bam%.*}" -T 2 
done

#--cluster-contigs
#-W

```

merge profle.db
```
anvi-merge */PROFILE.db -o O3D3D3_DDIG_megahit_461_merged -c contigs.db --sample-name O3D3D3_DDIG_megahit_461_merged  

#if we do not want to have CONCOCT binning, use --skip-concoct-binning
```

#generate and import collections from outside
```
grep '>' O3D3D3_DDIG_megahit.461.fa > O3D3D3_DDIG_megahit.461_head.txt
sed -i -e 's/>//g' O3D3D3_DDIG_megahit.461_head.txt
sed -i -e 's/$/\tO3D3D3_DDIG_megahit\.461/g' O3D3D3_DDIG_megahit.461_head.txt
sed -i -e 's/\./_/g' O3D3D3_DDIG_megahit.461_head.txt

#import collection from outside
anvi-import-collection -C O3D3D3_DDIG_megahit_461_collection -p O3D3D3_DDIG_megahit_461_merged/PROFILE.db -c contigs.db O3D3D3_DDIG_megahit.461_head.txt --contigs-mode
```


#activae view
```
#without collection
$ anvi-interactive -p O3D3D3_DDIG_megahit_461_merged/PROFILE.db -c contigs.db 

#with concoct collection
$ anvi-interactive -p O3D3D3_DDIG_megahit_461_merged/PROFILE.db -c contigs.db -C CONCOCT
anvi-interactive -p O3D3D3_DDIG_megahit_461_merged/PROFILE.db -c contigs.db -C O3D3D3_DDIG_megahit_461_collection
#
```

#summarize bins
```
anvi-summarize -p O3D3D3_DDIG_megahit_461_merged/PROFILE.db -c contigs.db -C CONCOCT
anvi-summarize -p O3D3D3_DDIG_megahit_461_merged/PROFILE.db -c contigs.db -C O3D3D3_DDIG_megahit_461_collection -o Metabat2_summary

```

#use the refine 
```
anvi-refine -p O3D3D3_DDIG_megahit_461_merged/PROFILE.db -c contigs.db -C O3D3D3_DDIG_megahit_461_collection -b O3D3D3_DDIG_megahit_461
anvi-summarize -p O3D3D3_DDIG_megahit_461_merged/PROFILE.db -c contigs.db -C O3D3D3_DDIG_megahit_461_collection -o Metabat2_summary_refined
```

#save after refine and then do re-summary
