# Basic - submitting job in Graham and Cedar (Slurm queuing system)
to access the cluster
```bash
ssh username@graham.computecanada.ca
ssh username@cedar.computecanada.ca
```
after you login, you need to go to your folder like this:
```
cd projects/def-ben/songxy/
```
for graham and cedar you need a bash file to start a queue using batch. 
**Submitting and check on job status**
```bash
#submit a job
sbatch script.sh #ex, sbatch bwa.sh

#check on the status of job submitted
squeue -u username #ex, squene -u songxy

# list resources used by completed job
 sacct -j jobID [--format=JobID,MaxRSS,Elapsed] #ex, sacct -j 9990456
 
# to cancel a job
scancel jobID #ex, scancel 10284976
 
```
**Loading and checking modules/softwares**
```bash
module avail <name> # search for a module
module spider <name> # will give info about the module name and its dependcies
module list # show currently loaded modules
module load moduleName
module unload moduleName
module show moduleName # show commands in the module
```
**Example of bash sript for job submission**
```bash
#####The bash file 

#!/bin/sh                                                                                            
#SBATCH --job-name=Bwa_Mem                                                                           
#SBATCH --nodes=1                                                                                    
#SBATCH --ntasks-per-node=32                                                                         
#SBATCH --time=96:00:00                                                                              
#SBATCH --mem=50gb                                                                                   
#SBATCH --output=BwaMem.%J.out                                                                       
#SBATCH --error=BwaMem.%J.err                                                                        
#SBATCH --account=def-ben                                                                            

/home/ben/project/ben/bin/bwa/bwa mem /home/ben/project/ben/MacaM/MacaM_mt_y.fa $1 $2 -t $SLURM_NTAS\
KS_PER_NODE | /home/ben/project/ben/bin/samtools-1.5/samtools view -Shu - | /home/ben/project/ben/bi\
n/samtools-1.5/samtools sort - -o $3

#####To submit the job
sbatch bwa.sh fastq1.fq.gz fastq2.fq.gz bamout.bam
```

Link to useful intro or resource:
- available programs: https://docs.computecanada.ca/wiki/Available_software
- check the cluster status: https://status.computecanada.ca/
- introduction ppt: https://www.westgrid.ca/files/WestGrid-July2017TownHall-CedarDemo.pdf
- more about sbatch: https://slurm.schedmd.com/sbatch.html
