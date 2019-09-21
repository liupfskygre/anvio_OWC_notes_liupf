## mapping on summit, get bam file for anvio

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

#O3D3_metabatSS.87
```
sbatch run_bbmap_summit_MetaG16_Mg24.sh metaG16_raw_reads.txt O3D3_metabatSS.87 O3D3_metabatSS.87.fa 
# Submitted batch job 3188957
#14:24 

```
