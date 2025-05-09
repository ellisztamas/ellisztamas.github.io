---
title: Writing README pages for research projects that don't suck
toc: true
---
21st September 2023

> Science is a game of show-and-tell, not hide-and-seek.

Richard McElreath

Research projects need to be transparent to others so folks can work out what
you've done, be they collaborators, or just future you.
An indispensible part of this is to have a clear README file in the top level of
any project folder.
However, it is rare for research groups to have any agreed guidelines on what 
information should be included, nor have I ever seen any training courses or
online resources mention this.

I have certainly written a lot of bad README files in the past, if I wrote one 
at all, which has repeatedly come back to bite me when I've needed to revisit 
what I'd done later.
That said, I do think I have learned a few things from trying to interpet my own
and others' research projects.
In this post I try to distill some of those lessons and give a template for 
how to put together a solid README file for a research project.
Since each project is different, it's hard to give hard rules, but I hope that 
this post can serve as a template you can adapt for your own work.

# What information do you need to convey?

If someone comes across your project they need to know:

1. What it is the project about?
2. What did you do?
3. What data were collected and where are they?
4. How have you processed those data and created results?
5. What information/scripts/packages do they need to reproduce this?
6. Who did what?

Construct a README file with a section addressing each of these points.
Let's go over each in turn.

# Sections of a project README

## Introduction

Give an informative title and a short overview (in one or two sentences) of what the project is about here.
You can also include links to, for example, a GitHub repository, electronic notebook entries, or a manuscript.

## Table of contents

If your project folder is shared on GitHub and the README is in markdown format (i.e. it ends in `.md`), README files will be rendered into HTML.
It is not essential, but if so you can include a [table of contents](https://thelinuxcode.com/markdown-table-contents/) to aid navigation with links to each section.
See also the example READMEs given below - they will be rendered by default on 
GitHub, but click on the README file itself on the folder overview, then on the
"Raw" button to see the raw markdown code.

## Experimental set up

Give a short overview of what you did.
This doesn't have to be exhaustive - you can link to somewhere the reader can find the details, like an electronic notebook, or other write-up.

## Data files

Give an overview of the data/data types you collected, and where to find it.
If there is a lot, consider placing one or more separate README file(s) in your data folder that goes into more detail, and mention in your main README where to find the data README.

## Dependencies

If someone is going to follow what you've done they need to know what packages they need.
At a minimum give a list of the important ones with package versions.
If you have used something like `conda`, give an `environment.yml` file in the top
level of your folder.
If you use <code>renv</code> in R see the section on [https://rstudio.github.io/renv/articles/renv.html#collaboration collaboration].

## Author information

This is often overlooked, but it is actually really useful to include information on who did what.
This makes it much easier to work out what was done if someone comes back to it later.

It also helps to include your name and the date at the top of your scripts for the same reason.

## License

If any of your could ever be shared, it is a good idea to include a license to state what/how people can use it.
See https://choosealicense.com/ for how to choose a license. If you aren't sure, use the MIT license.

# Example README templates

Here are a few examples of projects with READMEs I have written.
They differ in scale and complexity, so the READMEs do as well.

1. [A project on virus resistance in *A. thaliana*](https://github.com/ellisztamas/tumv_ms)
2. [Adaptation to soil type](https://github.com/ellisztamas/soil_adaptation_ellis_agren)
3. [Genotyping errors in bisulphite-converted sequence data](https://github.com/ellisztamas/bs_seq_with_typing_errors)
4. [Life-history trade-offs in *A. thaliana*](https://github.com/ellisztamas/fecundity_components)