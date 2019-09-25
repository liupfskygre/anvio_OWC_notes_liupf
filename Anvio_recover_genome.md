## for Methangoens genoms with CP>50%, Ct>25%

##use anvio to recover

##then do dRep on the clean database(50%-10%), for genomes from dRep dataset before cleanup, if it is not meet 50%-10% quality, 
not include in dRep, but used for later analysis, e.g., mapping

##for 
```
M3C4D4_idba_metabatSS.16
O3C3D3_DDIG_MN.366
Aug_M1C1D5_idba_k60_maxbin2.205
OWC_subtractive_megahit_Surface_metabat.462
35_ESOM_MUD_2014_11
O3C3D3_idba.19
OWC_subtractive_megahit_Surface_metabat.701
O3C3D3_DDIG_megahit.237 ##the name were changed in the list, but the .fa is not changed
O3C3D4_idba_metabatSS.88
OWC_subtractive_megahit_Surface_metabat.897
Aug_M1C1D5_metaHit_metabat_bin.139
OWC_MG_enrich2015_idba_metabat.10
O3C3D3_idba.85
OWC_Enrichment_Methanothrix_Bin5
Aug_M1C1D1_metaHit_metabat_bin.35
O3C3D4_idba_metabatSS.126
O3C3D4_DDIG_metabat.1018
O3C3D3_DDIG_MN.1182
O3C3D3_DDIG_megahit.559 ##
M3C4D3_v1_idba.66
36_ESOM_MUD_2014_11
OWC_subtractive_megahit_Surface_metabat.953
121_Metabat_MUD_2014_2015_coassembly
OWC_MG_enrich2015_idba_metabat.42
O3C3D4_idba_metabatSS.154
```

on zenith
```

/home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly
mkdir Methangoens_db_Cp50Ctl25_Anvio
cd Methangoens_db_Cp50Ctl25_Anvio

nano Methangoens_db_Cp50Ctl25_Anvio.list ##25 genomes

for file in $(cat Methangoens_db_Cp50Ctl25_Anvio.list)
do
cp /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_methanogens_db374_20Sept/${file}.fa ./
done

#O3D3C3 name issue, 
cp /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_methanogens_db374_20Sept/O3D3D3_DDIG_megahit.237.fa ./

cp /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_methanogens_db374_20Sept/O3D3D3_DDIG_megahit.559.fa ./

#rename
mv 121_Metabat_MUD_2014_2015_coassembly.fa  MUD_2014_2015_coassembly_Metabat_121.fa
mv 35_ESOM_MUD_2014_11.fa MUD_2014_11_ESOM_35.fa                   
mv 36_ESOM_MUD_2014_11.fa MUD_2014_11_ESOM_36.fa 


#zenith
cd ~
/opt/globusconnectpersonal-2.3.6/globusconnectpersonal -start &

```

#transfer to summit for mapping
```
#on summit
cd /scratch/summit/liupf@colostate.edu
mkdir Methangoens_db_Cp50Ctl25_Anvio

# /scratch/summit/liupf@colostate.edu/Methangoens_db_Cp50Ctl25_Anvio

```
## mapping using metaG 16
```
cd /scratch/summit/liupf@colostate.edu/Methangoens_db_Cp50Ctl25_Anvio

#copy scripts and metaG list
[liupf@colostate.edu@login10 MAGs_needs_refined]$ cp run_bbmap_summit_MetaG16_Mg24_2.sh /scratch/summit/liupf@colostate.edu/Methangoens_db_Cp50Ctl25_Anvio

[liupf@colostate.edu@login10 MAGs_needs_refined]$ cp metaG16_raw_reads.txt /scratch/summit/liupf@colostate.edu/Methangoens_db_Cp50Ctl25_Anvio
```

## mapping
1, Aug_M1C1D1_metaHit_metabat_bin.35.fa 
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt Aug_M1C1D1_metaHit_metabat_bin.35 Aug_M1C1D1_metaHit_metabat_bin.35.fa
squeue|grep liupf

