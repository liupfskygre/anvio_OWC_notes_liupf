## mapping on summit, get bam file for anvio

## click on the Red when using Anvio, highlight All to locate the source of redundancy

## list of MAGs
```
O3D3_metabatSS.87
Aug_M1_C1_D3_megahit_metabat.266
O3D3D3_DDIG_megahit.4
O3C3D3_DDIG_MN.967
O3C3D3_DDIG_MN.569
OWC_substrative_co_megahit_Deep_metabat.815
OWC_subtractive_megahit_Surface_metabat.783
Aug_OW2_C1_D5_megahit_metabat.368
O3C3D4_idba_metabatSS.159
OWC_substrative_co_megahit_Deep_metabat.1305
May_M1_C1_D1_megahit_metabat.122
O3C3D4_idba_metabatSS.114
O3D3_metabatSS.114
Aug_N3_C1_D1_megahit_metabat.230
M3C5D1_DDIG_MN.345
O3C3D4_DDIG_MN.831
O3C3D3_DDIG_MN.808
Aug_M1_C1_D3_megahit_metabat.302
Aug_M1C1D1_idbak60_metabat_bin.117
Aug_M1_C1_D2_megahit_metabat.5
M3C4D3_v1_idba.136
O3D3D3_DDIG_megahit.461
30_Metabat_PLANT_2015_08
124_Metabat_MUD_2014_2015_coassembly
```

#get fasta file
```
# /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_methanogens_db374_20Sept/Methanogens_db_dRep_20Spet2019_dRep2/dereplicated_genomes

# copy the fasta file of MAGs needs to be refined from 95 dRep Methanogens

#to
/home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_methanogens_db374_20Sept/Methanogens_db_dRep_20Spet2019_dRep2/MAGs_needs_refined

#check and chage the name of fasta file
#anvio do not want # begins the file name
mv 30_Metabat_PLANT_2015_08.fa PLANT_2015_08_Metabat_30.fa
mv 124_Metabat_MUD_2014_2015_coassembly.fa MUD_2014_2015_coassembly_Metabat_124.fa

#check the scaffold name
head -2 *.fa

```

#copy data to summit
```
cd /scratch/summit/liupf@colostate.edu
mkdir Methanogens_decon_MAGs

#globus transfer data to summit /scratch/summit/liupf@colostate.edu/Methanogens_decon_MAGs
### TURN OFF END POINT on zenith
$ /opt/globusconnectpersonal-2.3.6/globusconnectpersonal -start &
$ /opt/globusconnectpersonal-2.3.6/globusconnectpersonal -stop
#end point transfer, https://app.globus.org/endpoints


#summit
$ cd /scratch/summit/liupf@colostate.edu/Methanogens_decon_MAGs
$ /scratch/summit/liupf@colostate.edu/Methanogens_decon_MAGs/MAGs_needs_refined

```

