# checkM also have the workflow to identify bins outliers in bins

# 
```
usage: checkm outliers [-h] [-d dist_value] [-r {any,all}] [-x EXTENSION] [-q]
                       out_folder bin_folder tetra_profile output_file

Identify outliers in bins relative to reference distributions.

positional arguments:
  out_folder            folder specified during qa command
  bin_folder            folder containing bins (fasta format)
  tetra_profile         tetranucleotide profiles for each sequence (see tetra command)
  output_file           print results to file

optional arguments:
  -h, --help            show this help message and exit
  -d, --distributions dist_value
                        reference distribution used to identify outliers; integer between 0 and 100 (default: 95)
  -r, --report_type {any,all}
                        report sequences that are outliers in 'all' or 'any' reference distribution (default: any)
  -x, --extension EXTENSION
                        extension of bins (other files in folder are ignored) (default: fna)
  -q, --quiet           suppress console output

Example: checkm outliers ./output ./bins tetra.tsv outliers.tsv
```

O3D3D3_DDIG_megahit_461_anvioRefine

```
checkm tetra -t 2 O3D3D3_DDIG_megahit_461_1-contigs.fa O3D3D3_DDIG_megahit_461_1-contigs.tsv

checkm outliers ./O3D3D3_DDIG_megahit_461_anvioRefine ./ -x fa O3D3D3_DDIG_megahit_461_1-contigs.tsv O3D3D3_DDIG_megahit_461_1_outliers.tsv

#outliers were stored in O3D3D3_DDIG_megahit_461_1_outliers.tsv; based on TNF and GC, 95%

```
