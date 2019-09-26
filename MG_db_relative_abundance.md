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



```