#change the name of raw contigs
```
cd /scratch/summit/liupf@colostate.edu/raw_metaG_reads
# OWC_Aug_M1_C1_D1
mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_M1_C1_D1_B_[OWC_Aug_M1_C1_D1_FD] OWC_Aug_M1_C1_D1
mv 12757.4.282994.GTCTCCTT-AAGGAGAC.fastq.gz OWC_Aug_M1_C1_D1.fastq.gz

#
mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_M1_C1_D2_B_[OWC_Aug_M1_C1_D2_FD] OWC_Aug_M1_C1_D2

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_M1_C1_D3_B_[OWC_Aug_M1_C1_D3_FD] OWC_Aug_M1_C1_D3

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_M1_C1_D4_B_[OWC_Aug_M1_C1_D4_FD] OWC_Aug_M1_C1_D4

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_M1_C1_D5_B_[OWC_Aug_M1_C1_D5_FD] OWC_Aug_M1_C1_D5

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_M2_C1_D1_C_[OWC_Aug_M2_C1_D1_FD] OWC_Aug_M2_C1_D1


mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_M2_C1_D5_C_[OWC_Aug_M2_C1_D5_FD] OWC_Aug_M2_C1_D5


mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_N3_C1_D1_A_[OWC_Aug_N3_C1_D1_FD] OWC_Aug_N3_C1_D1

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_N3_C1_D5_A_[OWC_Aug_N3_C1_D5_FD] OWC_Aug_N3_C1_D5

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_OW2_C1_D1_C_[OWC_Aug_OW2_C1_D_2_FD] OWC_Aug_OW2_C1_D1

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_OW2_C1_D5_C_[OWC_Aug_OW2_C1_D_FD] OWC_Aug_OW2_C1_D5

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_T1_C1_D1_A_[OWC_Aug_T1_C1_D1_FD] OWC_Aug_T1_C1_D1

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_Aug_T1_C1_D5_A_[OWC_Aug_T1_C1_D5_FD] OWC_Aug_T1_C1_D5

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_May_M1_C1_D1_A_[OWC_May_M1_C1_D1_FD] OWC_May_M1_C1_D1

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_May_M1_C1_D3_A_[OWC_May_M1_C1_D3_FD] OWC_May_M1_C1_D3

mv From_genomes_to_methane_production__Targeting_critical_knowledge_gaps_in_wetland_soils__OWC_May_M1_C1_D6_A_[OWC_May_M1_C1_D6_FD] OWC_May_M1_C1_D6

# 
cd /scratch/summit/liupf@colostate.edu/raw_metaG_reads

for i in OWC_Aug_M1_C1_D2 OWC_Aug_M1_C1_D3 OWC_Aug_M1_C1_D4 OWC_Aug_M1_C1_D5 OWC_Aug_M2_C1_D1 OWC_Aug_M2_C1_D5 OWC_Aug_N3_C1_D1 OWC_Aug_N3_C1_D5 OWC_Aug_OW2_C1_D1 OWC_Aug_OW2_C1_D5 OWC_Aug_T1_C1_D1 OWC_Aug_T1_C1_D5 OWC_May_M1_C1_D1 OWC_May_M1_C1_D3 OWC_May_M1_C1_D6
do
cd $i
echo ${i}
cd Raw_Data
mv *.fastq.gz ${i}.fastq.gz
echo 'done'
cd ..
cd ..
done

```

#print path for mapping
```
for i in OWC_Aug_M1_C1_D2 OWC_Aug_M1_C1_D3 OWC_Aug_M1_C1_D4 OWC_Aug_M1_C1_D5 OWC_Aug_M2_C1_D1 OWC_Aug_M2_C1_D5 OWC_Aug_N3_C1_D1 OWC_Aug_N3_C1_D5 OWC_Aug_OW2_C1_D1 OWC_Aug_OW2_C1_D5 OWC_Aug_T1_C1_D1 OWC_Aug_T1_C1_D5 OWC_May_M1_C1_D1 OWC_May_M1_C1_D3 OWC_May_M1_C1_D6
do
cd $i
cd Raw_Data
#pwd 
ls -1
cd ..
cd ..
done

```

```
OWC_Aug_M1_C1_D1.fastq.gz
OWC_Aug_M1_C1_D2.fastq.gz
OWC_Aug_M1_C1_D3.fastq.gz
OWC_Aug_M1_C1_D4.fastq.gz
OWC_Aug_M1_C1_D5.fastq.gz
OWC_Aug_M2_C1_D1.fastq.gz
OWC_Aug_M2_C1_D5.fastq.gz
OWC_Aug_N3_C1_D1.fastq.gz
OWC_Aug_N3_C1_D5.fastq.gz
OWC_Aug_OW2_C1_D1.fastq.gz
OWC_Aug_OW2_C1_D5.fastq.gz
OWC_Aug_T1_C1_D1.fastq.gz
OWC_Aug_T1_C1_D5.fastq.gz
OWC_May_M1_C1_D1.fastq.gz
OWC_May_M1_C1_D3.fastq.gz
OWC_May_M1_C1_D6.fastq.gz
```

#modify run_bbmap_summit.sh to run mapping#
```
cd /scratch/summit/liupf@colostate.edu/Methanogens_decon_MAGs/MAGs_needs_refined
```

#1, O3D3_metabatSS.87
```
sbatch run_bbmap_summit_MetaG16_Mg24.sh metaG16_raw_reads.txt O3D3_metabatSS.87 O3D3_metabatSS.87.fa 
# Submitted batch job 3188957
#14:24 
```

