---
layout: presentation
title: Fantastic Histone Modifications and How to Find Them
theme: white
categories: talks
published: true
---

{{site.startvertical}}
{{site.startslide}}

# Fantastic Histone Modifications and How to Find Them

> Enes Kemal Ergin <br />
> Nov 16, 2017 <br />
> BIOF501 <br />
> Review Presentation

{{site.nextslide}}

## Outline

- Overview of Epigenomics and Epigenetic Modifications
- Histone Modifications
- Chromatin Immunoprecipitation
- ChIP-chip
- ChIP-seq
- Hidden Markov Chains
- Comparing ChIP-chip and ChIP-seq
- Summary

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## Epigenomics and Epigenetic Modifications

{{site.nextslide}}

### What is Epigenomics?

- Study of complete set of epigenetic modifications.
- Large scale study than a single gene study.
- Have an important role in gene expression and regulations.

{{site.nextslide}}

### Epigenetic Modifications I

- Heritable changes not due to changes in DNA sequence
- Cause of variation

{{site.nextslide}}

### Epigenetic Modifications II

<img style="width:350; height:450"  src="{{site.baseurl}}/images/talks/histone_modifications/epigenetic_mechanism_DNA.png"></img>

> [WhatisEpigenetics, 2017](https://www.whatisepigenetics.com/type-2-diabetes-mellitus-and-epigenetics/)

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## Histone Modifications

{{site.nextslide}}

### Histones and Their Modifications

- Histone is known for condensing of DNA functionality.
- Chromatin structure and density of its DNA packaging effects gene expression.
- Histone proteins affect the gene expression.
- There are 3 well studied modifications:
  - Acetylation
  - Methylation
  - Phosphorylation

{{site.nextslide}}

### Importance of Histone Modifications

- Histone proteins have key roles:
  - Gene regulation
  - DNA damage repair
  - Transcription and Replication
- Important for understanding epigenetic regulation.

{{site.nextslide}}

### Roles of Histone Modifications

<img src="{{site.baseurl}}/images/talks/histone_modifications/roles_of_histone_modifications.png"></img>

_(Jayani et al 2010)_

> [](#)


{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## Chromatin Immunoprecipitation

{{site.nextslide}}

### What is ChIP

- Tool to determine DNA sequences associated with protein of interest
- ChIP could be used for:
  - Post-transcriptionally modified histones
  - histone variants
  - transcription factors
  - chromatin modifying enzymes
- Scope of experiment could expand to genome-wide scale.

{{site.nextslide}}

### ChIP protocol

<img
src="{{site.baseurl}}/images/talks/histone_modifications/chip.png"></img>

{{site.nextslide}}

### ChIP Followed by Microarray and Sequencing

- __ChIP-chip__ (DNA microarray)
- __ChIP-seq__ (Next Generation Sequencing)


{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## ChIP-chip Method

{{site.nextslide}}

### What is ChIP-chip

- High resolution genome-wide profiling
- Has wide variety of applications
- Has also limitations:
  - Antibody quality
  - Need for large number of cells
  - Long, expensive and hard to troubleshoot


{{site.nextslide}}

### Figure for ChIP-chip

<img src="{{site.baseurl}}/images/talks/histone_modifications/chip-chip_overview.gif"></img>

{{site.nextslide}}


### ChIP-chip Data Processing

- Hybridization quality control,  
- Intra and Inter-array normalization  
- Peak Detection
- Motif Discovery
- Genomic average profiles
- Gene Clustering

{{site.nextslide}}

### The Output of ChIP-chip

<img src="{{site.baseurl}}/images/talks/histone_modifications/chip-chip_output.jpg"></img>

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}


## Applications used ChIP-chip

- HMMtiling
- TileMap
- Ringo

{{site.nextslide}}

### HMMtiling

Add figure to summarize the paper

{{site.nextslide}}


### TileMap

Add figure to summarize the paper

{{site.nextslide}}

### Ringo

Add figure to summarize the paper

{{site.nextslide}}

### Comparison of the Applications

Add a table that compares some aspects

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## ChIP-seq Method

{{site.nextslide}}

### What is ChIP-seq

- ChIP combined with high-throughput sequencing
- Genome-wide profiling
- Handling repetitiveness with high confidence
- Greater resolution, sensitivity, and specificity
- More common since 2007

{{site.nextslide}}

### Figure for ChIP-seq

<img src="{{site.baseurl}}/images/talks/histone_modifications/ChIP-seq_overview.jpg"></img>

{{site.nextslide}}

### Data Processing in ChIP-seq

<img src="{{site.baseurl}}/images/talks/histone_modifications/chip-seq_bioinformatics_workflow.png"></img>

{{site.nextslide}}

### Be Aware of the Bias!

<img src="{{site.baseurl}}/images/talks/histone_modifications/short_read.jpg"></img>

{{site.nextslide}}

### Differential Peak Calling in ChIP-seq

- Explain this concept here

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## Applications used ChIP-seq

- HMMChrome
- MACS
- ODIN

{{site.nextslide}}

### HMMChrome

Add figure to summarize the application

{{site.nextslide}}

### MACS

Add figure to summarize the application

{{site.nextslide}}

### ODIN

Add figure to summarize the application

{{site.nextslide}}

### Comparison of the Applications

Add a table that compares some aspects

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## Hidden Markov Models

{{site.nextslide}}

### Understanding HMM

No Math Involved, well maybe __A Little__, Promise!

<img src="https://media.giphy.com/media/ohdY5OaQmUmVW/giphy.gif"></img>

{{site.nextslide}}

#### Markov Models

<img src="{{site.baseurl}}/images/talks/histone_modifications/weather_predicting_cat.jpg"></img>

{{site.nextslide}}

<img src="{{site.baseurl}}/images/talks/histone_modifications/markov_model.png"></img>

{{site.nextslide}}

#### Hidden Markov Models

<img src="{{site.baseurl}}/images/talks/histone_modifications/weather_predicting_cat.jpg"></img>

{{site.nextslide}}

<img src="http://www.reactiongifs.com/r/but-why.gif"></img>

{{site.nextslide}}

### Why HMM is Useful

- Explain the usefulness of HMM in this context

{{site.nextslide}}

### Advantages and Disadvantages of HMM

- Advantages
  - Statistical Foundation
  - Using Raw Data Directly
  - Variable Lengths in Input
- Disadvantages
  - Expressing Dependencies Between Hiddent States
  - Unstructured Parameters

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## ChIP-chip vs ChIP-seq

{{site.nextslide}}

### Advantages and Disadvantages of Both Techniques

Show Advantages and Disadvantages in one table

Make sure to compare them in sensitivity, repeat regions, genome-wide analysis compatibility


{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## Thank You

> Questions?

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## Supplementary Slides

{{site.nextslide}}

### Epigenetic Mechanisms after DNA Level

<img style="max-width: 100%;" src="{{site.baseurl}}/images/talks/histone_modifications/epigenetic_mechanism_supp.png"></img>

{{site.nextslide}}

### Histone Modifications List

- __Acetylation__ (gene activation)
- __Methylation__ (gene activation,  gene repression)
- __Phosphorylation__ (gene activation)
- Ubiquitination (gene activation, gene repression)
- SUMOylation (gene repression)
- ADP-ribosylation  
- Deamination (gene repression)
- Proline isomerization (gene repression)

There is a nice reference of full table of Histone Modifications list in the __[cellsignal](https://www.cellsignal.com/contents/resources-reference-tables/histone-modification-table/science-tables-histone)__ website


{{site.nextslide}}

### Post-translational Modifications on Core Histones

<img style="max-width: 100%;" src="{{site.baseurl}}/images/talks/histone_modifications/PTM_of_core_histones.png"></img>

_(Jayani et al 2010)_

> [Sup Fig 1: PTMs on Core Histones](https://www.ncbi.nlm.nih.gov/pubmed/20816229)

{{site.nextslide}}

### Mass Spectrometry Based Detection of Histone Modifications

Add figure here

{{site.nextslide}}

### ChIP-chip Full Protocol

<img src="{{site.baseurl}}/images/talks/histone_modifications/">

{{site.endslide}}
{{site.endvertical}}
