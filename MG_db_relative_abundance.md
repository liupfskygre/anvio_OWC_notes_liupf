## Calculate the relative abundance of dRep methangoens MAGs in metaG database

##
creat reference db.fa for mapping
```
/home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/Methanogens_cleanDB_26Spet2019_dRep/dereplicated_genomes

#88 genomes from clean and deRep pipeline
#

#addd genome names to the seq_header
for file in *fa
do 
#awk -v str="${file%.*}" '/^>/{print str $0; next}{print}' "$file" >"${file%.*}"_rename.fasta
# not working
var=${file}
echo $var
sed -e "s/>\(.*\)/>"$var"_\1/g" $file >"${file%.*}"_rename.fasta
done
#
cat *_rename.fasta >OWC_methanogens_DB88_cat.fa

#transfer data to summit for mapping
```

#add O3C3D3_DDIG_MN_Anvio.967.fa
```


```


## mapping metaG 16 to methanogens db on summit
```
#sickle on metaG reads
https://github.com/liupfskygre/OWC_metaG16_ana2019/blob/master/megahit1.2.2_full.md

cd /scratch/summit/liupf@colostate.edu
cd raw_metaG_reads

#
ls -1 -d */ >sample_name.txt #remove 

# put the following into slurm scripts

cd /projects/liupf@colostate.edu/workspace

>>>>
#sickle_summit.sh

cd ${rawread_loc}/${sample_name}/Raw_Data

zcat ${rawread_loc}/${sample_name}/Raw_Data/${sample_name}.fastq.gz > ${rawread_loc}/${sample_name}/Raw_Data/tmp_reads.fastq

sickle pe -c ${rawread_loc}/${sample_name}/Raw_Data/tmp_reads.fastq  -t sanger -m ${rawread_loc}/${sample_name}/Raw_Data/${sample_name}_interleaved_trimmed.fastq  -s ${rawread_loc}/sample_name/Raw_Data/${sample_name}_trimmed.singles.fastq

rm ${rawread_loc}/${sample_name}/Raw_Data/tmp_reads.fastq

cd ${rawread_loc}

#done


#sickle_summit.sh sample_name 
>>>

cd /scratch/summit/liupf@colostate.edu
#run slurm
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_M1_C1_D1

#
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_M1_C1_D2
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_M1_C1_D3
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_M1_C1_D4
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_M1_C1_D5
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_M2_C1_D1
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_M2_C1_D5
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_N3_C1_D1
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_N3_C1_D5
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_OW2_C1_D1
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_OW2_C1_D5
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_T1_C1_D1
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_Aug_T1_C1_D5
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_May_M1_C1_D1
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_May_M1_C1_D3
sbatch /projects/liupf@colostate.edu/workspace/sickle_summit.sh OWC_May_M1_C1_D6

squeue|grep liupf

```

## mapping of trimmed reads to ref
```
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_M1_C1_D1

sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_M1_C1_D2
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_M1_C1_D3
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_M1_C1_D4
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_M1_C1_D5
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_M2_C1_D1
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_M2_C1_D5
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_N3_C1_D1
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_N3_C1_D5
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_OW2_C1_D1
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_OW2_C1_D5
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_T1_C1_D1
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_Aug_T1_C1_D5
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_May_M1_C1_D1
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_May_M1_C1_D3
sbatch /projects/liupf@colostate.edu/workspace/run_bbmap_summit_MetaG16_Methanogens_db.sh OWC_May_M1_C1_D6
```

## transfer sam file, summarize and relative abundance calculation
```
#zenith 
/home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db

rm *.fa  #del the 99 genomes

mv OWC_methanogens_DB88_cat.fna ../../ # move concatnated genomes to here

#transfer from summit of sam file to here
for folder in $(cat sample_name.txt)
do 
cd ${folder}/Raw_Data
mv *.sam ../../
cd ../../
done

mv *.sam OWC_methagnoens_db88_ReAb

cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/OWC_methagnoens_db88_ReAb

# https://github.com/liupfskygre/OWC_metaG16_ana2019/blob/master/metaG%20to%20mcrA%20gene%20mapping.md

for file in *.sam
do
samtools view -S -b ${file} > "${file%.*}".bam
samtools sort -@ 8 "${file%.*}".bam > "${file%.*}".sorted.bam
done

#
screen -S MGdb_megahit_metaG16_depth
jgi_summarize_bam_contig_depths --outputDepth MGdb88_megahit_metaG16_depth.txt *.sorted.bam

#use cut and R extract data we need

```

## calculate relative abundance 
```
cat MGdb88_megahit_metaG16_depth.txt |cut -f1-4,6,8,10,12,14,16,18,20,22,24,26,28,30,32,34 -d$'\t' > MGdb88_megahit_metaG16_depth_cut.txt
sed -i -e 's/\.sorted\.bam//g' MGdb88_megahit_metaG16_depth_cut.txt 
sed -i -e 's/_MGdb88//g' MGdb88_megahit_metaG16_depth_cut.txt 
sed -i -e 's/contigName/MAGsName\.fa_contigName/g' MGdb88_megahit_metaG16_depth_cut.txt 
sed -i -e 's/\.fa_/\t/g' MGdb88_megahit_metaG16_depth_cut.txt 
#transfer data to MAc, using R to do cal

```



