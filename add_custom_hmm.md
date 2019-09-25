## export bac and arc marker genes from gtdbtk data

##
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
