# FastQC

## how to run fastqc?
You can make a html file with QC information like this:

```
# do it for one file
fastqc BJE3909_single_R1_and_R2.fq.gz

# do it for all fastq.gz file in the folder
for i in *fastq.gz ; do fastqc $i; done
```

and then download the file to inspect with a browser like this:

```
scp xue@info.mcmaster.ca:/home/xue/transcriptome_data/BJE3909_tropicalis_trimmed_data/BJE3909_single_R1_and_R2_fastqc.html .
```

## How to read fastqc files?
- Video 
https://www.youtube.com/watch?v=bz93ReOv87Y

- Detail explanation on each category
https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/

- Example of good/bad sequence
  - Bad: https://www.bioinformatics.babraham.ac.uk/projects/fastqc/bad_sequence_fastqc.html
  - Good: https://www.bioinformatics.babraham.ac.uk/projects/fastqc/good_sequence_short_fastqc.html#M0
