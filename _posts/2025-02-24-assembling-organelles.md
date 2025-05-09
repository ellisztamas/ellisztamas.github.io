---
title: Assembling organelles from PacBio hifi reads
toc: true
---
25th February 2025

I previously wrote about my experiences [assembling *Arabidopsis thaliana*
genomes]({% link _posts/2025-02-20-a-n00b-assembles-some-genomes.md %}) using PacBio hifi reads, and some pitfalls I ran into.
The focus was on autosomes, but I also wanted to get good assemblies for the
chloroplast and mitochondria.
In particular I want a good idea of what the chloroplasts look like, because 
these are expected to be unmethylated, so they are often used as a control
sequence to confirm that library and data preparation were valid.

Mitochondrial and chloroplast sequences are a challenge because it can be hard to distinguish organellar sequence from homologous insertions of organellar genomes in the autosomes.
There are a few dedicated programs to do this, and I used TIPP.
See the [GitHub](https://github.com/Wenfei-Xian/TIPP) page and [paper](https://doi.org/10.1093/molbev/msae247).

Here I wanted to share what I learned about assembling organelles.
As in previous posts I have simplified the paths and file names to make the code more readable, so the code won't work out of the box.
To see the working script in action, see the [GitHub repo](https://github.com/ellisztamas/meth_pedigree/blob/main/03_processing/05_genome_assembly/06_assemble_organelles.sh) for this project.

# Prepare the reads

I had the problem that I was able to get enough raw reads to cover the genome at >100x coverage, which I will admit is not a terrible problem to have.
However, because cells have only one nucleus but tons of organelles, I first had to downsample the data to fit into memory so the assembler didn't melt.
I did this with `reformat.sh` from the [BBmap](https://archive.jgi.doe.gov/data-and-tools/software-tools/bbtools/bb-tools-user-guide/reformat-guide/) package.
This command takes the enormous fastq file that I used for the assembly with `hifiasm` and randomly samples 10% of those reads.

```sh
bbmap/reformat.sh \
    in= raw_reads.fastq.gz \
    out=downsampled_reads.fastq.gz \
    samplerate=0.1 \
    sampleseed=1612
```

# Assemble organelles, kinda

The following command identifies and assembles organellar reads to the directory `tipp_dir`.
`-g organelle` tells the program to assemble both the chloroplast and mitochondrion.

```sh
cd tipp_dir
TIPPo.v2.4.pl \
    -t 8 \
    -g organelle \
    -f downsampled_reads.fastq.gz
```

Notice the `cd` command to change directory to the output directory.
Normally I would never use `cd` in scripts, because this is a great way to get yourself into a mess.
I much prefer having a [project-oriented workflow](https://www.tidyverse.org/blog/2017/12/workflow-vs-script/), and defining paths relative to the root of that a project directory.
However, TIPP doesn't have an option to define an output path, so I had to suck it up on this occasion.

# Where are the output files?

TIPP creates many output files, and the output is frankly baffling.
The author of the package [told me](https://github.com/Wenfei-Xian/TIPP/issues/5#issue-2779824136) that for an input file named `downsampled_reads.fastq.gz` the final chloroplast assembly should be in a directory called `downsampled_reads.fastq.gz.organelle` and that the file should be named `downsampled_reads.fastq.gz.chloroplast.fasta.filter.800.round1.edge_3.edge_1.edge_2.organelle.chloroplast.fasta`.

TIPP creates two assemblies for the chloroplast, because it can be that a single genome contains more than one chloroplast genome.
In my case they were identical, so I used the following command to pull out the first assembly and rename it to `my_chloroplast.fasta`. This also changes the sequence key from "Configuration1" to "ChrC".

```sh
# Find the assembly file.
tippo_chloroplast=$(find downsampled_reads.fastq.gz.organelle/*edge*fasta)
# Pull out the sequence with the key ">Configuration1"
awk '/^>/ { if (c++) exit; } { print }' $tippo_chloroplast | 
    awk '/^>Configuration1/{sub("Configuration1", "ChrC")}1' \
    > my_chloroplast.fasta
```

The package author also told me that the mitochondrion assembly should be in the directory
```
downsampled_reads.fastq.gz.mitochondrial.fasta.filter.fasta.flye
```
and that I should look for files `assembly_graph.gfa` or `50.repeat-graph/graph_before_rr.gfa`.
However, I couldn't find these files.
In the end I decided that although I definitely need the chloroplast, I don't need the mitochondrion as urgently, so I did not follow up on this.

# Concatenate autosomes and organelles

I need a single FASTA file containing autosomes and organelles.

I used the assembled chloroplast, but since I couldn't get the mitochondrion to work, I used the mitochondrion from the TAIR10 reference genome.

```sh
cat autosome_assembly.fasta \
    chloroplast_assembly.fasta \
    TAIR10_ChrM.fasta \
    > main_assembly.fasta
```