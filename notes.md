# Notes on Yeast Hybrid Genome Assembly Pipeline 

This file was created by the following command:

```
touch notes.md
```

## PacBio QC using LongQC

First we will go to our directory

```
cd Documents/Yeast-hybrid-genome-assembly/Data/PacBio/
```

We unzip the tar file

```
tar xvf X204SC23033130-Z01-F002_01.tar
```

- x: extract
- v: verbose (you will supervise the process)
- f: specify that is a single file to be unziped (we write the name of the file after this command)

```
cd X204SC23033130-Z01-F002_01/raw_data/M1
```
```
ls
```

Result of ls:

```
1_m64164_230517_123413.subreads.bam
M1_m64164_230517_123413.subreads.bam.pbi
M1_m64164_230517_123413.subreadset.xml
MD5.txt
```

We will use the samtools to check the .bam file: 

We need to install the samtool package: 

```
conda activate perfect_assembly
```
```
conda install bioconda::samtools
```

Let's get a look of our bam file: 

```
samtools view M1_m64164_230517_123413.subreads.bam | head
```

We will create a new directory in the repo:

```
mkdir Results
```

Let's do the LongQC on our bam file:

It is better to set the working directory in the folder of the .bam file and just lead the output in the Results directory.

```
pwd

cd Results

pwd

python /home/labguest/software/LongQC/longQC.py sampleqc -x pb-sequel -o /home/labguest/Documents/Yeast-hybrid-genome-assembly/Results/LongQC_M1 M1_m64164_230517_123413.subreads.bam
```

Inspect the process:

We open a new terminal window and write:

```
htop
```

Now we can inspect the process (e.g. how much of RAM, CPUs etc. are used). 

*In the results of the LongQC, the QV had a value of 0. 

## Illumina short-reads QC 

We will run the **fastp** package to remove adapters, duplicates and low quality bases of the Illumina short-reads:

First, we need to return to our repo and inside the Results folder:

```
cd /home/labguest/Documents/Yeast-hybrid-genome-assembly/Results
```

Now we will create a new folder to save the fastp output for the M1 Illumina reads:

```
mkdir fastp_M1
```

Now we will go to the terminal and move to the directory where the short reads are located. From this directory we will run the fastp package and save the output in the fasp_M1 directory in the Results folder. 

To the terminal we write:

```
cd /home/labguest/Documents/Yeast-hybrid-genome-assembly/Data/Illumina/2
```

Now we will unzip the .tar file:

```
tar xvf X204SC23033130-Z01-F003.tar
```




