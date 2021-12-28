---
toc: true
title: "Software"
permalink: /software/
---

### Inference of paternity and sibling relationships

Reconstructing natural 'pedigrees' - the relationships between parents and offspring, and between siblings - is a [very useful tool](https://royalsocietypublishing.org/doi/full/10.1098/rspb.2007.1531) for investigating processes in natural populations, because it allows you to directly measure true fitness - that is to say the actual number of offspring produced by individuals.
Biologists have been reconstructing pedigrees from genetic data since the 1980s, but inferences from such analyses are most reliable when you can include as much data about the pedigree as possible, for example:

1. Genotying more loci, at substantial additional cost
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