```

2, Aug_M1C1D5_idba_k60_maxbin2.205.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt Aug_M1C1D5_idba_k60_maxbin2.205 Aug_M1C1D5_idba_k60_maxbin2.205.fa

```

3, Aug_M1C1D5_metaHit_metabat_bin.139.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt Aug_M1C1D5_metaHit_metabat_bin.139 Aug_M1C1D5_metaHit_metabat_bin.139.fa
Submitted batch job 3202102

```

4, M3C4D3_v1_idba.66.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt M3C4D3_v1_idba.66 M3C4D3_v1_idba.66.fa
Submitted batch job 3202104

```

5, M3C4D4_idba_metabatSS.16.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt M3C4D4_idba_metabatSS.16 M3C4D4_idba_metabatSS.16.fa
Submitted batch job 3202106
```

6, MUD_2014_11_ESOM_35.fa
```
sed -i -e 's/35_ESOM_MUD_2014_11\.fa//1' MUD_2014_11_ESOM_35.fa
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt MUD_2014_11_ESOM_35 MUD_2014_11_ESOM_35.fa
Submitted batch job 3202109

```

7, MUD_2014_11_ESOM_36.fa

```
sed -i -e 's/36_ESOM_MUD_2014_11\.fa//1' MUD_2014_11_ESOM_36.fa
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt MUD_2014_11_ESOM_36 MUD_2014_11_ESOM_36.fa
Submitted batch job 3202110

```

8, MUD_2014_2015_coassembly_Metabat_121.fa

```

sed -i -e 's/121_Metabat_MUD_2014_2015_coassembly\.fa//1' MUD_2014_2015_coassembly_Metabat_121.fa
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt MUD_2014_2015_coassembly_Metabat_121 MUD_2014_2015_coassembly_Metabat_121.fa
Submitted batch job 3202112

```

9, O3C3D3_DDIG_MN.1182.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D3_DDIG_MN.1182 O3C3D3_DDIG_MN.1182.fa
Submitted batch job 3202113

```

10, O3C3D3_DDIG_MN.366.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D3_DDIG_MN.366 O3C3D3_DDIG_MN.366.fa

```

11, O3C3D3_idba.19.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D3_idba.19 O3C3D3_idba.19.fa
Submitted batch job 3202118

```

12, O3C3D3_idba.85.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D3_idba.85 O3C3D3_idba.85.fa
Submitted batch job 3202119

```

13, O3C3D4_DDIG_metabat.1018.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D4_DDIG_metabat.1018 O3C3D4_DDIG_metabat.1018.fa
Submitted batch job 3202121

```

14, O3C3D4_idba_metabatSS.126.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D4_idba_metabatSS.126 O3C3D4_idba_metabatSS.126.fa
Submitted batch job 3202122

```

15, O3C3D4_idba_metabatSS.154.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D4_idba_metabatSS.154 O3C3D4_idba_metabatSS.154.fa
Submitted batch job 3202123

```

16, O3C3D4_idba_metabatSS.88.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D4_idba_metabatSS.88 O3C3D4_idba_metabatSS.88.fa
Submitted batch job 3202124

```

17, O3D3D3_DDIG_megahit.237.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3D3D3_DDIG_megahit.237 O3D3D3_DDIG_megahit.237.fa
Submitted batch job 3202125

```

18, O3D3D3_DDIG_megahit.559.fa

```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3D3D3_DDIG_megahit.559 O3D3D3_DDIG_megahit.559.fa
Submitted batch job 3202126

```

19,OWC_Enrichment_Methanothrix_Bin5.fa

```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt OWC_Enrichment_Methanothrix_Bin5 OWC_Enrichment_Methanothrix_Bin5.fa
Submitted batch job 3202128

```
20,OWC_MG_enrich2015_idba_metabat.10.fa
 
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt OWC_MG_enrich2015_idba_metabat.10 OWC_MG_enrich2015_idba_metabat.10.fa
Submitted batch job 3202130

