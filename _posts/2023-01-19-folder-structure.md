---
title: How to structure a research project
toc: true
---
19th January 2023

I've [previously argued]({% link _posts/2023-01-18-separate-project-folders.md %}) that it is a good idea to maintain separate folders for day-to-day project work on data analysis projects from the folders you would use to submit the same project manuscript to a journal.

This post contains some opinionated suggestions about how to do the first of these.
See here for [how to structure a manuscript folder]({% link _posts/2023-01-20-manuscript-folder.md %}).

## Why worry about folder structure?

Here are some things that Are True about a lot of research projects, at least in biology:

* You will probably try many things, many of which won't work. That's fine, but you want to keep track of everything you've done.
* You will come back to things later and not remember what and why you did something.
* Projects are often exploratory and may not have a clear question. That's fine, but you want to be able to keep track of things you've explored.
* If anyone else needs to use or follow up on what you've done, this should be easy for them to work out.

So, a project folder needs to allow for the **flexibility** of very non-linear projects, but still be **transparent and easy to navigate** for someone else or future you. Actively documenting what you have done by annotating your code and [writing READMEs]({% link _posts/2023-09-21-readme-files.md %}) is one, important, part of it. However, you can also help yourself enormously by structuring your project folder in a way that makes it easy to know where things are and what order to run things in. Sticking to that structure is like a partial passive documentation. The best way to do this might depends on the project at hand, but the template outlined below will work in most cases - it is much better to start with some kind of structure than nothing at all.

I strongly recommended **starting a project folder with a clear structure right from the beginning of a project** and fill in as you go, because that way you set up a scaffold and just 'fill in the blanks'. It is unwise to start with no structure and tell yourself that you will tidy it later, because realistically you won't.

## A template structure

The best way to structure a project folder depends on the project, but the example below will work in the majority of cases, and can be adapted as necessary.
```
01_data
02_library
03_processing
04_results
05_reports
06_presentations
07_manuscript
slurm
README.md
LICENSE
```

There are eight main folders with names that make obvious, or mostly obvious, what each contains. They are numbered so they appear roughly in the order you would want to deal with them (i.e. projects start with raw data and finish with published manuscript). The numbers also mean its quick to autocomplete directory names on the command line; if you want to go to `06_presentations` you just type `06` and hit tab to autocomplete. If there were no numbers you'd have to distinguish between `presentations` and `processing`.

There are a couple of other things there:

* `README.md` tells the reader what the folder is about and how to use it. [It is absolutely essential]({% link _posts/2023-09-21-readme-files.md %}).
* `slurm`: The HPC where I work uses SLURM to schedule compute jobs. This serves as a folder to store the `.out` and `.err` files that those jobs generate.
* `LICENSE` is a license file telling people what they can and cannot do with your code. It's a good idea to include one if your code goes on GitHub. See [https://choosealicense.com/ https://choosealicense.com/] for how to choose a license. If you aren't sure, use the MIT license.

## What to put where?

### Data

A folder to house the raw data for the project.

Some point about managing data:

1. Depending on the project it may be sensible to have subfolders for raw and processed data files.
2. If you haven't done so in the main project folder README, give a README file here with a description of each data file here and what each variable means, or else point the reader to where they can find that information.
3. Never edit raw data files by hand or in a program like Excel except to add more data, because there is no record of what you have done. Instead, write code to do it and put either here or in `03_processing`, and link to it here.

<!-- If data files are already stored somewhere else, don't make a copy. Make a [https://wiki.nordborg.vbc.ac.at/index.php/Soft_link_data_files soft link] instead. -->

### Library code

