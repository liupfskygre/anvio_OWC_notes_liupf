## this is a markdown file to log how to use refineM to improve high contamined bins 

#

refinem -h

                ...::: RefineM v0.0.24 :::...

    Scaffold statistics:
     scaffold_stats -> Calculate statistics for scaffolds
     genome_stats   -> Calculate statistics for genomes

    Reduce contamination:
     outliers       -> Identify scaffolds with divergent GC, coverage, or tetranucleotide signatures
     taxon_profile  -> Generate a taxonomic profile from the genes within a genome
     taxon_filter   -> Identify scaffolds with divergent taxonomic classification
     ssu_erroneous  -> Identify scaffolds with erroneous 16S rRNA genes

    Improve completeness:
     reference      -> Identify scaffolds with similarity to specific reference genome(s)
     compatible     -> Identify scaffolds with compatible GC, coverage, and tetranucleotide signatures
     merge          -> [not implemented] Identify partial genomes which should be merged together (requires CheckM)
     
    Cluster:
     kmeans         -> Partition bin with k-means clustering
     dbscan         -> [not implemented] Partition bin with DBSCAN clustering
     split          -> Split bin into exactly two partitions using genomic feature thresholds
     manual         -> Partition bin into clusters based on manual assignment

    Modify genome(s):
     modify_bin     -> Modify scaffolds in a single bin
     filter_bins    -> Remove scaffolds across a set of bins

    Genome validation and exploration:
     unique         -> Ensure scaffolds are assigned to a single genome
     unbinned       -> Identify unbinned scaffolds
     bin_compare    -> Compare two sets of genomes (e.g., from alternative binning methods)
     bin_union      -> [not implemented] Merge multiple binning efforts into a single bin set

    Utility functions:
     call_genes     -> Identify genes within genomes


```
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_Methanogens_MAGs248_db28June2019/dRep_methanogens_28June2019/dereplicated_genomes

refinem scaffold_stats -c 2 <scaffold_file> <bin_dir> <stats_output_dir> <bam_files>

for file in *_O3D3D3_DDIG_megahit.461_sorted.bam
do
samtools index $file
done

refinem scaffold_stats -c 2 -x fa O3D3D3_DDIG_megahit.461.fa ./ O3D3D3_DDIG_megahit.461_stats_output *_O3D3D3_DDIG_megahit.461_sorted.bam

refinem outliers ./O3D3D3_DDIG_megahit.461_stats_output/scaffold_stats.tsv O3D3D3_DDIG_megahit.461_outlier_output --cov_corr 0.8

```
