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
- ChIP-chip vs ChIP-seq

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
- Most studied:
  - DNA Methylations
  - Histone Modifications


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

### ChIP-chip Overview

<img src="{{site.baseurl}}/images/talks/histone_modifications/chip-chip_overview.gif"></img>

{{site.nextslide}}


### Data Processing in ChIP-chip

- Array normalization
- Peak Detection

{{site.nextslide}}

### The Output of ChIP-chip

<img src="{{site.baseurl}}/images/talks/histone_modifications/chip-chip_output.jpg"></img>

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

### ChIP-seq Overview

<img src="{{site.baseurl}}/images/talks/histone_modifications/Chip_seq_overview.png"></img>

{{site.nextslide}}

### Data Processing in ChIP-seq

<img src="{{site.baseurl}}/images/talks/histone_modifications/chip-seq_bioinformatics_workflow.png"></img>

{{site.nextslide}}

#### Quality Control/Check

- Fundamental Step(s)
- Fully automated or Manually
- Aided by Visuals
- Tools like ChIPQC(R/Bioconductor)

{{site.nextslide}}

#### Alignment
Mapping - Sorting - Removing

1. Map reads to genome (__Bowtie2, BWA, STAR__)
2. Sort the mapped reads (__Samtools__)
3. Remove the duplicates

{{site.nextslide}}

##### Be Aware of the Bias!

<img src="{{site.baseurl}}/images/talks/histone_modifications/short_read.jpg"></img>

{{site.nextslide}}

#### Normalization

- Must be done when have multiple experiments.
- In absence could result bias in peak calling phase.

{{site.nextslide}}

#### Peak Calling

- Main point for optimization for years.
-

{{site.nextslide}}

##### Differential Peak Calling in ChIP-seq

- Explain this concept here

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## ChIP-chip vs ChIP-seq

{{site.nextslide}}

| Features        | ChIP-chip       | ChIP-seq  |
| -------------   |:-------------:| -----:|
| __Resolution__      | Array Specific | Single Nucleotide - High |
| __Coverage__        | Limited by Sequences on the Array |  Limited by alignability of reads |
| __Sensitivity__     | Low Sensitivity | High Sensitivity |
| __Repeat Elements__ | Masked out   |  Can be covered |
| __Cost__            | Expensive | Relatively Cheaper |
| __Source of Noise__ | Cross Hybridization | Sequencing, GC bias, Sequencing error |
| __ChIP DNA__        | Large amount needed | Low amount necessary |


