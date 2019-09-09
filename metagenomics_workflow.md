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

#anvi-display-contigs-stats contigs.db

```

**binnning but with 10 samples coverage files**