#2 Aug_M1_C1_D3_megahit_metabat.266
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt Aug_M1_C1_D3_megahit_metabat.266 Aug_M1_C1_D3_megahit_metabat.266.fa 
squeue|grep liupf
```

#3, O3D3D3_DDIG_megahit.4
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3D3D3_DDIG_megahit.4 O3D3D3_DDIG_megahit.4.fa 
```

#4,O3C3D3_DDIG_MN.967

```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D3_DDIG_MN.967 O3C3D3_DDIG_MN.967.fa 
 
```

#5, O3C3D3_DDIG_MN.569
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D3_DDIG_MN.569 O3C3D3_DDIG_MN.569.fa 
```
6, OWC_substrative_co_megahit_Deep_metabat.815
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt OWC_substrative_co_megahit_Deep_metabat.815 OWC_substrative_co_megahit_Deep_metabat.815.fa
```
7, OWC_subtractive_megahit_Surface_metabat.783
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt OWC_subtractive_megahit_Surface_metabat.783 OWC_subtractive_megahit_Surface_metabat.783.fa

```
8, Aug_OW2_C1_D5_megahit_metabat.368
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt Aug_OW2_C1_D5_megahit_metabat.368 Aug_OW2_C1_D5_megahit_metabat.368.fa

```
9, O3C3D4_idba_metabatSS.159
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D4_idba_metabatSS.159 O3C3D4_idba_metabatSS.159.fa

```
10,OWC_substrative_co_megahit_Deep_metabat.1305
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt OWC_substrative_co_megahit_Deep_metabat.1305 OWC_substrative_co_megahit_Deep_metabat.1305.fa

```
11, May_M1_C1_D1_megahit_metabat.122
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt May_M1_C1_D1_megahit_metabat.122 May_M1_C1_D1_megahit_metabat.122.fa
```
12, O3C3D4_idba_metabatSS.114
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D4_idba_metabatSS.114 O3C3D4_idba_metabatSS.114.fa

```
13, O3D3_metabatSS.114
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3D3_metabatSS.114 O3D3_metabatSS.114.fa

```
14, Aug_N3_C1_D1_megahit_metabat.230
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt Aug_N3_C1_D1_megahit_metabat.230 Aug_N3_C1_D1_megahit_metabat.230.fa
```
15, M3C5D1_DDIG_MN.345
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt M3C5D1_DDIG_MN.345 M3C5D1_DDIG_MN.345.fa
#Submitted batch job 3189038 wrong
```
16, O3C3D4_DDIG_MN.831
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D4_DDIG_MN.831 O3C3D4_DDIG_MN.831.fa
```
17, O3C3D3_DDIG_MN.808
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D3_DDIG_MN.808 O3C3D3_DDIG_MN.808.fa

```
18, Aug_M1_C1_D3_megahit_metabat.302
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt Aug_M1_C1_D3_megahit_metabat.302 Aug_M1_C1_D3_megahit_metabat.302.fa
```
19, Aug_M1C1D1_idbak60_metabat_bin.117
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt Aug_M1C1D1_idbak60_metabat_bin.117 Aug_M1C1D1_idbak60_metabat_bin.117.fa
```
20, Aug_M1_C1_D2_megahit_metabat.5
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt Aug_M1_C1_D2_megahit_metabat.5 Aug_M1_C1_D2_megahit_metabat.5.fa
```
21, M3C4D3_v1_idba.136
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt M3C4D3_v1_idba.136 M3C4D3_v1_idba.136.fa
```
22, O3D3D3_DDIG_megahit.461
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3D3D3_DDIG_megahit.461 O3D3D3_DDIG_megahit.461.fa
```
PLANT_2015_08_Metabat_30.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt PLANT_2015_08_Metabat_30 PLANT_2015_08_Metabat_30.fa

```

124_Metabat_MUD_2014_2015_coassembly
```
finished on zenith
```

```
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_Methanogens_MAGs248_db28June2019/dRep_methanogens_28June2019/dereplicated_genomes

screen -S samtools

/home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_bins_refine_anvio