{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## Hidden Markov Models

{{site.nextslide}}

### Understanding HMM

No Math Involved, Promise!

<img src="https://media.giphy.com/media/ohdY5OaQmUmVW/giphy.gif"></img>

{{site.nextslide}}

#### Markov Models

<img src="{{site.baseurl}}/images/talks/histone_modifications/weather_predicting_cat.jpg"></img>

{{site.nextslide}}

<img src="{{site.baseurl}}/images/talks/histone_modifications/markov_model.png"></img>

{{site.nextslide}}

#### Hidden Markov Models

<img src="{{site.baseurl}}/images/talks/histone_modifications/wheater_predicting_cat_in_box.jpg"></img>

{{site.nextslide}}

### Why HMM is Useful

<img src="http://www.reactiongifs.com/r/but-why.gif"></img>

{{site.nextslide}}

<img src="{{site.baseurl}}/images/talks/histone_modifications/chip_seq_modeling_hmm_1.gif"></img>

{{site.nextslide}}

<img src="{{site.baseurl}}/images/talks/histone_modifications/chip_seq_modeling_hmm_2.gif"></img>

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

## Thank You

> Questions?

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## Supplementary Slides


{{site.nextslide}}

### Epigenetic Mechanisms DNA Level

<img style="width:350; height:450"  src="{{site.baseurl}}/images/talks/histone_modifications/epigenetic_mechanism_DNA.png"></img>

> [WhatisEpigenetics, 2017](https://www.whatisepigenetics.com/type-2-diabetes-mellitus-and-epigenetics/)

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

### Roles of Histone Modifications

<img src="{{site.baseurl}}/images/talks/histone_modifications/roles_of_histone_modifications.png"></img>

{{site.nextslide}}

### Post-translational Modifications on Core Histones

<img style="max-width: 100%;" src="{{site.baseurl}}/images/talks/histone_modifications/PTM_of_core_histones.png"></img>

{{site.nextslide}}

### Extensive ChIP-seq Workflow

<img style="max-width: 100%;" src="{{site.baseurl}}/images/talks/histone_modifications/chip_seq_workflow.jpg"></img>

{{site.nextslide}}

### ChIP-seq Quality Check
<img style="max-width: 100%;" src="{{site.baseurl}}/images/talks/histone_modifications/chip-seq_vis_qc.jpg"></img>

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

### References

__1-__ Callinan, P. A., & Feinberg, A. P. (2006). The emerging science of epigenomics. Human Molecular Genetics. doi:10.1093/hmg/ddl095 </br>
__2-__ Handy, D. E., Castro, R., & Loscalzo, J. (2011). Epigenetic Modifications: Basic Mechanisms and Role in Cardiovascular Disease. Circulation, 123(19), 2145-2156. doi:10.1161/circulationaha.110.956839 </br>
__3-__ Lennartsson, A., & Ekwall, K. (2009). Histone modification patterns and epigenetic codes. Biochimica et Biophysica Acta (BBA) - General Subjects, 1790(9), 863-868. doi:10.1016/j.bbagen.2008.12.006 </br>

{{site.nextslide}}

__4-__ Jayani, R. S., Ramanujam, P. L., & Galande, S. (2010). Studying Histone Modifications and Their Genomic Functions by Employing Chromatin Immunoprecipitation and Immunoblotting. Methods in Cell Biology Nuclear Mechanics & Genome Regulation, 35-56. doi:10.1016/s0091-679x(10)98002-3 </br>
__5-__ Collas, P. (2009). The State-of-the-Art of Chromatin Immunoprecipitation. Chromatin Immunoprecipitation Assays Methods in Molecular Biology, 1-25. doi:10.1007/978-1-60327-414-2_1 </br>
__6-__ Lee, T. I., Johnstone, S. E., & Young, R. A. (2006). Chromatin immunoprecipitation and microarray-based analysis of protein location. Nature Protocols, 1(2), 729-748. doi:10.1038/nprot.2006.98 </br>

{{site.nextslide}}

__7-__ Cauchy, P., Benoukraf, T., & Ferrier, P. (2011). Processing ChIP-Chip Data: From the Scanner to the Browser. Methods in Molecular Biology Bioinformatics for Omics Data, 251-268. doi:10.1007/978-1-61779-027-0_12 </br>
__8-__ Reinke, V. (2013). Transcriptional regulation of gene expression in C. elegans. WormBook, 1-31. doi:10.1895/wormbook.1.45.2 </br>
__9-__ Newkirk, D., Biesinger, J., Chon, A., Yokomori, K., & Xie, X. (2011). AREM: Aligning Short Reads from ChIP-Sequencing by Expectation Maximization. Lecture Notes in Computer Science Research in Computational Molecular Biology, 283-297. doi:10.1007/978-3-642-20036-6_26 </br>


{{site.nextslide}}

__10-__ Allhoff, M., Sere, K., Chauvistre, H., Lin, Q., Zenke, M., & Costa, I. G. (2015). Detecting differential peaks in ChIP-seq signals with ODIN. Bioinformatics, 31(6), 980-980. doi:10.1093/bioinformatics/btv030 </br>
__11-__ Meyer, I. (2004). Hidden Markov Model (HMM, Hidden Semi-Markov Models, Profile Hidden Markov Models, Training of Hidden Markov Models, Dynamic Programming, Pair Hidden Markov Models). Dictionary of Bioinformatics and Computational Biology. doi:10.1002/9780471650126.dob0318.pub2 </br>
__12-__ Vinciotti, V. (2017). Modelling ChIP-seq Data Using HMMs. Hidden Markov Models Methods in Molecular Biology, 115-122. doi:10.1007/978-1-4939-6753-7_8 </br>

{{site.nextslide}}

__13-__ Ho, J. W., Bishop, E., Karchenko, P. V., Nègre, N., White, K. P., & Park, P. J. (2011). ChIP-chip versus ChIP-seq: Lessons for experimental design and data analysis. BMC Genomics, 12(1). doi:10.1186/1471-2164-12-134 </br>
__14-__ Carroll TS, Liang Z, Salama R, Stark R and de Santiago I (in press). “Impact of artefact removal on ChIP quality metrics in ChIP-seq and ChIP-exo data.” Frontiers in Genetics. </br>
__15-__ Guzman, C., & D’Orso, I. (2017). CIPHER: a flexible and extensive workflow platform for integrative next-generation sequencing data analysis and genomic regulatory element prediction. BMC Bioinformatics, 18(1). doi:10.1186/s12859-017-1770-1 </br>


{{site.nextslide}}

__16-__ Nakato, R., & Shirahige, K. (2016). Recent advances in ChIP-seq analysis: from quality management to whole-genome annotation. Briefings in Bioinformatics. doi:10.1093/bib/bbw023 </br>
__17-__ Diaz, A., Park, K., Lim, D. A., & Song, J. S. (2012). Normalization, bias correction, and peak calling for ChIP-seq. Statistical Applications in Genetics and Molecular Biology, 11(3). doi:10.1515/1544-6115.1750 </br>


{{site.endslide}}
{{site.endvertical}}
