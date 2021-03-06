Longreads vs. Shortreads
========================================================
author: Prof. Harbert
date: 05 February, 2019
autosize: true

Resources for R Labs
========================================================

[ggplot cheatsheet](https://www.rstudio.com/wp-content/uploads/2016/11/ggplot2-cheatsheet-2.1.pdf)

Goals
====================

Understand the division between long and short read DNA sequencing technology.

Conceptualize the scale of the difference involved in mapping long vs. short reads.

Discuss how both are used for hybrid assembly of genomes

Dividing Sequencing Tech
========================================================

"Short read" Technology includes:
- Illumina platforms (Sequencing by Synthesis)
- Ion Torrent

***

"Long read" Technology includes:
- Pacific Biosciences (PacBio)
- Oxford Nanopore

*Long read technology is sometimes called "Third Generation Sequencing" and sometimes separated into Third and Fourth gen.

What separates "Long" and "Short"
========================================================

Short read tech tends to have fixed read lenghts of 50-150bp depending on the platform. 

What qualifies as long? That depends on when you ask that question. A safe answer might be [2000-10000bp](https://www.omicsonline.org/open-access/generations-of-sequencing-technologies-from-first-to-next-generation-0974-8369-1000395.pdf) but people are working to get [longer and longer reads](https://nanoporetech.com/about-us/news/world-first-continuous-dna-sequence-more-million-bases-achieved-nanopore-sequencing) using careful laboratory and sequencing [protocols](http://lab.loman.net/protocols/).

Why does this matter?
=========================================================

Some features of genomes are difficult to "see" with short reads:
- low-complexity regions
- repetitive sequences 
- heterozygous elements

We can visualize general trends with simulated matching of random DNA segments of variable lengths to a genome...

E.g., The E. coli genome
=========================================================

The *E. coli* [genome](https://www.nature.com/articles/35054089) is ~4,100,000bp (4.1Mb) long. 

![E.coli Genome](images/ecoli.jpg)

E.g., The E. coli genome
=========================================================

IF we assume this is made up of randomly generated DNA, what is the probability that any randomly selected base is an "A"? What about the segment "ATCTA"? "ATCTATAT"?

Random nucleotide strings
=======================================================

For random sequence (no bias in base identity) we can express the probability of a random sequence occurring as:

$$
P(seq) = 0.25^n
$$

Where 'n' is the length of the nucleotide sequence string.

Random nucleotide strings
=======================================================

How often would a specific sequence be produced by drawing a random string?

<img src="longreads-figure/unnamed-chunk-1-1.png" title="plot of chunk unnamed-chunk-1" alt="plot of chunk unnamed-chunk-1" style="display: block; margin: auto;" />
But we have a lot of chances to select any given string in 4,100,000bp...

Probability of matching to the genome
======================================================

The probability of matching a random nucleotide string to a genome can be represented as:

$$
P(Match) = S * 0.25^n
$$

Where *S* is the size of the genome and *n* is the size of the nucleotide string.

Probability of matching to a genome
======================================================

<img src="longreads-figure/unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />

*NOTE: Horizontal line represents P(Match) = 1. How should you interpret P()=1?

But what about the probability of correctly matching a whole sequencing experiment of, let's say 5 million reads between 50-150bp?

Probability of matching to a genome
======================================================

Typical read lengths for short read platforms are 50-150bp x 5 million reads

<img src="longreads-figure/unnamed-chunk-3-1.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" style="display: block; margin: auto;" />

Scaling up
=========================

Using a log-scale we can zoom out to look at 'order-of-magnitude' differences for longer reads

<img src="longreads-figure/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />
NOTE: R runs out of numbers to describe how close to P(Match)=0 we get after *n*=500. 

For datasets composed of reads of >500bp, for our 4.1Mb E.coli genome mapping should be correctly placing reads with near-certainty.

Caveats
=======================

Are genomes random? 

How do new genes arise?

What makes up most of the "junk" (unused) DNA in a genome?

How does this scale with larger genomes? Larger samples?

Any factor that creates repeatable patterns in a genome (duplication, horizontal transfer, recombination) will decrease the certainty with which we can place a sequence read.

Long read accuracy
===========================

![Nanopore Accuracy](images/nanopore_qual.png)

[Nanopore read accuracy](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-018-1462-9)

VS: [Illumina per base accuracy >99%](https://bmcgenomics.biomedcentral.com/articles/10.1186/1471-2164-13-341)


Hybrid Sequencing
========================

In practice what is often done now is to sequence with both long and short reads. 

The long reads provide the genome structure and the short reads are used to correct base identity errors. Leading to a more complete genome that maintains high accuracy.

[Example](https://genome.cshlp.org/content/25/11/1750.full.pdf)


Reading for next class
=========================================================
Check eLearn for the ONT Plant Genome white paper.
Also, read [Assembly of chloroplast genomes with long- and short-read data: a comparison of approaches using Eucalyptus pauciflora as a test case](https://doi.org/10.1186/s12864-018-5348-8)

Suggested Readings
========================================================

https://www.genengnews.com/insights/the-long-and-the-short-of-dna-sequencing/
https://www.omicsonline.org/open-access/generations-of-sequencing-technologies-from-first-to-next-generation-0974-8369-1000395.php?aid=87862

