

This small tutorial consists of 10 parts from [Snipcademy](http://binf.snipcademy.com/lessons/pairwise-alignment).


1. Introduction to Pairwise Alignment
---

 - Aligning two DNA, RNA, or protein sequences such that the regions of similarity are maximized.
 - Scientists use to find relatedness, quantitatively. They are able to identify common domains and motifs, and sequence ancestry.

> Domain: They are parts of a DNA or amino acid strand that code for physiochemically similar feature as found in other sequences and proteins. They refer to specific functionalities.

> Motifs: They reference the structural characteristics rather than functional regions. They often found in domains.


### Protein versus DNA Sequence Alignment
Protein amino acid sequences are preferred over DNA sequences for a list of reasons.

- Protein residues are more informative - a change in DNA (especially the 3rd position) does not necessarily change the AA.
- The larger number of amino acids than nucleic acids makes it easier to find significance.
- Some amino acids share related biochemical properties, which can be accounted for when scoring multiple pairwise alignments.
- Protein sequence comparisons can link back to over a billion years ago, whereas DNA sequence comparisons can only go back up to 600 mya. Thus, protein sequences are far better for evolutionary studies.

However, there are some obvious instances when DNA alignments are needed.

- When confirming the identity of cDNA (forensic sequencing).
- When studying noncoding regions of DNA. These regions evolve at a faster rate than coding DNA, while mitochondrial noncoding DNA evolves even faster.
- When studying DNA mutations.
- When researching on very similar organisms such as Neanderthals and modern humans.

To be able to understand the Protein and DNA sequencing we should have a good knowledge on Codes for nucleotides and Amino Acid residues.

__Nucleotide Codes__
![NucleotideCodes](https://github.com/eneskemalergin/eneskemalergin.github.io/blob/master/images/NucleotideCodes.png)


__Amino Acid Residue Codes__
![AminoAcidCodes](https://github.com/eneskemalergin/eneskemalergin.github.io/blob/master/images/AminoAcidResidue.png)

2. Homology - a Qualitative Measure
---

> Homology: it is "the same organ in different animals under every variety of form and function."

Today, we use the term homology is used to characterize biological species that share a common evolutionary ancestory.

> Homology is strictly qualitative measure in binary for which mean either two sequences are homologous or not.

### Orthologous versus Paralogous
These are two subclasses of the homology concept.

_Paralogous:_
  - is when gene duplication occurs, but both copies descend side-by-side during the history of the organism (para = in parallel).
  -  occurs within the species.
  - Paralogous genes are assumed to carry common functions.

_Orthologous:_
  -  When speciation occurs, and a gene is inherited in both species, these sequences are said to be orthologous (ortho = exact).

In simplified terms, orthology is the homology between species, while parology is the homology within species.

If you see the figure below from Jensen et al., the ancestral gene has two copies of a particular gene (A and B). Relative to the ancestral genome, this is considered paralogs since they are within its own species.

![Homology](https://github.com/eneskemalergin/eneskemalergin.github.io/blob/master/images/Homology.png)

However, once speciation occurs, two copies of genes A and B are created. Since the duplication of A and B genes occurred before speciation, A and B genes are still considered paralogs. However, genes A1 and A2 are orthologs, as are B1 and B2.

In the second case, gene duplication occurs after speciation. Thus, A2 and B2 are orthologs of A1, while A2 and B2 are paralogs of each other.

3. Identity and Similarity - a quantitative measure
---

To assess the similarity we use pairwise-alignments. Pairwise alignment algorithms find the optimal alignment between two sequences including gaps. Example Algorithms:

 - BLAST
 - FASTA
 - LALIGN

After an alignment is made, we can extract two quantitative parameters from each pairwise comparison - identity and similarity.
