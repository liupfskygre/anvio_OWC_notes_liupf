## 124_Metabat_MUD_2014_2015_coassembly

#copy sorted bam from zenith to MAC

#on MAC

```
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/anvio_refine_MAGs

conda activate anvio5
#creat
anvi-gen-contigs-database -f 124_Metabat_MUD_2014_2015_coassembly.fa -n '124_Metabat_MUD_2014_2015_coassembly'

#run hmm
anvi-run-hmms -c contigs.db

#display contigs stats
anvi-display-contigs-stats contigs.db

# Profiling BAM files 
#init sorted bam file to generate bai

ls -1 *sorted.bam > sorted_bam.txt
for sample in $(cat sorted_bam.txt); do anvi-init-bam $sample -o "${sample%.*}"_index.bam; done

#profile: --blank-profile, in case we do not have bam file but just want to view the genome
#profile

$ 
for bam in *_index.bam
do 
anvi-profile -c contigs.db -i $bam  -o ./"${bam%.*}" -T 2 
done

#--cluster-contigs
#-W

#
#merge profle.db

anvi-merge */PROFILE.db -o 124_Metabat_MUD_2014_2015_coassembly_merged -c contigs.db --sample-name 124_Metabat_MUD_2014_2015_coassembly_merged  

#if we do not want to have CONCOCT binning, use --skip-concoct-binning

#
#after anvio refine, check on zenith
#copy the data to zenith for checkM
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_bins_refine_anvio