```

21,OWC_MG_enrich2015_idba_metabat.42.fa
```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt OWC_MG_enrich2015_idba_metabat.42 OWC_MG_enrich2015_idba_metabat.42.fa
Submitted batch job 3202131

```

22, OWC_subtractive_megahit_Surface_metabat.462.fa

```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt OWC_subtractive_megahit_Surface_metabat.462 OWC_subtractive_megahit_Surface_metabat.462.fa
Submitted batch job 3202133

```
23, OWC_subtractive_megahit_Surface_metabat.701.fa

```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt OWC_subtractive_megahit_Surface_metabat.701 OWC_subtractive_megahit_Surface_metabat.701.fa
Submitted batch job 3202135

```
24, OWC_subtractive_megahit_Surface_metabat.897.fa

```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt OWC_subtractive_megahit_Surface_metabat.897 OWC_subtractive_megahit_Surface_metabat.897.fa
Submitted batch job 3202137

```

25, OWC_subtractive_megahit_Surface_metabat.953.fa

```
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt OWC_subtractive_megahit_Surface_metabat.953 OWC_subtractive_megahit_Surface_metabat.953.fa
Submitted batch job 3202138

```

==> MUD_2014_2015_coassembly_Metabat_121.fa <==
>121_Metabat_MUD_2014_2015_coassembly.fascaffold_2079
==> MUD_2014_11_ESOM_36.fa <==
>36_ESOM_MUD_2014_11.fascaffold_1
==> MUD_2014_11_ESOM_35.fa <==
>35_ESOM_MUD_2014_11.fascaffold_97


```
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_Methanogens_MAGs248_db28June2019/dRep_methanogens_28June2019/dereplicated_genomes

screen -r samtools

cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methangoens_db_Cp50Ctl25_Anvio

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

#anvio on MAC, creat db
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
anvi-gen-contigs-database -f Aug_M1C1D1_metaHit_metabat_bin.35.fa -n 'Methanogens_anvio'

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
#for MAGs in Aug_M1C1D1_metaHit_metabat_bin.35_bbmap_out
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
for MAGs in $(cat bbmap_file.list) #25
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
for MAGs in $(cat bbmap_file.list) #25
do 
echo ${MAGs}
cd $MAGs
anvi-import-collection -C Meta_collection -p Methanogens_merged_profile/PROFILE.db -c contigs.db seq_header.txt --contigs-mode
cd ..
done
```

#summarize
```
for MAGs in $(cat bbmap_file.list) #25
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

#xx_bbmap_out
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd xxxx_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 

xx.117
```
```
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methangoens_db_Cp50Ctl25_Anvio

sed -e 's/_bbmap_out//1' bbmap_file.list >bbmap_file_prefix.list

for file in $(cat bbmap_file_prefix.list)
do
sed -e "s/xxxx/$file/1" temp.txt > ${file}_anvio.txt
done
```
```
Aug_M1C1D1_metaHit_metabat_bin.35_bbmap_out
Aug_M1C1D5_idba_k60_maxbin2.205_bbmap_out
Aug_M1C1D5_metaHit_metabat_bin.139_bbmap_out
M3C4D3_v1_idba.66_bbmap_out
M3C4D4_idba_metabatSS.16_bbmap_out
MUD_2014_11_ESOM_35_bbmap_out
MUD_2014_11_ESOM_36_bbmap_out
MUD_2014_2015_coassembly_Metabat_121_bbmap_out
O3C3D3_DDIG_MN.1182_bbmap_out
O3C3D3_DDIG_MN.366_bbmap_out
O3C3D3_idba.19_bbmap_out
O3C3D3_idba.85_bbmap_out
O3C3D4_DDIG_metabat.1018_bbmap_out
O3C3D4_idba_metabatSS.126_bbmap_out
O3C3D4_idba_metabatSS.154_bbmap_out
O3C3D4_idba_metabatSS.88_bbmap_out
O3D3D3_DDIG_megahit.237_bbmap_out
O3D3D3_DDIG_megahit.559_bbmap_out
OWC_Enrichment_Methanothrix_Bin5_bbmap_out
OWC_MG_enrich2015_idba_metabat.10_bbmap_out
OWC_MG_enrich2015_idba_metabat.42_bbmap_out
OWC_subtractive_megahit_Surface_metabat.462_bbmap_out
OWC_subtractive_megahit_Surface_metabat.701_bbmap_out
OWC_subtractive_megahit_Surface_metabat.897_bbmap_out
OWC_subtractive_megahit_Surface_metabat.953_bbmap_out
```
#
```
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/Methangoens_db_Cp50Ctl25_Anvio

