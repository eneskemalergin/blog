---
layout: post
title: Data Preparation for one specific Bioinformatics task
tags:
- Python
- Bash
- Bioinformatics
---

Hello folks, in this post I will share how I prepare data for the project that I am currently working on.

Data preparation is always messy and painful, since finding ideal data for your project is almost impossible. For my project it is not the case too. To get the data as input to my deep neural network model, it must be well structured. To be able to make it that way I use the following tools:

- genomedata
- hdf5
- h5py
- pandas
- numpy
- bioawk
- bedtools
- samtools
- awk
- sed
- grep
- shell most of the time :)

I did not use one tool for a big task, instead I combined more than 2-3 tools to do one big task, which allowed me to learn more and use my brain more efficiently.

- First task was to get human genome data and convert it to type which genomedata tool can use it

Human genome data is 3.3gb and in ```fasta``` format. As you may remember from my previous posts, fasta format has description lines for describing the following sequence, starts with ">". In the original file it has a lot of things with this specific word "chromosome". That was what I needed. first thing was to check description lines, if they are usable or not.

```Bash
grep > humangenome38.fa
```

This small line gave me all the lines that has ```>``` inside. I saw that it had more than what I needed

```Bash
grep > humangenome38.fa | wc
```

That line takes every line that has ```>``` inside, and get the count of it. ```wc``` counts the lines, words, and characters. After running the command above, result was 480 lines, which was not a result that I needed. I needed 23, chromosome number in each genome, unless genome has a genetic problem.

Then I should get only those it has chromosome 1/2/3/.../Y inside of it. I solved this problem with using [bioawk](http://ged.msu.edu/angus/tutorials-2012/monday-june-11-links.html) tool

```Bash
./bioawk -cfastx 'BEGIN{while((getline k <"chrID.txt")>0)i[k]=1}{if(i[$name])print ">"$name"\n"$seq}' hg38.fa
```

This line only takes sequences and save description as ```>chr1```.

Here are more scripts that you can use:

```Bash
# How to modify the HumanGenome38 form that task asks for

# Get all the necessary id's with in the
./bioawk -cfastx 'BEGIN{while((getline k <"chrID.txt")>0)i[k]=1}{if(i[$name])print ">"$name"\n"$seq}' hg38.fa
# OR
awk 'NR==1{printf $0"\t";next}{printf /^>/ ? "\n"$0"\t" : $0}' test.fa | awk -F"\t" 'BEGIN{while((getline k < "chrID.txt")>0)i[k]=1}{gsub("^>","",$0); if(i[$1]){print ">"$1"\n"$2}}'

# Create a new file with the lines between chromosome 1 and chromosome 2
sed -n "/.*chromosome 1.*/,/.*chromosome 2.*/p" HumanGenome38.fa > hg38_chr1.fa

# Need to Extract the last line since it contains chromosome 2
sed -i '$ d' hg38_chr1.fa


# Also for the task we need to have only > chr 1 for the description
# Make a temporary file to append them all
echo ">chr1" > chr1.fa

# get the length of the lines in seq
wc -l hg38_chr1.fa

# 17155298 in our case so  we will append the lines except the first line
tail -17155297 hg38_chr1.fa >> chr1.fa

# At the end we get the fasta file that we want.


## How to get only chr1 from HeLa cells using Terminal

# Takes only chromosome 1 from whole data
grep -P 'chr1\t' test27.bg > K27ac_chr1.bg

# Takes only chromosome 1 from whole data
grep -P 'chr1\t' test36.bg > K36me3_chr1.bg

# Now we have two HeLa cells which has only chr1 information available


## Creating a sample dataset using data that we modified:

# Need genomedata-load to load the datasets

# Command: genomedata-load
# Sequence: chr1.fa (Human Genome)
# Tracks:
	# K27ac: K27ac_chr1.bg
	# K36me: K36me3_chr1.bg
# Dataset Name: genomedataset.test

genomedata-load -s chr1.fa -t K27ac=K27ac_chr1.bg -t K36me3=K36me3_chr1.bg  genomedataset.test


# viewing bam file using samtools
samtools view HeLa_RNA-seq.bam | less -S

# Taking only chr1 from bam file
samtools view HeLa3_Cyt.bam | awk -v OFS='\t' '$3=="chr1" {print}' > HeLa3_Cyt_chr1.bam


# Creating genomedataset for all the HeLa cell we have
genomedata-load -s hg38_new.fa -t 3H3k36me3StdSig=wgEncodeBroadHistoneHelas3H3k36me3StdSig.bg -t 3CtcfStdSig=wgEncodeBroadHistoneHelas3CtcfStdSig.bg -t 3H3k4me2StdSig=wgEncodeBroadHistoneHelas3H3k4me2StdSig.bg -t 3H3k04me1StdSi=wgEncodeBroadHistoneHelas3H3k04me1StdSig.bg -t 3H3k4me3StdSig=wgEncodeBroadHistoneHelas3H3k4me3StdSig.bg -t 3H3k09me3Sig=wgEncodeBroadHistoneHelas3H3k09me3Sig.bg -t 3H3k79me2StdSig=wgEncodeBroadHistoneHelas3H3k79me2StdSig.bg -t 3H3k27acStdSig=wgEncodeBroadHistoneHelas3H3k27acStdSig.bg -t 3H3k9acStdSig=wgEncodeBroadHistoneHelas3H3k9acStdSig.bg -t 3H3k27me3StdSig=wgEncodeBroadHistoneHelas3H3k27me3StdSig.bg -t 3H4k20me1StdSig=wgEncodeBroadHistoneHelas3H4k20me1StdSig.bg All_Hg38_HeLa.test
# Modifying description of Human Genome fasta file
# >* into chr1, chr2 ... chr3
awk '/^>/{print ">chr" ++i; next}{print}' < HumanGenome38.fa

# Concatenate
```
---

bedtools
---

```Bash
# Bedtools Tool usage commands



## Get the intersection exons and write them in newReferenceExons.bed
## Also careful with strand (+,-) with -s
bedtools intersect -s -a table_ref.bed -b ensMergedExons.bed > newReferenceExons.bed

## Sort the files
sortBed -i exonIntersectB.bed > exonIntersectBSorted.bed


## Add columns to the file
awk 'BEGIN{FS=OFS="\t"}{print $1,$2,$3,"x","x",$4}' exonIntersectBSorted.bed > testB.bed

## Merging the File
bedtools merge -i testB.bed -s > exonMergedB.bed

```
