---
layout: single
title: "What the heck is BLAST?"
description: A, hopefully, simple explainer on the bioinformatics tool BLAST
header:
  teaser: "unsplash-gallery-image-2-th.jpg"
categories:
  - "What the heck is"
  - BLAST
  - Software
  - Bioinformatics
tags:
  - BLAST
  - biology
  - genomics
  - bioinformatics
---

BLAST is one of the more commonly used tools by biologists to investigate DNA sequences, whether the sequencing is achieved with traditional Sanger sequencing, or next-generation sequencing. At a basic level, it takes an input sequence of DNA or amino acids, and tries to find a 'best match' in a database. The majority of people will use the tool through the NCBI web interface, and find alignments within the nt (nucleotide) database.

## Etymology
BLAST stands for Basic Local Alignment Search Tool, first described in the original BLAST paper by Altschul et al, 1990 [^1] (back when acronyms weren't so tortured!).
Unfortunately even after nearly 20 years, it's still behind a paywall.

You'll commonly see BLASTN, BLASTX, BLASTP (or variants of), these refer to additional variations of BLAST that have been developed since the initial release of the tool that can be used to investigate nucleotide sequences (BLASTN), amino acid sequences (BLASTP), or amino acid sequences from nucleotide sequences (BLASTX).

## How does it work?



# Bit scores and E-values
Bit scores are a metric for summarising alignments
 - The number of identities (I)
 - The number of mismatches (X)
 - The number of gaps (O)
 - The length of the gaps (G)
Each of the values is multiplied by a co-efficient (these will normally be set by default).
The 'raw' Bit score is then calculated as:
R = (I x a) + (X x b) - (O x c) - (G x d)

A bit more maths using natural log and greek letters goes into obtaining what is called a Normalised Bit score. This gives you a result independent of the scoring system used. I'm not going into detail here...the NCBI has an in depth page on statistics I recommend if you're interested [^1].

An E-value, or 'Expected value' is your best measure of 'significance' of a result.
It takes the output of the normalised Bit Score (S) and turns it into a probability value.
This represents the likelihood of finding a match in your database as good as your query (or better), by chance.

The E-value (the lower the better!) is considered the best means of assessing the quality of a hit.

## Pitfalls and issues


E-values rely on the length of the query and the size of the database used.
This means if you search a different database with the same query you can't compare your E-values between results.
## References

[^1]: [Altschul et al, 1990, J Mol Bio, Basic local alignment search tool](https://www.ncbi.nlm.nih.gov/pubmed/2231712)
[^2]: [The Statistics of Sequence Similarity Scores](https://www.ncbi.nlm.nih.gov/BLAST/tutorial/Altschul-1.html)
