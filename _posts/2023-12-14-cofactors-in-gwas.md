---
title: Including cofactors in GWAS
toc: true
---
14th December 2023

Two advantages of using plants to do genetics are that they don't run away and often have large families.
This is really useful if you want to measure phenotypes and look run a genome-wide association (GWA) analysis, because you can easily carry out proper randomised experiments with replication.

It's common to process plants in some kind of 'blocking' structure, which might be a replicate cohort, or just the tray that you grew them.
In this case individuals from the same block share a similar micro-environment and therefore cannot be considered independent.
If we ignore this non-independence we should expect to get wrong answers in subsequent analyses.
The plus side, is is straightforward to account for this to get clearer results for the things you are interested in.

However, it is not always clear how to specify discrete categories for statistical software, especially GWA packages.
This page gives an example of how to do this by specifying blocks as dummy variables.

## Example data

Here is some R code to generate an example of five samples from three experimental blocks:

```
library(tidyverse)
set.seed(27)
df <- data.frame(
  id = paste0('sample', 1:5),
  block = sample(1:3, 5, replace = TRUE)
)
```

You can see that block is expressed as an integer from one to three:

 ```
 df
       id block
1 sample1     1
2 sample2     2
3 sample3     2
4 sample4     1
5 sample5     3
```

## Blocks are not integers

`block` is a factor - it is a discrete categorical label with no meaning in itself, and the order doesn't matter.
We could just have easily have labelled blocks A, B and C, or swapped blocks 1 and 2, and the results shouldn't change.
We obviously don't want to treat it as an integer, because that would indicate something quantitative where the order definitely matters.

If you were doing something like an ANOVA in R you could specify that `block` is a factor and should be treated as such, and it knows what to do.
If you try to give block as a number to, for example, GWA packages like Limix or GEMMA, they will interpret this as an integer, and will not account for block correctly.

## Blocks as dummy variables

The correct way to specify experimental block is as a matrix of dummy variables.

Imagine a row for each sample, and a column for each block.
The column for each block will show a one for samples in that block, and a zero for samples in another block.
Since a sample can only belong to a single block, each row should contain a single one.

Here is some code to make a model matrix for the dataframe above:

```
df %>% 
  mutate(
    block1 = ifelse(block == 1, 1, 0),
    block2 = ifelse(block == 2, 1, 0),
    block3 = ifelse(block == 3, 1, 0),
    block4 = ifelse(block == 4, 1, 0),
    block5 = ifelse(block == 5, 1, 0)
  ) %>% 
  select(-block)
```

which returns
```
       id block1 block2 block3
1 sample1      1      0      0
2 sample2      0      1      0
3 sample3      0      1      0
4 sample4      1      0      0
5 sample5      0      0      1
```

## Two caveats

Here are two things to be aware of:

* Check the exact formatting requirements for the software you're using. For example, you may need to save this without the header or sample names.
* Often statistical software takes one of the states as the intercept, and defines other factor levels as a deviation from that. In this case if you include all the factor levels you may get an error about the model being unidentifiable. Depending on what software you're using you may need to drop one of the columns to get it to run.