Use this folder to store library code, that is functions and generic scripts that can be used again and again with different parameters.
This is a safer way to maintain your code than copy-pasting code repeatedly because you only have to maintain code in one place.
For example, the [https://wiki.nordborg.vbc.ac.at/index.php/Multitrait_GWA_(using_Limix) this example] gives a generic script to run a multitrait GWAS. You would put the script here, and actually call it as many times as you need to in your results.

This is good software-development practice, which will make your science better. See [this excellent video](https://www.youtube.com/watch?v=zwRdO9_GGhY) by Richard McElreath on the topic.

### Data processing

Use this folder for scripts for processing raw data to get it into a format you can use for generating results.

This distinct from ''library code'' in that it is doing something specific to data, and will usually use library code to do that.
It is also distinct from code for generating results. Processing scripts prepare data for analysis, which can then be looked at in different ways to produce a range of results.

There is flexibility in where to store the output. If the processing is not too demanding, you can also just call the processing scripts at the start of every results script. That way, if there are updates to the raw data, the processed data will be updated automatically as well.

### Results

A folder to store code to generate individual results.

You will probably generate many individual results, many of which won't be interesting, but you do want to keep track of everything you've done so you can come back to it later.
The goal here is to identify the smallest questions possible and address them one at a time in individual subfolders that you can easily keep an overview of.

#### Create a good results subfolder

1. Break up your overal scientific questions(s) into very specific questions you can address one at a time. For example, a standard GWA on your data would be one question, and a multitrait GWA another.
2. For each question, create a subfolder here with a succinct but informative name
3. Number subfolders in the order you do them, so you have a chronological overview of what you've done. (Label by date if you wish, but this gets messy).
4. Add scripts to do what you need to do and analyse the results, and save the output in the subfolder.
5. Add a results_summary file to briefly summarise what you did and why, with a main message. This is primarily to help you work out what you did ''quickly'' when you come back to this in the future.

#### Example result

Here is an example of how a result subfolder might look like for a simple GWAS
analysis of a disease phenotype.

The directory contains scripts numbered to indicate the order they should be run
in, a directory to store the results, and a summary of the results.
```
output
01_format_phenotypes.R
02_kruskall_wallis_gwas.sh
results_summary.md
```

`02_kruskall_wallis_gwas.sh` is a SLURM submission script that calls `01 format_phenotypes.R` internally and saves the output to the folder `output`. The results summary file might look something like this
```
 # 017_kruskal-wallis-gwas

**Date:** 26th March 2021s
**Author:** Tom Ellis

## Background
The four cohorts are non-random with respect to geography and kinship.
Also, GWAS plots using a kinship matrix seem to still show inflation, which I don't have an answer for.
To check whether something funky is happening, run GWAS without a K-matrix or defining a response distribution at all.

## What did you do?
- `format_phenotypes.R` makes separate CSV files for ancestral and evolved viruses. It also creates files for the same, but removing accessions with the top necrosis hit.
- `kruskall_wallis_gwas.sh` runs GWA on these data without data transformation and without a K-matrix

## Main conclusion
- Both evolved and ancestral strains give a peak where you expect at Chr2:5923326.
- When you remove accessions with the top hit there is a suggestion that something else crops up a bit further down Chr2

## Caveats
The output of PyGWAS won't upload to GWASviewer, which is odd because they were written by the same person.

## Follow-up
Repeat GWA but condition on the major association on Chr2.</nowiki>
```

### Reports

A folder to store scientific reports.

This is intended for times when you need to synthesise several results from your results folder into a single document, such as for a progress report or to summarise things to external collaborators.
It is not the same as a manuscript.

### Presentations

A folder to store files for presentations, which will usually cover multiple results.
You would probably make a separate subfolder for each presentation.

### Manuscript

From friends in other groups you may have heard tell of the legend of a mystical dreamland where projects are "finished" and ready for publication. You know not whether this can be true, only that the road to get here has been long, and many a grey hair has accumulated atop your worried brow.

At this point it is probably worth taking time to review what you have done so far and what actually needs to go into a paper, and to [create a fresh folder]({% link _posts/2023-01-20-manuscript-folder.md %}) just to present the code and data for the manuscript. That might be a completely new folder, especially if you need to synthesise data from more than one existing project folder. If the manuscript will be based only on things in one existing project folder, then it would make sense to put it here.
