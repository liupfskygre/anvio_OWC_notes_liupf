# Making anvi'o use your own HMM collection

## export bac and arc marker genes from gtdbtk data

##

**issues when hmmpress cat hmm profile
```
I found the answer elsewhere. To solve this issue you need to convert the different versions of the individual hmms to the most recent version using hmmconvert.

hmmconvert <old_hmm>  >  <new_hmm_name.hmm>
Then you can concatenate and press the database.

for i in `ls *hmm | sed 's/.hmm//g'`; do hmmconvert ${i}.hmm > ${i}_new.hmm;done
cat *_new.hmm >> database.hmm
hmmpress database.hmm

#all this works well in linux but not macOS

```

```
[liupf@zenith ORG-Data]$ cd /opt/gtdbtk/data/
cd release89
```

```
#1
cd /Users/pengfeiliu/anvio_dataset/gtdbtk_marker/pfam/individual_hmms
#2
cd /Users/pengfeiliu/anvio_dataset/gtdbtk_marker/tigrfam/individual_hmms

#for 1 and 2, run command below
for file in $(cat /Users/pengfeiliu/anvio_dataset/gtdbtk_marker/Arc_122_marker_prefix.txt)
do 
cp ${file}.hmm ../../Arc_122_marker
cp ${file}.HMM ../../Arc_122_marker
done

#
for file in $(cat /Users/pengfeiliu/anvio_dataset/gtdbtk_marker/Bac_120_marker_prefix.txt)
do 
cp ${file}.hmm ../../Bac_120_marker
cp ${file}.HMM ../../Bac_120_marker
done


```

```
#If you have already run this once, and now would like to add an HMM profile of your own, that is easy. You can use --hmm-profile-dir parameter to declare where should anvi’o look for it. 
#for Bacteria
anvi-run-hmms -c contigs.db --hmm-profile-dir /Users/pengfeiliu/anvio_dataset/gtdbtk_marker/Bac_120_marker

#for Archaea
anvi-run-hmms -c contigs.db --hmm-profile-dir /Users/pengfeiliu/anvio_dataset/gtdbtk_marker/Arc_122_marker

#how to use this info for refine bins
```

You can use anvi-export-collection to export collection information and import into other profiles. It becomes very handy when you are doing benchmarking between different approaches.

You can use anvi-show-collections-and-bins to see all available collections and bins in an anvi’o profile or pan database.

You can use anvi-script-get-collection-info to see completion and redundancy estimates for all bins in a given anvi’o collection.

#http://merenlab.org/2016/05/21/archaeal-single-copy-genes/
```
cd /Users/pengfeiliu/anvio_dataset/gtdbtk_marker/Bac_120_marker
cd 
#cat all hmm
cat *.hmm> genes_profile

#gz the concatenate files
gzip genes_profile
mv genes_profile.gz genes.hmm.gz

#add another five files to the marker gene db
touch genes.txt	
touch kind.txt	
touch reference.txt	
touch target.txt

#https://github.com/merenlab/anvio/issues/498#issuecomment-362115921
touch noise_cutoff_terms.txt
#-E 1e-12

#defaultValues.py - store default values used in many places in CheckM; -E 1e-10

#Archaeal
cd /Users/pengfeiliu/anvio_dataset/gtdbtk_marker/Arc_122_marker

#

#
```
http://merenlab.org/2016/04/17/predicting-CPR-Genomes/

```

```
