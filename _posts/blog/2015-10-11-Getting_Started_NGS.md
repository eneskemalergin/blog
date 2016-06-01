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

Let's go ahead and talk about how to reach the databases and get data from them using Python scripts.

### GenBank and NCBI

Even if you have your own data to analyze, you will need other datas from internet or from other researchers results time to time. __NCBI(National Center of Biotechnology Information) has an extensive database on sequences called "```GenBank```", in this blog post we will learn how to access that database and get data from it. Also I will put other databases for you that you can try.

For this task we will use ```BioPython``` library of Python, since it has very large options and already defined functions to make our life easier. ```Biopython``` provides an interface to ```Entrez```, the data retrieval system made available by ```NCBI```.

> Since we are requesting data transfer from NCBI live API, we should follow the rules of NCBI. You can see the rules and requirements [here](http://www.ncbi.nlm.nih.gov/books/NBK25497/#chapter2.Usage_Guidelines_and_Requiremen.)

- Let's Access with Entrez and call libraries

```Python
from Bio import Entrez, SeqIO # These are the libraries we will use
Entrez.email = "your@email.goes.here" # You should give your email, and store it in Entrez.email
```
- We will now try to find the ```Cholroquine Resistance Transporter``` (CRT) gene in ```Plasmodium falciparum``` (the parasite that causes the deadliest form of malaria) on the nucleotide database:

```Python
# Defining the search criteria
# We put which database to look for
# and which terms to look for
handle = Entrez.esearch(db='nucleotide', term='CRT [Gene Name] AND "Plasmodium falciparum"[Organism]')
# Read the searched ones and store them into rec_list
rec_list = Entrez.read(handle)
# If actual results are more than page result limit
if rec_list['RetMax'] < rec_list['Count']:
    # Then check other pages result as well
  handle = Entrez.esearch(db='nucleotide', term='CRT [Gene Name] AND "Plasmodium falciparum"[Organism]', retmax=rec_list['Count'])
  rec_list = Entrez.read(handle)
```

Note that the standard search will limit the number of record references to 20, so if you have more, you may want to repeat the query with an increased maximum limit. In our case, we will actually override the default limit with ```retmax```.

- Let's now try to retrieve all these records. The following query will download all matching nucleotide sequences from ```GenBank```.

```Python
# Take the id's of the records
id_list = rec_list['IdList']
# Get them with defined id_list
hdl = Entrez.efetch(db='nucleotide', id=id_list, rettype='gb')
```

> Alert: The code above most likely download very large amount of data.

There are several ways around this. One way is to make a more restrictive query and/or download just a few at a time and stop when you have found the one that is enough.

- Let's read and parse the result:

```Python
recs = list(SeqIO.parse(hdl, 'gb'))
```
As you realized we converted it into list, that we can use the result as many times as we want. This saves time, bandwidth, and server usage if you plan to iterate many times over. The disadvantage is that it will allocate memory for all records.

- We will now just concentrate on a single record:

```Python
for rec in recs:
  if rec.name == 'KM288867':
    break
```

The ```rec``` variable now has our record of interest. The ```rec.description``` will contain its human-readable description

- Let's now extract some sequence features, which contain information such as gene products and exon positions on the sequence:

```Python
for feature in rec.features:
  if feature.type == 'gene': # If the feature type is gene
    print(feature.qualifiers['gene']) # print it's name
  elif feature.type == 'exon': # If exon
    loc = feature.location # save the location
    print(loc.start, loc.end, loc.strand) # Print location's start, end and strand
  else: # If none of above
    print('not processed:\n%s' % feature) # Simply print it
```

We will now look at the annotations on the record, which is mostly metadata that is not related to the sequence position:

```Python
# Prints the names and values of annotations in the record.
for name, value in rec.annotations.items():
  print('%s=%s' % (name, value))

# Simply shows the sequence itself
sequence = rec.seq
```

There are also other databases that we can use like,  __short read archive (SRA)__. Other useful one is called __PubMed__, which includes a list of scientific and medical citations, abstracts, even full texts.

```Python
from Bio import Medline # Import necessary library
refs = rec.annotations['references'] # get the annotations with reference key word
for ref in refs: 
  if ref.pubmed_id != '':
    print(ref.pubmed_id)
    handle = Entrez.efetch(db='pubmed', id=[ref.pubmed_id], rettype='medline', retmode='text')
  records = Medline.parse(handle)
  for med_rec in records:
    print(med_rec)
```
This code above will take all reference annotations; check whether they have a PubMed identifier and then access the PubMed database to retrieve the records, parse them, and then print them.

Share your thoughts with me by commenting below...

> Until next time, be safe...