for MAGs in $(cat bbmap_file.list)
do 
echo ${MAGs}
cd $MAGs
for file in *.sam
do
echo "${file%.*}"
samtools view -@ 6 -bS $file > "${file%.*}".bam
samtools sort -@ 6 "${file%.*}".bam > "${file%.*}".sorted.bam
rm $file
rm "${file%.*}".bam
done
cd ..
done
```

#anvio on MAC
```
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/anvio_refine_MAGs

for MAGs in $(cat bbmap_file.list)
do 
echo ${MAGs}
cd $MAGs
for file in *.fa
do
echo "${file%.*}"
#creat
anvi-gen-contigs-database -f ${file} -n 'Methanogens_anvio'
anvi-run-hmms -c contigs.db
done
cd ..
done
```


#index bam file
```
for MAGs in $(cat bbmap_file.list)
do 
echo ${MAGs}
cd $MAGs
ls -1 *.bam > sorted_bam.txt
for sample in $(cat sorted_bam.txt)
do 
anvi-init-bam $sample -o "${sample%.*}"_index.bam
done
cd ..
done

```

profile
```
#for MAGs in M3C5D1_DDIG_MN.345_bbmap_out
for MAGs in $(cat bbmap_file.list) #change the list accordingly
do 
echo ${MAGs}
cd $MAGs
for bam in *sorted_index.bam
do 
anvi-profile -c contigs.db -i $bam  -o ./"${bam%.*}" -T 2 
done
anvi-merge */PROFILE.db -o Methanogens_merged_profile -c contigs.db --sample-name Methanogens_merged_profile
cd ..
done

```

#creat collection from bins 
```
for MAGs in $(cat bbmap_file_full.list) #23
do 
echo ${MAGs}
cd $MAGs
for file in *.fa
do
grep '>' ${file} > seq_header.txt
sed -i -e 's/>//g' seq_header.txt
sed -i -e 's/$/\tMAGs_from_megahit/g' seq_header.txt
done
cd ..
done
```

#import collection
```
for MAGs in $(cat bbmap_file_full.list) #23
do 
echo ${MAGs}
cd $MAGs
anvi-import-collection -C Meta_collection -p Methanogens_merged_profile/PROFILE.db -c contigs.db seq_header.txt --contigs-mode
cd ..
done
```

#summarize
```
for MAGs in $(cat bbmap_file_full.list) #23
do 
echo ${MAGs}
cd $MAGs
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary
cd ..
done

```

#viz interactive
```
anvi-interactive -p Methanogens_merged_profile/PROFILE.db -c contigs.db 

```

### refine each genomes
```
cd to each bbmap
anvi-refine Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
```

#Aug_M1C1D1_idbak60_metabat_bin.117_bbmap_out
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd Aug_M1C1D1_idbak60_metabat_bin.117_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 

Aug_M1C1D1_idbak60_metabat_Anvio.117
```
#Aug_M1_C1_D2_megahit_metabat.5_bbmap_out??? not working

```
cd Aug_M1_C1_D2_megahit_metabat.5_bbmap_out 

anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 

```
Aug_M1_C1_D3_megahit_metabat.266_bbmap_out

```
cd Aug_M1_C1_D3_megahit_metabat.266_bbmap_out

anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
Aug_M1_C1_D3_megahit_metabat_Anvio.266.fa
```

Aug_M1_C1_D3_megahit_metabat.302_bbmap_out ???not working
```
cd Aug_M1_C1_D3_megahit_metabat.302_bbmap_out

anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 

```

Aug_N3_C1_D1_megahit_metabat.230_bbmap_out
```
cd Aug_N3_C1_D1_megahit_metabat.230_bbmap_out

anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
Aug_N3_C1_D1_megahit_metabat_Anvio.230.fa
```
Aug_OW2_C1_D5_megahit_metabat.368_bbmap_out
```
cd Aug_OW2_C1_D5_megahit_metabat.368_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
Aug_OW2_C1_D5_megahit_metabat_Anvio.368.fa
```

#M3C4D3_v1_idba.136_bbmap_out
```
cd M3C4D3_v1_idba.136_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
M3C4D3_v1_idba_Anvio.136
```

