---
layout: post
title: Getting Started with Next Generation Sequencing
tags:
- Bioinformatics
- Python
---

Here I am, with you again. Today's post will be about the the getting started part of ```Next Generation Sequencing```. Let's start with defining what is Next-generation Sequencing:

__Next-generation Sequencing (NGS)__ is one of the fundamental technological developments of the decade in life sciences. NGS is the main reason for computational biology becoming a "big data" discipline. More than anything else, this is a field that requires strong bioinformatics techniques.

We will use the the index file from [1000genomes.org](http://www.1000genomes.org/). You should download that file(~61mb) if you haven't. If you were following my blog from beginning, you are just alright, because we downloaded this file at the very beginning. The recipes presented here in this topic and following ones will be easily applicable for other genomic sequencing approaches too.

Recipes that we will use here is species-independent. So, you will be able to apply them to any other species for which you have sequenced data

File Formats
---

__FASTA__:

FASTA format is a text-based bioinformatics file format for representing sequences. In this sequencese nucleotides or aminoacids are represented with single-character codes. Because of it's simplicity in parsing with scripting languages it became very popular on Bioinformatics community.

```
>gi|31563518|ref|NP_852610.1| microtubule-associated proteins 1A/1B light chain 3A isoform b [Homo sapiens]
   MKMRFFSSPCGKAAVDPADRCKEVQQIRDQHPSKIPVIIERYKGEKQLPVLDKTKFLVPDHVNMSELVKI
   IRRRLQLNPTQAFFLLVNQHSMVSVSTPIADIYEQEKDEDGFLYMVYASQETFGFIRENE
```

In the example above, you see in the first line starts with ```>``` we have the ```id``` and ```description``` of the sequence. Then sequence itself comes in next lines. In on ```FASTA``` file you may find more than one ```id``` and ```description``` as well as sequence so be aware when you get those sequences.

__FASTQ__:

```FASTQ``` format is a text-based bioinformatics file format to store both a biological sequence and its corresponding quality scores.

A ```FASTQ``` file normally uses four lines per sequence:

- Line 1 begins with a ```'@'``` character and is followed by a sequence identifier and an optional description (like a FASTA title line).
- Line 2 is the raw sequence letters.
- Line 3 begins with a ```'+'``` character and is optionally followed by the same sequence identifier (and any description) again.
- Line 4 encodes the quality values for the sequence in Line 2, and must contain the same number of symbols as letters in the sequence.

> The character '!' represents the lowest quality while '~' is the highest.

Following is an example of ```FASTQ``` file.

```
@SEQ_ID
GATTTGGGGTTCAAAGCAGTATCGATCAAATAGTAAATCCATTTGTTCAACTCACAGTTT
+
!''*((((***+))%%%++)(%%%%).1***-+*''))**55CCF>>>>>>CCCCCCC65
```

Since you already know what I focus on, you should be familiar with Python. Also some basic genomic terms, you have to know to understand the concept fully.

Share your thoughts with me by commenting below...

> Until next time, be safe...
