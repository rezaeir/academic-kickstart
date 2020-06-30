---
title: From Large FASTQ files to Small Count tables using Colab
subtitle: Use Google Colaboratory to preprocess and align your raw NGS data to
  reduce the required amount of local disk space and internet traffic for your
  NGS data analysis project.
date: 2020-06-30T08:45:38.120Z
summary: Use Google Colaboratory to preprocess and align your raw NGS data to
  reduce the required amount of local disk space and internet traffic for your
  NGS data analysis project.
draft: false
featured: false
tags:
  - NGS-data-analysis
  - colab
  - tutorial
  - fastq
image:
  filename: featured.jpg
  focal_point: Smart
  preview_only: false
  caption: Photo by [Alfons
    Morales](https://unsplash.com/@alfonsmc10?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText)
    on
    [Unsplash](/?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText)
  alt_text: a man looking at bioinformatics data
---
## The Problem

One of your colleagues asked you to analyze their RNA-seq data and give them some insight. So, he/she gives you a link in some cloud storage drive, and you should download and analyze it. You don't want to use tens of gigabytes of precious drive space and internet traffic on downloading and storing all these data. Mainly, because you know that after some basic QC and alignment, you're not going to use those large fastq.gz files, and you need to extract the count data from them. There is the possibility of using cloud computing servers, but many of us have neither access nor the money to rent them.

## The solution

Guess what! Google Colaboratory is the free, accessible, easy to use cloud computing platform that you need. Go to their website, prepare the environment, import your data, and do your QC & alignment. If you'd like to know how to do all these steps, read the following tutorial.

## The Tutorial

### Create a colab notebook

Go to the [Colab website](https://colab.research.google.com/) and start a new notebook. Change its name from `Untitled0.ipynb` to whatever you'd like. It will save it automatically to your google drive. You can use `File --> Locate in drive` in case you want to move it to a specific folder. I have a distinct `Colab Notebook` folder, which I use for all my work.

### Prepare the notebook

Before starting the data preprocessing and alignment steps, you need to install some tools. In this case, I'm using FASTQC for quality check, Trimmomatic for trimming reads, Kallisto for alignment, and MultiQC for generating summary files. You can use any tool that you wish. However, installing all these tools from source is hard, and most of these tools aren't accessible through pip, available in colab by default. in my local system, I use conda to install and manage all these packages and a lot more. So, let's install miniconda in colab and use it for installing packages.

### Install conda and fix the issue with python version

```python
! wget https://repo.anaconda.com/miniconda/Miniconda3-py37_4.8.2-Linux-x86_64.sh
! chmod +x Miniconda3-py37_4.8.2-Linux-x86_64.sh
! bash ./Miniconda3-py37_4.8.2-Linux-x86_64.sh -b -f -p /usr/local
import sys
sys.path.append('/usr/local/lib/python3.7/site-packages/')
```

### Install Packages

```python
# FastQC is a program designed to spot potential problems in high throughput sequencing datasets.
!conda install -c bioconda fastqc -y
```

```python
# Multiqc can aggregate and summarize all the QC data and alignment log data in one file
!pip install multiqc
```

```python
# Trimmomatic: A flexible read trimming tool for Illumina NGS data
! conda install -c bioconda trimmomatic -y
```

```python
# Kallisto is a program for quantifying abundances of transcripts from RNA-Seq data, or more generally of target sequences using high-throughput sequencing reads
! conda install -c bioconda kallisto -y
```

### Import the raw data

If your desired data is already in one of the public databases, you have several options. My preferred method is the easiest one, which is to get the download links from [SRA Explorer](https://sra-explorer.info/). Search your desired fastq file, or set of fastq files, using one of the several possible identifiers.

You can get download links in different methods that it presents, but I like the simple `curl` download. So, for example, you can import one dataset like the following code:

```python
# get the link to all files from SRA Explorer
!curl -L ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRRXXX/006/SRR8668XXX/SRR8668XXX.fastq.gz -o SRR8668XXX\_GSM3639XXX\_skin\_HS2\_Homo\_sapiens\_RNA-Seq.fastq.gz
```

### Preprocessing and Alignment

Go through your usual process of Quality assessment, trimming, and alignment. You can use FASTQC, MultiQC, Trimmomatic, and Kallisto, or you can install any other tools using conda and use them. Something like the following code chunk.

```python
# Pre-alignment QA
!fastqc \*.fastq.gz
```

```python
# Trimming
!trimmomatic PE -phred33 41\_R1.fastq 41\_R2.fastq 41\_R1\_paired.fq.gz 41\_R1\_unpaired.fq.gz 41\_R2\_paired.fq.gz 41\_R2\_unpaired.fq.gz ILLUMINACLIP:contams\_forward\_rev.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36
```

```python
# Pre-alignment Multiqc summary file
!multiqc .
```

```python
## alignment
!kallisto quant -i index -o output pairA\_1.fastq pairA\_2.fastq
```

### Zip and download the result files

You can't download folders, so you need to zip them first and then download the result files

```python
# create a zip file from multiqc folder and download it to your local drive
!zip -r ./<zipFileName>.zip <directoryPath>
```

### The rest

Just import the count data in your local drive and continue doing your analysis. I hope you discover something valuable!

### Note

The currently accessible storage in the CPU mode of colab is around 100 GB. *If your raw data is more than 60gb, it is better to load the data in batches, go through the QC/TRIM/ALIGN process, delete the batch raw file, and proceed with the next batch*.

### *Ask me or Help me learn more*

If you have a question, don't hesitate to ask me. If you have a comment or feedback, I'll be happy to know more. I'm also a student like you with little experience, so I'll be grateful if you teach me something. Have fun analyzing your data :)