#M3C5D1_DDIG_MN.345_bbmap_out ??? not working
```
cd M3C5D1_DDIG_MN.345_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
```
#May_M1_C1_D1_megahit_metabat.122_bbmap_out
```
cd May_M1_C1_D1_megahit_metabat.122_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 

May_M1_C1_D1_megahit_metabat_Anvio.122

```

#O3C3D3_DDIG_MN.569_bbmap_out
```
cd O3C3D3_DDIG_MN.569_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 

O3C3D3_DDIG_MN_Anvio.569
```

#O3C3D3_DDIG_MN.808_bbmap_out

```
cd O3C3D3_DDIG_MN.808_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
O3C3D3_DDIG_MN_Anvio.808

```
#O3C3D3_DDIG_MN.967_bbmap_out
```
cd O3C3D3_DDIG_MN.967_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
O3C3D3_DDIG_MN_Anvio.967
```

#O3C3D4_DDIG_MN.831_bbmap_out
```
cd O3C3D4_DDIG_MN.831_bbmap_out

anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
O3C3D4_DDIG_MN.Anvio.831
```

#O3C3D4_idba_metabatSS.114_bbmap_out
```
cd O3C3D4_idba_metabatSS.114_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
O3C3D4_idba_metabatSS.Anvio.114
```

O3C3D4_idba_metabatSS.159_bbmap_out
```
cd O3C3D4_idba_metabatSS.159_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
O3C3D4_idba_metabatSS.Anvio.159

```
O3D3D3_DDIG_megahit.461_bbmap_out
```
cd O3D3D3_DDIG_megahit.461_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
O3D3D3_DDIG_megahit.Anvio.461
```

#O3D3D3_DDIG_megahit.4_bbmap_out
```
cd O3D3D3_DDIG_megahit.4_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 

O3D3D3_DDIG_megahit.Anvio.4
```
#O3D3_metabatSS.114_bbmap_out

```
cd O3D3_metabatSS.114_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
O3D3_metabatSS.Anvio.114

```
#O3D3_metabatSS.87_bbmap_out

```
cd O3D3_metabatSS.87_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 

O3D3_metabatSS.Anvio.87
```
OWC_substrative_co_megahit_Deep_metabat.1305_bbmap_out
```
cd OWC_substrative_co_megahit_Deep_metabat.1305_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 

OWC_substrative_co_megahit_Deep_metabat.Anvio.1305
```

OWC_substrative_co_megahit_Deep_metabat.815_bbmap_out
```
cd OWC_substrative_co_megahit_Deep_metabat.815_bbmap_out

anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
OWC_substrative_co_megahit_Deep_metabat.Anvio.815
```

OWC_subtractive_megahit_Surface_metabat.783_bbmap_out
```
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
OWC_subtractive_megahit_Surface_metabat.Anvio.783
```

PLANT_2015_08_Metabat_30_bbmap_out
```
cd PLANT_2015_08_Metabat_30_bbmap_out

anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit

#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 
PLANT_2015_08_Metabat_30.Anvio
```
#checkM
```
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_bins_refine_anvio/Refine_list_fa

screen -S chekcM
/home/projects/Wetlands/2018_sampling/scripts/run_checkm.sh Refine_list_fa fa ./ ./Refine_list_fa_checkM

#gtdbtk
/home/projects/Wetlands/2018_sampling/scripts/run_gtdbtk.sh Refine_list_fa

Using GTDB-Tk reference data version r89: /opt/gtdbtk/data/release89/

#merge
python /home/projects/Wetlands/2018_sampling/scripts/add_gtdbtk_tax_to_checkm.py Refine_list_fa_checkm_summary.txt gtdbtk_out/Refine_list_fa.bac120.summary.tsv gtdbtk_out/Refine_list_fa.ar122.summary.tsv >Refine_list_fa_checkm_gtdbtk_summary.txt
```

#four genomes needs to refine again 
```
Aug_M1C1D1_idbak60_metabat_Anvio.117
May_M1_C1_D1_megahit_metabat_Anvio.122
O3C3D3_DDIG_MN_Anvio.808.Anvio
```
PLANT_2015_08_Metabat_30.Anvio