cd Aug_M1C1D1_metaHit_metabat_bin.35_bbmap_out 
anvi-run-hmms -c contigs.db -H /Users/pengfeiliu/anvio_dataset/gtdbtk_marker/Arc_122_marker
#after run this after the profile step, the summarize is not working anymore??

anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary

#try without profile??not help :(
anvi-profile -c contigs.db -i Aug_M1C1D1_metaHit_metabat_bin.35_OWC_Aug_OW2_C1_D5.sorted_index.bam  -o ./Aug_M1C1D1_metaHit_metabat_bin.35_OWC_Aug_OW2_C1_D5 -T 2  --cluster-contigs

anvi-import-collection -C Meta_collection -p Aug_M1C1D1_metaHit_metabat_bin.35_OWC_Aug_OW2_C1_D5/PROFILE.db -c contigs.db seq_header.txt --contigs-mode

anvi-summarize -p Aug_M1C1D1_metaHit_metabat_bin.35_OWC_Aug_OW2_C1_D5/PROFILE.db -c contigs.db -C Meta_collection -o Single_Refine_summary
```


```
cd Aug_M1C1D5_idba_k60_maxbin2.205_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```

Aug_M1C1D5_metaHit_metabat_bin.139_bbmap_out
```
cd Aug_M1C1D5_metaHit_metabat_bin.139_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
#######
cd M3C4D3_v1_idba.66_bbmap_out
```
cd M3C4D3_v1_idba.66_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary

```

cd M3C4D4_idba_metabatSS.16_bbmap_out
```
cd M3C4D4_idba_metabatSS.16_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
cd MUD_2014_11_ESOM_35_bbmap_out
```
cd MUD_2014_11_ESOM_35_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```

cd MUD_2014_11_ESOM_36_bbmap_out
```
cd MUD_2014_11_ESOM_36_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```

cd MUD_2014_2015_coassembly_Metabat_121_bbmap_out
```

cd MUD_2014_2015_coassembly_Metabat_121_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```

cd O3C3D3_DDIG_MN.1182_bbmap_out
```
cd O3C3D3_DDIG_MN.1182_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```

cd O3C3D3_DDIG_MN.366_bbmap_out
```
cd O3C3D3_DDIG_MN.366_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```

cd O3C3D3_idba.19_bbmap_out

```

cd O3C3D3_idba.19_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```


>>>>
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd O3C3D3_idba.85_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd O3C3D4_DDIG_metabat.1018_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd O3C3D4_idba_metabatSS.126_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd O3C3D4_idba_metabatSS.154_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd O3C3D4_idba_metabatSS.88_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd O3D3D3_DDIG_megahit.237_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd O3D3D3_DDIG_megahit.559_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd OWC_Enrichment_Methanothrix_Bin5_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd OWC_MG_enrich2015_idba_metabat.10_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd OWC_MG_enrich2015_idba_metabat.42_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd OWC_subtractive_megahit_Surface_metabat.462_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd OWC_subtractive_megahit_Surface_metabat.701_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd OWC_subtractive_megahit_Surface_metabat.897_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
```
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

cd OWC_subtractive_megahit_Surface_metabat.953_bbmap_out
anvi-refine -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
#remove to 0 contamination
anvi-summarize -p Methanogens_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary
```
