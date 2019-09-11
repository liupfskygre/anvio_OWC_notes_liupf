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
