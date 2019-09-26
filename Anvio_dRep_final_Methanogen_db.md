## after Anvio clean of dRep geneomes and recover genome with CP>50% and Ctl>25%, 

## do dRep on these genomes with de-Replicated and cleaned genomes again

# 
```
copy checkM file of genomes after cleanning
# /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/Methanogens_final_dRep_clean_db

#OWC_methanogens_MAGs_deRep95_checkM_gtdbtk_Anvio.xlsm

--> remove Ct>10, completeness < 50%
OWC_methanogens_MAGs_checkM_gtdbtk_Anvio.txt

#
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db
$ cat OWC_methanogens_MAGs_checkM_gtdbtk_Anvio.txt|cut -f1 -d$'\t' >OWC_methanogens_MAGs_checkM_gtdbtk_Anvio.prefix

# OWC_methanogens_MAGs_checkM_gtdbtk_Anvio.prefix
cp genomes here 

#dRep 95
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_methanogens_db374_20Sept/Methanogens_db_dRep_20Spet2019_dRep2/dereplicated_genomes
#Anvio refine, part I-1
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_bins_refine_anvio/Refine_list_fa
#Anvio refine, part I-2
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_bins_refine_anvio/Refine_list_fa_refine2
#Anvio recovery part II
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methangoens_db_Cp50Ctl25_Anvio/A_refined_fa

for file in $(cat /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/OWC_methanogens_MAGs_checkM_gtdbtk_Anvio.prefix)
do
cp ${file}.fa /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db
done

#99 genomes
```
#rename and clean bins
```
mv 13_Metabat_OPEN_2014_2015_coassembly.fa  OPEN_2014_2015_coassembly_Metabat_13.fa
mv 14_Metabat_MUD_2015_08.fa MUD_2015_08_Metabat_14.fa
mv 21_Metabat_MUD_2014_2015_coassembly.fa MUD_2014_2015_coassembly_Metabat_21.fa
mv 69_Metabat_MUD_2014_2015_coassembly.fa MUD_2014_2015_coassembly_Metabat_69.fa
mv 7_Metabat_MUD_2015_08.fa MUD_2015_08_Metabat_7.fa

#changed the name in OWC_methanogens_MAGs_checkM_gtdbtk_Anvio.txt
cut -f1,6,7 OWC_methanogens_MAGs_checkM_gtdbtk_Anvio.txt > OWC_methanogens_MAGs_checkM_gtdbtk_info.csv

sed -i -e 's/\t/\.fa,/1' OWC_methanogens_MAGs_checkM_gtdbtk_info.csv
sed -i -e 's/\t/,/g' OWC_methanogens_MAGs_checkM_gtdbtk_info.csv
nano  OWC_methanogens_MAGs_checkM_gtdbtk_info.csv
genome,completeness,contamination

dRep dereplicate -p 6 -comp 50 -con 25 --genomeInfo ./OWC_methanogens_MAGs_checkM_gtdbtk_info.csv ./Methanogens_cleanDB_26Spet2019_dRep -g ./*.fa


#get the checkM and gtdbtk
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/Methanogens_cleanDB_26Spet2019_dRep/dereplicated_genomes



/home/projects/Wetlands/2018_sampling/scripts/run_gtdbtk.sh Methanogens_cleanDB_26Spet2019_dRep

/home/projects/Wetlands/2018_sampling/scripts/run_checkm.sh Methanogens_cleanDB_26Spet2019_dRep fa ./ ./Methanogens_cleanDB_26Spet2019_dRep_checkM

#merge
python /home/projects/Wetlands/2018_sampling/scripts/add_gtdbtk_tax_to_checkm.py Methanogens_cleanDB_26Spet2019_dRep_checkm_summary.txt gtdbtk_out/Methanogens_cleanDB_26Spet2019_dRep.bac120.summary.tsv gtdbtk_out/Methanogens_cleanDB_26Spet2019_dRep.ar122.summary.tsv >Methanogens_cleanDB_26Spet2019_dRep_checkm_gtdbtk_summary.txt

#use old ones
sed -i -e 's/\.fa//1' dRep_genome90.list
grep -w -f dRep_genome90.list OWC_methanogens_MAGs_checkM_gtdbtk_Anvio.txt > Methanogens_cleanDB_26Spet2019_dRep_checkM_gtdbtk_old.txt

```

```
remove following based on GTDBtk tax
M3C4D4_idba_metabatSS_Anvio.16_1; Bacterial??
O3C3D3_DDIG_MN_Anvio.967.??
O3D3_metabatSS.Anvio.87??
May_M1_C1_D3_megahit_metabat.45??

```


#clean server,
#clean my MacOS
