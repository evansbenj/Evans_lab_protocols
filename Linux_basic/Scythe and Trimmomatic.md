# Scythe
more detail about scythe: https://github.com/vsbuffalo/scythe. 

## how to run Scythe
```
#run scythe for XT10 R1
/home/xue/software/scythe-master/scythe -a /home/xue/software/scythe-master/illumina_adapters.fa -p 0.1 -o /home/xue/tropicalis_gonad_transcriptome_Dec2018/raw_data/XT10_R1_scythe.fastq.gz /home/xue/tropicalis_gonad_transcriptome_Dec2018/raw_data/XT10_R1.fastq.g

#run scythe for XT10 R2
/home/xue/software/scythe-master/scythe -a /home/xue/software/scythe-master/illumina_adapters.fa -p 0.1 -o /home/xue/tropicalis_gonad_transcriptome_Dec2018/raw_data/XT10_R2_scythe.fastq.gz /home/xue/tropicalis_gonad_transcriptome_Dec2018/raw_data/XT10_R2.fastq.gz

/home/xue/software/scythe-master/scythe -a /home/xue/software/scythe-master/illumina_adapters.fa -p 0.1 -o /home/xue/tropicalis_gonad_transcriptome_Dec2018/raw_data/XT11_R1_scythe.fastq.gz /home/xue/tropicalis_gonad_transcriptome_Dec2018/raw_data/XT11_R1.fastq.gz
```
What are the parameters
- -a: adapter file in fasta format
- -p: the prior contamination rate is 0.05; BenF used 0.1.
- -o: output file name

Other options:
- -q: Illumina's quality scheme (pipeline > 1.3) is used. Sanger or Solexa (pipeline < 1.3) qualities can be specified
- -n: one can specify the minimum match length argument with -n <integer> and 
- -M: the minimum length of sequence (discarded less than or equal to this parameter) to keep after trimming with -M <integer>

## how to run Scythe on all the file with one command
```
#way 1: output file name would be like XT10_R1_scythe.fastq.gz

for i in *fastq.gz ; do name=$(grep -o "XT[0-9]*_[A-Z][0-9]" <(echo $i)); /home/xue/software/scythe-master/scythe -a /home/xue/software/scythe-master/illumina_adapters.fa -p 0.1 $i | gzip > /home/xue/tropicalis_gonad_transcriptome_Dec2018/scythed_data/$name\_scythe.fastq.gz; done

#way two: output file name would be like XT10_R1.fastq.gz; you can do this but make sure the output folder is different from the input folder, otherwise the old file will be overwritten 

for i in *fastq.gz; do /home/xue/software/scythe-master/scythe -a /home/xue/software/scythe-master/illumina_adapters.fa -p 0.1 -o /home/xue/tropicalis_gonad_transcriptome_Dec2018/scythed_data/$i $i | gzip > ; done
```

# Trimmomatic 

## Installing trimmomatic

This software is used to trim off bad sequences based on position in the read and quality scores of the nucleotides.  You can get it like this `wget http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip`

Uncompress it like this:
`unzip Trimmomatic-0.36.zip`

path to raw read file: 
```
/home/xue/diploid_tetraploid_transcriptome_QA/Laevis_TranscriptomeData/Sample_BenEvansBJE3909cDNA_Library
```
## what does trimmomatic does
This will perform the following:

- Remove adapters (ILLUMINACLIP:TruSeq3-PE.fa:2:30:10)
- Remove leading low quality or N bases (below quality 3) (LEADING:3)
- Remove trailing low quality or N bases (below quality 3) (TRAILING:3)
- Scan the read with a 4-base wide sliding window, cutting when the average quality per base drops below 15 (SLIDINGWINDOW:4:15)
- Drop reads below the 36 bases long (MINLEN:36)

## Run trimmomatic 
run it like this if it is paired end
learn how to run trimmomatic and what the command means: http://www.usadellab.org/cms/?page=trimmomatic

```
#how Xue ran it on Xue's account
java -jar /home/xue/Trimmomatic-0.36/trimmomatic-0.36.jar PE -phred33 -trimlog trim_out.txt /home/xue/transcriptome_data/Sample_BenEvansBJE3909cDNA_Library/BenEvansBJE3909cDNA_Library_GTGAAA_L004_R1_001.fastq.gz /home/xue/transcriptome_data/Sample_BenEvansBJE3909cDNA_Library/BenEvansBJE3909cDNA_Library_GTGAAA_L004_R2_001.fastq.gz /home/xue/transcriptome_data/BJE3909_tropicalis_trimmed_data/BenEvansBJE3909cDNA_Library_GTGAAA_L004_R1_001_paired.fastq.gz /home/xue/transcriptome_data/BJE3909_tropicalis_trimmed_data/BenEvansBJE3909cDNA_Library_GTGAAA_L004_R1_001_single.fastq.gz /home/xue/transcriptome_data/BJE3909_tropicalis_trimmed_data/BenEvansBJE3909cDNA_Library_GTGAAA_L004_R2_001_paired.fastq.gz /home/xue/transcriptome_data/BJE3909_tropicalis_trimmed_data/BenEvansBJE3909cDNA_Library_GTGAAA_L004_R2_001_single.fastq.gz ILLUMINACLIP:/home/xue/Trimmomatic-0.36/adapters/TruSeq2-PE.fa:2:30:10 SLIDINGWINDOW:4:15 MINLEN:36

#how you can run it on info with the jar in user/local
java -jar /usr/local/trimmomatic/trimmomatic-0.36.jar PE -phred33 -trimlog trim_out.txt /home/martin/tropicalis_gonad_transcriptome/raw_data/XT10_R1.fastq.gz /home/martin/tropicalis_gonad_transcriptome/raw_data/XT10_R2.fastq.gz /home/martin/tropicalis_gonad_transcriptome/test/XT10_R1_paired.fastq.gz /home/martin/tropicalis_gonad_transcriptome/test/XT10_R1_unpaired.fastq.gz /home/martin/tropicalis_gonad_transcriptome/test/XT10_R2_paired.fastq.gz  /home/martin/tropicalis_gonad_transcriptome/test/XT10_R2_unpaired.fastq.gz ILLUMINACLIP:/usr/local/trimmomatic/adapters/TruSeq2-PE.fa:2:30:10 SLIDINGWINDOW:4:15 MINLEN:36

```
What the parameters mean:
- LLUMINACLIP: Cut adapter and other illumina-specific sequences from the read.
- SLIDINGWINDOW: Perform a sliding window trimming, cutting once the average quality within the window falls below a threshold.
- LEADING: Cut bases off the start of a read, if below a threshold quality
- TRAILING: Cut bases off the end of a read, if below a threshold quality
- CROP: Cut the read to a specified length
- HEADCROP: Cut the specified number of bases from the start of the read
- MINLEN: Drop the read if it is below a specified length
- TOPHRED33: Convert quality scores to Phred-33
- TOPHRED64: Convert quality scores to Phred-64


```
ls | wc -l
```
