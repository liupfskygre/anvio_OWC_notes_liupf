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

**example test**

O3D3D3_DDIG_megahit.461.fa

#381 total contigs
#

anvio test remove to 266, 

```
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_Methanogens_MAGs248_db28June2019/dRep_methanogens_28June2019/dereplicated_genomes

refinem scaffold_stats -c 2 <scaffold_file> <bin_dir> <stats_output_dir> <bam_files>
#index all sorted bam file 
for file in *_O3D3D3_DDIG_megahit.461_sorted.bam
do
samtools index $file
done

#
refinem scaffold_stats -c 2 -x fa O3D3D3_DDIG_megahit.461.fa ./ O3D3D3_DDIG_megahit.461_stats_output *_O3D3D3_DDIG_megahit.461_sorted.bam

#cov not used
refinem outliers ./O3D3D3_DDIG_megahit.461_stats_output/scaffold_stats.tsv O3D3D3_DDIG_megahit.461_outlier_output_no_cov
#76

#test a proper cov_corr, not too stringent, 

##in addition, use the cov_correlation, 0.8
refinem outliers ./O3D3D3_DDIG_megahit.461_stats_output/scaffold_stats.tsv O3D3D3_DDIG_megahit.461_outlier_output --cov_corr 0.8
#115, the number is close to anvio test; 

##in addition, use the cov_correlation, 0.6
refinem outliers ./O3D3D3_DDIG_megahit.461_stats_output/scaffold_stats.tsv O3D3D3_DDIG_megahit.461_outlier_output_cov6 --cov_corr 0.6

#101 outliers
```

```
#use remove the contaminated 
cd O3D3D3_DDIG_megahit.461_outlier_output
>refinem filter_bins -x fa ./ ./outliers.tsv refineM_filter_out
#
O3D3D3_DDIG_megahit.461.filtered.fa
cd refineM_filter_out
/home/projects/Wetlands/2018_sampling/scripts/run_checkm_t2.sh O3D3D3_DDIG_megahit_461 fa ./ ./O3D3D3_DDIG_megahit_461_refineM
# worse than the anvio results, we have  40.97cp/ 11.21ct

#gtdbtk
/home/projects/Wetlands/2018_sampling/scripts/run_gtdbtk_t2.sh O3D3D3_DDIG_megahit_461
Using GTDB-Tk reference data version r89: /opt/gtdbtk/data/release89/

```


### Removing contamination based on taxonomic assignments workflow
**based on taxonomy **
https://github.com/dparks1134/RefineM#reference-database-and-taxonomy-files
https://data.ace.uq.edu.au/public/misc_downloads/refinem/

#download the database to server, use refine

```
/home/liupf/database_downloaded/
#building db
tar -xzf gtdb_r86_protein_db.2018-09-25.tar.gz
screen -S builddb
> diamond makedb -p 2 -d gtdb_r86_protein_db.2018-09-25.faa --in gtdb_r86_protein_db.2018-09-25.faa

#this is for blast db, not used
#makeblastdb -dbtype prot -in gtdb_r86_protein_db.2018-09-25.faa -out gtdb_r86_protein_db.2018-09-25

#analysis data
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/OWC_Methanogens_MAGs248_db28June2019/dRep_methanogens_28June2019/dereplicated_genomes

mkdir O3D3D3_DDIG_megahit.461_gene
>refinem call_genes -c 2 O3D3D3_DDIG_megahit.461_gene O3D3D3_DDIG_megahit.461_gene_output -x fa

screen -S refineM
>refinem taxon_profile -c 1 O3D3D3_DDIG_megahit.461_gene_output O3D3D3_DDIG_megahit.461_stats_output/scaffold_stats.tsv /home/liupf/database_downloaded/gtdb_r86_protein_db.2018-09-25.faa.dmnd /home/liupf/database_downloaded/gtdb_r86_taxonomy.2018-09-25.tsv O3D3D3_DDIG_megahit.461_taxon_profile

refinem taxon_filter -c 2 O3D3D3_DDIG_megahit.461_taxon_profile ./O3D3D3_DDIG_megahit.461_taxon_profile/taxon_filter.tsv

cd O3D3D3_DDIG_megahit.461_gene
>refinem filter_bins -x fa ./ ../O3D3D3_DDIG_megahit.461_taxon_profile/taxon_filter.tsv filtered_output_dir
##after checkM, the now scaffolds were removed

##check the bin report , do manually remove of bins from MAGs based on 'bacteria'
$ sed -i 's/\(k121_[0-9].*\)_[0-9]*$/\1/g' O3D3D3_DDIG_megahit.461_genes.gene_bacteria_f1.tsv>O3D3D3_DDIG_megahit.461_genes.gene_bacteria_f1.txt

$ cat O3D3D3_DDIG_megahit.461_genes.gene_bacteria_f1.tsv|sort|uniq> O3D3D3_DDIG_megahit.461_genes.gene_bacteria_f1.txt

$ cp ../O3D3D3_DDIG_megahit.461_taxon_profile/bin_reports/O3D3D3_DDIG_megahit.461_genes.gene_bacteria_f1.txt ./

pullseq -i O3D3D3_DDIG_megahit.461.fa -e -n O3D3D3_DDIG_megahit.461_genes.gene_bacteria_f1.txt >O3D3D3_DDIG_megahit.461_genes.tax_man.fa 

#checkm aganin on the taxon divergent remove bins
/home/projects/Wetlands/2018_sampling/scripts/run_checkm_t2.sh O3D3D3_DDIG_megahit_461 fa ./ ./O3D3D3_DDIG_megahit_461_refineM

48.19           19.63 , after doing this, the quality is not improved 
```
