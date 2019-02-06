# Trinity
More detail about trinity here: https://github.com/trinityrnaseq/trinityrnaseq/wiki/Running-Trinity

Reference:
   - Grabherr MG, Haas BJ, Yassour M, Levin JZ, Thompson DA, Amit I, Adiconis X, Fan L, Raychowdhury R, Zeng Q, Chen Z, Mauceli E, Hacohen N, Gnirke A, Rhind N, di Palma F, Birren BW, Nusbaum C, Lindblad-Toh K, Friedman N, Regev A. Full-length transcriptome assembly from RNA-seq data without a reference genome. Nat Biotechnol. 2011 May 15;29(7):644-52. doi: 10.1038/nbt.1883. PubMed PMID: 21572440.
  - Haas BJ, Papanicolaou A, Yassour M, Grabherr M, Blood PD, Bowden J, Couger MB, Eccles D, Li B, Lieber M, Macmanes MD, Ott M, Orvis J, Pochet N, Strozzi F, Weeks N, Westerman R, William T, Dewey CN, Henschel R, Leduc RD, Friedman N, Regev A. De novo transcript sequence reconstruction from RNA-seq using the Trinity platform for reference generation and analysis. Nat Protoc. 2013 Aug;8(8):1494-512. Open Access in PMC doi: 10.1038/nprot.2013.084. Epub 2013 Jul 11. PubMed PMID:23845962.
  - Grabherr MG, Haas BJ, Yassour M, Levin JZ, Thompson DA, Amit I, Adiconis X, Fan L, Raychowdhury R, Zeng Q, Chen Z, Mauceli E, Hacohen N, Gnirke A, Rhind N, di Palma F, Birren BW, Nusbaum C, Lindblad-Toh K, Friedman N, Regev A. Full-length transcriptome assembly from RNA-seq data without a reference genome. Nat Biotechnol. 2011 May 15;29(7):644-52. doi: 10.1038/nbt.1883. PubMed PMID: 21572440.
  - 

Before I start Trinity run, I will like to combine all the R1_paired together and all the R2_paired together by doing:
```
cat *_R1_paired.fastq.gz > XT_R1.fastq.gz
cat *_R2_paired.fastq.gz > XT_R2.fastq.gz
```

## How to run trinity
```bash
time /home/xue/software//home/xue/software/trinityrnaseq-Trinity-v2.5.1/Trinity --seqType fq  --left /home/xue/tropicalis_gonad_transcriptome_Dec2018/trim/XT_R1.fastq.gz --right /home/xue/tropicalis_gonad_transcriptome_Dec2018/trim/XT_R2.fastq.gz --CPU 20 --inchworm_cpu 6 --full_cleanup --max_memory 200G --min_kmer_cov 2 --output /home/xue/tropicalis_gonad_transcriptome_Dec2018/tropicali_gonad_transcriptome_trinityOut
```
Below is the explaination of what we included in the above command:
- --seqType <string>      :type of reads: ('fa' or 'fq')
- --left  <string>    :left reads, one or more file names (separated by commas, no spaces)
- --right <string>    :right reads, one or more file names (separated by commas, no spaces)
- --CPU <int>                     :number of CPUs to use, default: 2
- --inchworm_cpu <int>           :number of CPUs to use for Inchworm, default is min(6, --CPU option); capped at 6, perform wouldn't increase even increase higher than 6
-  --full_cleanup                  :only retain the Trinity fasta file, rename as ${output_dir}.Trinity.fasta
- --max_memory <string>      :suggested max memory to use by Trinity where limiting can be enabled. (jellyfish, sorting, etc) provided in Gb of RAM, ie.  '--max_memory 10G'
- --min_kmer_cov <int>           :min count for K-mers to be assembled by Inchworm (default: 1)
- --output <string>               :name of directory for output (will be created if it doesn't already exist)

How to see the full usage
```
/usr/local/trinity/current/Trinity --show_full_usage_info|less -S
```

# Practice
#### Write your own command base on the one that I ran before
The one that ran successfully on Xue's account
```
/usr/local/trinity/current/Trinity --seqType fq  --left /home/xue/tropicalis_gonad_transcriptome_Dec2018/trim/XT_R1.fastq.gz --right /home/xue/tropicalis_gonad_transcriptome_Dec2018/trim/XT_R2.fastq.gz --CPU 20 --inchworm_cpu 6 --full_cleanup --max_memory 200G --min_kmer_cov 2 --output /home/xue/tropicalis_gonad_transcriptome_Dec2018/tropicali_gonad_transcriptome_trinityOut
```
The one to run on Martin's account. Please put how you think you should run it from your account
```
/usr/local/trinity/current/Trinity --seqType fq  --left /home/martin/tropicalis_gonad_transcriptome/trim/XT_R1.fastq.gz --right /home/martin/tropicalis_gonad_transcriptome/trim/XT_R2.fastq.gz --CPU 20 --inchworm_cpu 6 --full_cleanup --max_memory 100G --min_kmer_cov 2 --output /home/martin/tropicalis_gonad_transcriptome/trinity_output

```



#### command 1 to try - contain error
below might contain error, try to run it and correct it. It should give you an error message when you run it
```
#path to the folder
/home/martin/tropicalis_gonad_transcriptome

#command to run for trinity 

```
below is the corrected command:
```

```
#### command 2 to try - contain error
below command contains error, if you try to run it, it will probably run but there's missing information. Try to identify the error and correct it before you run it.  
```

```

