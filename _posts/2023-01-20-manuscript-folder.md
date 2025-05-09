---
title: "Project folders for manuscripts"
toc: true
---
20th January 2023

I've [previously argued]({% link _posts/2023-01-18-separate-project-folders.md %}) that it is a good idea to maintain separate folders for day-to-day project work on data analysis projects from the folders you would use to submit the same project manuscript to a journal.

This post contains some opinionated suggestions about how to do the second of these.
See [this post]({% link _posts/2023-01-19-folder-structure.md %}) for my thoughts on how to structure a folder for day-to-day work.

## Make a manuscript folder

I'm assuming you have been working on a project and worked out what you want to say in a paper.
Once you're ready to turn your project into a manuscript, the most obvious place to put the folder would be the [in the main project folder]({% link _posts/2023-01-19-folder-structure.md %}) you already have.
If its more appropriate you could also create a separate folder somewhere else, especially if the paper covers material from multiple project folders.
You probably want to create a clean Git repository inside your manuscript folder.

The best way to structure the folder again depends on the paper itself, but here is a general template:

```
01_data
02_library
03_analysis
04_manuscript
README.md
environment.yml
LICENSE
```

This looks a like a simplified structure for a project folder.
It is numbered in the order you (and a reader) would deal with them, and it the names clearly tell you what to expect in each folder.

* The `01_data` and `01_library` folders are much the same as for a main project folder.
* The `03_analysis` folder is where you would put the scripts to run the analysis. You could split this into directories for data processing and generating results if that is more appropriate.
* `04_manuscript` is for files relating to the manuscript itself. This might include
    * A `tex` or `docx` file for the manuscript itself.
    * A `bib` file for the references.
    * A `fig` folder for figures.
    * Cover letters, supplementary information, or any other files you might need to submit to a journal.

There are some additional files in the top level of the folder:

* A `README.md` file that explains what the folder contains and how to use it. This is especially important if this will end up on GitHub because it is the first thing readers will see, and will use this to navigate the folder, so make sure this is [well-written]({% link _posts/2023-09-21-readme-files.md %}).
* An `environment.yml` file that lists the software dependencies for the project if you rely on conda. If you're using a different tool for this, there may be something equivalent.
* A `LICENSE` file if you want to make the code available to others.

## Figures

First, I would encourage you to [create your figures with code]({% link _posts/2024-01-20-figures-from-code.md %}) because this means its easy to track changes and make edits later.

Aside from that, where to output figures probably the aspect of this which most depends on the specifics of the project.
Here are some options:

* If you're results are such that you roughly have one figure for each analysis, it probably makes sense to keep the analysis and figure code together. On the other hand, if figures summarise multiple analyses it might make sense to have a separate directory for figures.
* Code to create figures could output to the same directory as the script. Since code and output are together, it is easy to see how the figure was made.
* You could also have code in one directory and have it output to the manuscripts directory. That has the advantage of making latex documents compile more smoothly, especially if they need to be rendered on some journal's website.

Do what works best for you here.

## Make sure people can run your code

This is important, but harder than you might think. It boils down to making sure people can get the data, and making sure people can run the code.

### Where should the data go?

If the data is fairly small (for example, can be contained in CSV files), you might get away with committing the data files to the code repo.

Large files need to go into a separate public repository.
In the main README file you can tell people where to find the data and how to download them.
For example, if you have used the data from the 1001 Genomes project, you could include something like this:

> For genome-wide associations we use the SNP matrix and kinship matrix associated with the [1001 Genomes project](https://1001genomes.org/). Download and extract them to `01_data/1001_SNP_MATRIX` by running the following command from the folder root:

```
wget -c https://1001genomes.org/data/GMI-MPI/releases/v3.1/SNP_matrix_imputed_hdf5/1001_SNP_MATRIX.tar.gz -O - | tar -xz -C 01_data/
```

> PyGWAS requires specific file names for the input files which don't match the default names from this link. Rename the SNP matrix with:

```
mv 01_data/1001_SNP_MATRIX/imputed_snps_binary.hdf5 01_data/1001_SNP_MATRIX/all_chromosomes_binary.hdf5
```

### Reproducibility

It is surprisingly difficult to get code to run to different machines because package versions vary.

For general packages, especially anything involving Python, give a conda environment file and tell people how to install it.
For RStudio, you can use [renv](https://rstudio.github.io/renv/articles/renv.html).

Two caveats here:

1. Conda is a pet hate of mine, and a great way to lose a whole afternoon fixing a dependency conflict that didn't need to happen.
2. This field is changing rapidly, and by the time you read this `conda` and `renv` could well be out-of-date.


## Make it available on GitHub and Zenodo

A scientific publication is meant to be a brick in the wall of human knowledge, and should be permanent.
We recognise that data is part of that and needs to be stored somewhere permanent on a long-term public database.
Code is also part of that and also needs to be shared on a long-term public database.

### Start with GitHub

Usually, people commit the code to a Git repository and upload to a public repository on GitHub, then give a link to the GitHub page. This is a good first step, but it is not really enough, for two reasons:

1. GitHub is not a long-term public repository. It is a private company who could be sold or go out of business at any time.
2. GitHub is meant for tracking changes for code that evolves, but drafts of manuscripts are static. As such, if you update the repo it is easy for the code to diverge to whatever link you put in a manuscript in ways that might not be transparent to the reader.

As such, GitHub is not really a robust solution on its own.

### Push to Zenodo

Zenodo is a proper long-term public repository for storing code. Once your code is on GitHub it is easy to push it to Zenodo and get a proper DOI you can include in your paper.

1. Create and account at [www.zenodo.org www.zenodo.org] and tell it to link to your GitHub account.
2. On the Zenodo website, click on your user name in the top right and go to 'GitHub'. You will see a list of your GitHub repos. Find the one for your manuscript and click to turn it on.
3. Once your manuscript is in a state to submit, create a [release](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases). This is a way of taking a snapshot of the repository and giving it a label, in the same way that software comes in versions labelled 1.0, 1.1, 2.0 etc.
4. The release should appear in the Github page of Zenodo, along with a DOI. Note that this will only work if you *first* allow access to the repo, *then* create the release.
5. In your manuscript, give a link to Zenodo link. It doesn't hurt to also add a link to the Github page. Write something like "Code to recreate the analyses and figures are available from `<link to Zenodo>` and `<link to GitHub>`.
6. When you need to update the code and manuscript, create a new release in GitHub, which will spawn a new DOI in Zenodo. Update your manuscript accordingly.
