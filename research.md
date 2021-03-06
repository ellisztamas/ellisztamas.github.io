---
layout: page
title: "Research"
permalink: /research/
---

### Flower colour in a snapdragon hybrid zone

Hybrid zones are fantastic tools for investigating how selection acts on natural populations.
Hybrid zones form where two partially diverged populations meet and interbreed, causing alleles to recombine into new combinations that have not previously been tested by selection.
As such, hybrid zones are like evolutionary laboratories where we can observe which combinations thrive and which do not, and try to identify the strength, agent and mechanism of selection acting in real time.

The snapdragon *Antirrhinum majus* has two subspecies with contrasting flower colours; *A. m. pseudomajus* has magenta flowers, while *A. m. striatum* has yellow flowers.
In particular valleys in the Spanish Pyrenees, these subspecies meet and form hybrid zones, and genes controlling flower colour recombine to generate a spectrum of white, orange and pink flowers.
Since flower colour is an important signal to pollinators, and the plants depend on pollinators for reproduction, my [PhD thesis](https://research-explorer.app.ist.ac.at/download/1398/5106/IST-2016-526-v1%2B1_Ellis_signed_thesis.pdf) with Nick Barton at IST Austria focussed on the extent to which pollinators discriminate between plants of different colours and exerted selection on them.

### Inference of paternity and sibling relationships

Reconstructing natural 'pedigrees' - the relationships between parents and offspring, and between siblings - is a [very useful tool](https://royalsocietypublishing.org/doi/full/10.1098/rspb.2007.1531) for investigating processes in natural populations, because it allows you to directly measure true fitness - that is to say the actual number of offspring produced by individuals.
Biologists have been reconstructing pedigrees from genetic data since the 1980s, but inferences from such analyses are most reliable when you can include as much data about the pedigree as possible, for example:

1. Genotying more loci
2. Jointly estimating multiple relationships at once, such as between parents and all their offspring at once
3. Including relevant non-genetic information, such as location or social status.

Methods exist to do these things, but typically pre-date the DNA sequencing revolution of the late 2000s, and as such, tend to be very slow when dealing with SNP data for many individuals.

As part of my PhD I developed a new method, **Fractional Analysis of Sibships and Paternity** (FAPS), to jointly infer paternal and sibling relationships using for large SNP datasets. The key innovations are:

1. FAPS uses hierarchical clustering to identify plausible pedigree sturctures, which removes the need to explore possible pedigrees using a Markov chain, which are typically slow.
2. The relative support (likelihood) for those pedigrees is estimated by Monte Carlo simulation, which allows likelihoods to be calculated in parallel.
3. FAPS automatically integrates over possible sibship structures and paternities for each sibship, rather than identifying a single most likely configuration. This leads to more robust inferences, because you can account for this uncertainty.

Simulations show that FAPS is as accurate and two order of magnitude faster than the current state-of-the-art. 

For full details see:

> Ellis, T. J., Field, D. L., & Barton, N. H. (2018). Efficient inference of paternity and sibship inference given known maternity via hierarchical clustering. *Molecular Ecology Resources*, 18(5), 988-999.

See also the github [repository](https://github.com/ellisztamas/faps) and [documentation](https://fractional-analysis-of-paternity-and-sibships.readthedocs.io/en/latest/index.html), which includes extensive tutorials.

### Local adaptation in *Arabidopsis thaliana*

Local adaptation is the process by which populations respond to the selection pressures in their local environment over time.
Among the best ways to investigate this is to use reciprocal transplant experiments, where individuals from two or more locations are reared in common gardens at each site.
As a postdoc with Jon Ågren at Uppsala university in Sweden I was involved in setting up and analysising large scale reciprocal transplants using ecotypes of *Arabidopsis thaliana* originating in Sweden and Italy to examine the prevalent selection pressures at each site, which aspects of plant phenotype they act on, and to identify the regions of the genomes that respond to that selection.
A particular strength of this project is that experiments have been carried out for more than a decade, which means we can investigate how consistent these effects are between years, and try and identify selection events which occur only rarely but have major impacts on survival and fecundity.

### Methylation variation in *Arabidopsis thaliana*

Nucleotides, especially cytosines, can be methylated by adding a methyl group (CH~3~).
Ecotypes of *Arabidopsis thaliana* from across Europe show remarkable variation in cytosine methylation, and this variation is correlated with climate of origin and transposable element load, but the meaning of this variation is not clear.
My current work focusses is part of a broader effort to understand the biology of these observations.
In particular, my projects focus on growing plants under field conditions.
This is in contrast to most previous work which has investigated methylation variation in controlled growth chambers, which can never capture the full range of environmental cues that might affect the regulation of methylation marks.