## 124_Metabat_MUD_2014_2015_coassembly

#copy sorted bam from zenith to MAC

#on MAC

```
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/anvio_refine_MAGs

conda activate anvio5
#creat
sed -i -e 's/124_Metabat_MUD_2014_2015_coassembly\.fascaffold/Metabat_MUD_2014_2015_coassembly124_fascaffold/g' 124_Metabat_MUD_2014_2015_coassembly.fa

#fix the header of bam file
#http://seqanswers.com/forums/showthread.php?t=22504
for sample in $(cat sorted_bam.txt); do samtools view -h $sample|sed -e 's/124_Metabat_MUD_2014_2015_coassembly\.fascaffold/Metabat_MUD_2014_2015_coassembly124_fascaffold/g'|samtools view -bS - > "${sample%.*}"_fixed.bam; done
#this work to fix the header
Metabat_MUD_2014_2015_coassembly124_fascaffold_881

anvi-gen-contigs-database -f 124_Metabat_MUD_2014_2015_coassembly.fa -n 'Metabat_MUD_2014_2015_coassembly124'

#run hmm
anvi-run-hmms -c contigs.db

#display contigs stats
anvi-display-contigs-stats contigs.db

# Profiling BAM files 
#init sorted bam file to generate bai

#
ls -1 *sorted_fixed.bam > sorted_bam.txt
for sample in $(cat sorted_bam.txt); do anvi-init-bam $sample -o "${sample%.*}"_index.bam; done

#profile: --blank-profile, in case we do not have bam file but just want to view the genome
#profile

$ 
for bam in *sorted_fixed_index.bam
do 
anvi-profile -c contigs.db -i $bam  -o ./"${bam%.*}" -T 2 
done

#--cluster-contigs
#-W

#
#merge profle.db

anvi-merge */PROFILE.db -o Metabat_MUD_2014_2015_coassembly124_merged -c contigs.db --sample-name Metabat_MUD_2014_2015_coassembly124_merged

#if we do not want to have CONCOCT binning, use --skip-concoct-binning
#
#generate and import collections from outside

grep '>' 124_Metabat_MUD_2014_2015_coassembly.fa > 124_Metabat_MUD_2014_2015_coassembly.txt
sed -i -e 's/>//g' 124_Metabat_MUD_2014_2015_coassembly.txt
sed -i -e 's/$/\t124_Metabat_MUD_2014_2015_coassembly/g' 124_Metabat_MUD_2014_2015_coassembly.txt
sed -i -e 's/124_Metabat_MUD_2014_2015_coassembly/Metabat_MUD_2014_2015_coassembly124/g' 124_Metabat_MUD_2014_2015_coassembly.txt

#import collection from outside
anvi-import-collection -C Metabat_MUD_2014_2015_coassembly124_collection -p Metabat_MUD_2014_2015_coassembly124_merged/PROFILE.db -c contigs.db 124_Metabat_MUD_2014_2015_coassembly.txt --contigs-mode

#bin names started with number cause problems
#activae view

#without collection
anvi-interactive -p Metabat_MUD_2014_2015_coassembly124_merged/PROFILE.db -c contigs.db 

#with concoct collection
anvi-interactive -p Metabat_MUD_2014_2015_coassembly124_merged/PROFILE.db -c contigs.db -C CONCOCT
anvi-interactive -p Metabat_MUD_2014_2015_coassembly124_merged/PROFILE.db -c contigs.db -C Metabat_MUD_2014_2015_coassembly124_collection
#

#summarize bins

anvi-summarize -p Metabat_MUD_2014_2015_coassembly124_merged/PROFILE.db -c contigs.db -C CONCOCT
anvi-summarize -p Metabat_MUD_2014_2015_coassembly124_merged/PROFILE.db -c contigs.db -C Metabat_MUD_2014_2015_coassembly124_collection

#use the refine

anvi-refine -p Metabat_MUD_2014_2015_coassembly124_merged/PROFILE.db -c contigs.db -C Metabat_MUD_2014_2015_coassembly124_collection -b Metabat_MUD_2014_2015_coassembly124

#anvi-summarize -p Metabat_MUD_2014_2015_coassembly124_merged/PROFILE.db -c contigs.db -C Metabat_MUD_2014_2015_coassembly124_collection -o Metabat2_summary_refined

anvi-summarize -p Metabat_MUD_2014_2015_coassembly124_merged/PROFILE.db -c contigs.db -C Metabat_MUD_2014_2015_coassembly124_collection -o Metabat2_summary_refined2
#in the bin-to-bin folder will find the new 


>>>
#
#after anvio refine, check on zenith
#copy the data to zenith for checkM
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_bins_refine_anvio

# cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_bins_refine_anvio


/home/projects/Wetlands/2018_sampling/scripts/run_checkm_t2.sh Metabat_MUD_2014_2015_coassembly124_1 fa ./ ./Metabat_MUD_2014_2015_coassembly124_1

#gtdbtk
/home/projects/Wetlands/2018_sampling/scripts/run_gtdbtk_t2.sh O3D3D3_DDIG_megahit_461
Using GTDB-Tk reference data version r89: /opt/gtdbtk/data/release89/

#merge
