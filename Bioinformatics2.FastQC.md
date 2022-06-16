# Bioinformatics II.  "Fastq reads. Evaluating quality"

UpdatedAugust 2021


###### tags: `MAE`, `fastq-dump`, `fastqc`, 
[TOC]

## Getting your terminal ready

Navigate to the folder where you will run your analysis. 
Hint, you will need to use `cd` `ls` `pwd`

here is the Unix tutorial of this course. 
https://jbpc.mbl.edu/unix-tutorial/MAE2020.html

if you have *any doubt* about UNIX most probably is already solved in the tutorial, but we are happy to help


**are you running in a screened session?**

**summary for screen**
Screen
---

check here: [screen instructions](https://hackmd.io/Y3AabwWoTpObumF4eYb37g?view#screen)

navigate to the folder where you will run your analysis

1. to give a name to a screen session `screen -S sessionID`
2. List screens? `screen -r`
3. to connect to screen session `screen -r sessionID`
4. generate a file to log in specific parts of the session
Once in a screened session type `crt+a` release and press `:` a line of text will appear on the botton of the terminal Type `logfile NAMEforlog.txt` press enter (twice).  If you want to log something, press `crt+a` followed by `h`  in the botton of the terminal a line saying creating file NAMEforlog.txt will appear, press enter all you type now will be recorded. To stop recording type again `crt+a` followed by `h`. Recording will stop. **Supercool!** if you use `crt+a` followed by `h` it will append (instead of overwrite!) to the log file. To stop, once again  `crt+a` followed by `h`
4. close screen `crt+a` release and press `d`
5. kill screen `crt+a` release and press `k`
6. finished? type `exit`


## Types of sequence files

and how they look in a terminal?

![](https://i.imgur.com/Y1Adigy.png)

and inside?

lets use `head`

![](https://i.imgur.com/ZPm3XA1.png)


Still not telling you much? let's go one by one.


## File formats

We are using Illumina sequencing technology. 
Illumina sequencing steps
https://www.illumina.com/documents/products/techspotlights/techspotlight_sequencing.pdf

Once your data is ready, it will be provided to you as some special format of text files (fastq). These files are huge, containing millions of reads, and are not designed for human reading.
Here, we will briefly cover some aspects of how to first interact with these files.


### FastQ files
FASTQ is a text file format (human readable) that provides 4 lines of data per sequence.
> Sequence identifier
> The sequence
> Comments
> Quality scores

The results of sequencing will be provided to you as fastq files. 
We are using paired-end sequencing, so we are getting 2 files per sample, one with the Forward read (read 1, R1) and other with the Reverse read (read 2, R2). You can learn more about it [here](https://www.youtube.com/watch?v=fCd6B5HRaZ8). 
    
In the case of paired-end reads, sequencing results may be stored either in one FASTQ file (alternating R1 and R2) or in two different FASTQ files (one containing the R1 and another the R2. 
AS in the case below, paired-end reads may have sequence identifiers ended by "/1" and "/2" respectively.

Example FASTQ entry for one Illumina read:

:::info
@EAS20_8_6_1_3_1914/1 -> identifier
CGCGTAACAAAAGTGTCTATAATCACGGCAGAAAAGTCCACATTGATTATTTGCACGGCGTCACAC
TTTGCTATGCCATAGCATTTTTATCCATAAGATT ->sequence

.+ -> comments
HHHHHHHHHFHGGHHHHHHHHHHHHHHHHHHHHEHHHHHHHHHHHHHHGHHHGHHHGHIH
HHHHHHHHHHHHHHGCHHHHFHHHHHHHGGGCFHBFBCCF ->quality
:::

Generally a FASTQ file is stored in files with the suffix .fq or .fastq 

We use compressing programs such as Gzip to reduce the file size. Compression is indicated by the suffix .gz or .gzip.

```
gzip file.fastq

```
decompress 

```
gzip -d file.fastq.gz

```

### Fasta files

FASTA it is a text file format in which is sequence is characterized by two lines, 

> one the identifier starting with >, 
> the other the sequence itself. 

As no data on read quality is included, the size of the file is considerable smaller than that of a fastq.

:::info

>EAS20_8_6_1_3_1914_1 -> identifier
CGCGTAACAAAAGTGTCTATAATCACGGCAGAAAAGTCCACATTGATTATTTGCACGGCGTCACAC
TTTGCTATGCCATAGCATTTTTATCCATAAGATT -> sequence
:::


## Getting data from NCBI short read archive (SRA)

**In this example we are dowloading are amplicon from NCBI.**


1. **Go to NCBI https://www.ncbi.nlm.nih.gov/ and select SRA in the database menu. Also, you can search in the project database.**

2. **You can search samples of interest by description, e.g. human microbiome or by usinga  SRA sample number (usually these number will appear in the papers as data are usually required to be deposit in a public database prior publication)**

3. example. Search in the search bar for 'salt marsh amplicon'. Select sample of interest, e.g. 16SRNA-gene-saltmarshsediment

![](https://i.imgur.com/61LRPrN.png)

![](https://i.imgur.com/mFp1KeV.png)

    a. What is this sample from?
    b. What sequencing technology was used?
    c. When was it published?
    d. Does it belong to a bigger study?

4. **Open the Project accession in a separate tab.**

![](https://i.imgur.com/Dgr2pAO.png)

5. **Click on the SRA experiments link** (the number 53). A new tab will open. You can now send the results to the **run selector** (link in center top). This will provide you access to each sample within the project and also to the metadata of the experiment.
Download the metadata and accession list files. these are text files, separated by commas. You can import the files into excel (search into how to import data, key words for office Data import, text, tabulated commas). to avoid confussion add the project name to the file name

e.g. 

* SRR_Acc_List_PRJNA610907.txt
* SraRunTable_PRJNA610907.txt



![](https://i.imgur.com/JULPIaU.png)


6. **Click in run SRR11277344**. You will navigate to a new menu with lots of info about the sample.

However, you cannot process or analyze the full scope of the information contained in this file just by looking at it. To really analyze this data set, you will need to download it to your computer.

### Downloading data from NCBI

We are going to be downloading the data from the project PRJNA610907

[Documentation from NCBI](https://ncbi.github.io/sra-tools/fastq-dump.html)
On the terminal create a folder for this analysis

```
mkdir saltmarsh
cd saltmarsh
```

make folder for the raw data

```
mkdir SRAdump_PRJNA610907
```
this will create a folder for you to download your data.
```
cd SRAdump_PRJNA610907
```
navigate to the folder.
we will use fastq-dump to download the data.

We have already check the data characteristics. 

This is very important because we need to know how to process them afterwars. This is a set of samples sequenced using [paired-end reads](https://www.illumina.com/science/technology/next-generation-sequencing/plan-experiments/paired-end-vs-single-read.html)
so we want to separate each read in a separate file 1/ and 2/. To do so, we will use the split files flag. we will also skip any technical reads that might be present)

[SRR11277344](https://trace.ncbi.nlm.nih.gov/Traces/sra/?run=SRR11277344)


### Prefetch


We will download files from NCBI using `prefetch` so we will get the data in compressed .sra format. Then we will use `fastq-dump` to uncompress the files (note, fastq-dump can also be used to download files)

http://www.metagenomics.wiki/tools/short-read/ncbi-sra-file-format/prefetch 

https://edwards.sdsu.edu/research/fastq-dump/

https://ncbi.github.io/sra-tools/fastq-dump.html 



check that you are in the right directory using `pwd`

~/saltmarsh/SRAdump_PRJNA610907

Now, let's download some files!
Type
```
prefetch -f yes SRR11277344
```
Use `ls` to check if the file is present. 

```
vdb-validate ~/saltmarsh/SRAdump_PRJNA610907/SRR11277344/SRR11277344.sra


```
You can use `**vdb-validate**` for checking the download
[documentation from NCBI](https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=toolkit_doc&f=vdb-validate)

:::success
#[MAE2019 eperedo@class-02 SRR11277344$] vdb-validate ~/saltmarsh/SRAdump_PRJNA610907/SRR11277344/SRR11277344.sra

2020-10-08T16:45:43 vdb-validate.2.10.0 info: Database 'SRR11277344.sra' metadata: md5 ok

2020-10-08T16:45:43 vdb-validate.2.10.0 info: Table 'SEQUENCE' metadata: md5 ok

2020-10-08T16:45:43 vdb-validate.2.10.0 info: Column 'QUALITY': checksums ok

2020-10-08T16:45:43 vdb-validate.2.10.0 info: Column 'READ': checksums ok

2020-10-08T16:45:43 vdb-validate.2.10.0 info: Column 'READ_LEN': checksums ok

2020-10-08T16:45:43 vdb-validate.2.10.0 info: Column 'READ_START': checksums ok

2020-10-08T16:45:43 vdb-validate.2.10.0 info: Database '/users/eperedo/saltmarsh/SRAdump_PRJNA610907/SRR11277344/SRR11277344.sra' contains only unaligned reads

2020-10-08T16:45:43 vdb-validate.2.10.0 info: Database 'SRR11277344.sra' is consistent

:::

```
fastq-dump  \
    -W -\
    -split-files \
    --read-filter pass \
    --gzip \
    --skip-technical \
    ~/saltmarsh/SRAdump_PRJNA610907/SRR11277344/SRR11277344.sra
```
in `fastq-dump`

* The flag -W will remove adapters, if present. 
* --split-files will separate R1 and R2
* --gzip will compress the files 
* --read-filter pass remove low quality data
* --skip-technical remvoe technical reads, if present. 

:::info
Read 61166 spots for /users/eperedo/saltmarsh/SRAdump_PRJNA610907/SRR11277344/SRR11277344.sra
Written 61166 spots for /users/eperedo/saltmarsh/SRAdump_PRJNA610907/SRR11277344/SRR11277344.sra

:::



If you do `ls` now, you should see two files.

SRR11277344_pass_1.fastq.gz  SRR11277344_pass_2.fastq.gz



## Quality control

### fastqc

Now let’s have a look to the quality of the reads. We will be using `fastqc`, first have a look to the options of the program using the help type `fastqc -h`. Then, have a look to the data in the read 1 & 2.
```
fastqc SRR11277344_pass_1.fastq.gz SRR11277344_pass_2.fastq.gz 
```

List the files to check that all run properly `ls` and you can use filezilla to transfer the report file .html to your computer. 

Open the .html (using your web browser) and have a look to the report.

![](https://i.imgur.com/wAMKkIu.png)
 
The grey box details the basic info e.g. number of reads in the file, length.
On the left you have a series of links to navigate different stats. 

#### Quality score graph. 

In the graph it is represented the quality (y, phred score) per base (x). Good quality data stays in the green. (As we selected reads that pass the quality filter it is expected they will be all gree, but still it is important to check)

**Quality and phred score**
Phred quality scores **Q** are defined as a property which is logarithmically related to the base-calling error probabilities **P**.

![](https://i.imgur.com/EJSOZ7R.png)

https://learn.gencore.bio.nyu.edu/ngs-file-formats/quality-scores/ 




No sequence has been flagged as bad quality for this file. If that was the case, we can use programs such as trimmomatic to remove low quality reads from our data sets.

Why do you think the per base sequence content has been flagged?

more info: https://rtsf.natsci.msu.edu/genomics/tech-notes/fastqc-tutorial-and-faq/
 
 lets check read 2. what you see?
 



## LOOPS
Of course, if you were analyzing a relatively long set of samples, you would not be doing this one by one!

To avoid having to do this one by one we will create a **for loop**. [more here](https://www.tutorialspoint.com/unix/unix-shell-loops.htm)
All we need is a text file containing the list of files you want to process. Here we will cover an example, using the same dataset as before. In the terminal, get out of the current folder and make a new one.

do you remember the file SRR_Acc_List_PRJNA610907.txt you downloaded?
copy it to the folder. (you can fdrag and drop using filezilla or youcan create a file using the terminal)We will start at 9. 

```
cat > SRR_Acc_List_PRJNA610907.txt
```
this creates the file, let's populate it. We will only use 29 samples of this dataset (the ones identified as PCR in the metadata file)

Enter your document's text. open the txt file in your computer, select all (crt +a) and copy (crt +c) now copy all the text in the terminal **(crt + shift +v)** note: copy and past require crt +shift. 
```
SRR11277348
SRR11277349
SRR11277350
SRR11277352
SRR11277353
SRR11277354
SRR11277355
SRR11277356
SRR11277357
SRR11277358
SRR11277359
SRR11277360
SRR11277361
SRR11277363
SRR11277364
SRR11277365
SRR11277366
SRR11277367
SRR11277368
SRR11277369
SRR11277370
SRR11277371
SRR11277372
SRR11277374
SRR11277375
SRR11277376


```
#Press enter to insert and end line.exit using Ctrl + Z
and check!
```
ls -l SRR_Acc_List_PRJNA610907.txt
head SRR_Acc_List_PRJNA610907.txt

```

### Loop it!

Example with fastq-dump

now let's run all the commands we just used in loop.

check that you are in the right directory
~/saltmarsh/SRAdump_PRJNA610907/

```
for line in `cat SRR_Acc_List_PRJNA610907.txt`; \
    do prefetch -f yes ${file}; \
    done

```
```
for line in `cat SRR_Acc_List_PRJNA610907.txt`; \
    do vdb-validate ~/saltmarsh/SRAdump_PRJNA610907/${file}/${file}.sra; \
    done
```

could you write the rest?

Or check below for the loop for each of the four steps. 



```
#download
for line in `cat SRR_Acc_List_PRJNA610907.txt`; \
    do prefetch -f yes ${file}; \
    done

#validate
for line in `cat SRR_Acc_List_PRJNA610907.txt`; \
    do vdb-validate ~/saltmarsh/SRAdump_PRJNA610907/${file}/${file}.sra; \
    done

#uncompress
for line in `cat SRR_Acc_List_PRJNA610907.txt`; \
    do fastq-dump \
    --split-files \
    --read-filter pass \
    --gzip \
    --skip-technical \
    ~/saltmarsh/SRAdump_PRJNA610907/${file}/${file}.sra; \
    done

#check quality

for line in `cat SRR_Acc_List_PRJNA610907.txt`; \
    do fastqc ${file}_pass_1.fastq.gz ${file}_pass_2.fastq.gz; 
    done

```


