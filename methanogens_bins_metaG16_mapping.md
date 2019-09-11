



**mapping 16 metaG to all dRep methanogens mags**

#11-Sept-2019

```

cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_Methanogens_MAGs248_db28June2019/dRep_methanogens_28June2019/dereplicated_genomes

screen -r liu_mapping

for MAGs in $(cat dRep_methanogens_prefix.txt)
do 
echo ${MAGs}
for file in $(cat /home/projects/Wetlands/2018_sampling/OWC_metaG_megahit/OWC_metaG16_link_list.txt)
do
echo ${file}
bbmap.sh ref=${MAGs}.fa in=/home/projects/Wetlands/2018_sampling/OWC_metaG_megahit/${file}.fq.gz xmtag=t ambiguous=random outm=${MAGs}_${file}.bam threads=6 -Xmx50g &> ${MAGs}_${file}.log
echo "1"
samtools sort -@ 6 ${MAGs}_${file}.bam > ${MAGs}_${file}.sorted.bam
rm ${MAGs}_${file}.bam
done
done

```
