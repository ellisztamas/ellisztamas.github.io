---
title: "The case for making figures from code"
toc: true
---
20th January 2024

I have strong preference that wherever possible it is wise to create figures using code rather than a graphical program like Illustrator.
Using a script has the benefit of self-documenting how you made the figure so you can others can see what you did.
It also has the advantage that it is easy to change something later if you need to revise the analysis or match a specific journal format.

Some people, including certain PIs, argue that creating figures with code is unrealistic.
Here are some criticisms, and my sour-faced counter arguments:

> Most data analysis software makes ugly figures.

It isn't difficult to create great-looking figures with modern packages like ggplot. This includes figures with subfigures - take a look at the [cowplot](https://wilkelab.org/cowplot/articles/introduction.html) or [ggpubr](https://rpkgs.datanovia.com/ggpubr/) packages.

> Getting legends right or inserting arrows or other things is incredibly time consuming.

Extensions to ggplot, like cowplot and ggpubr handle legends pretty well, and you can usually find a good solution for other visualisation challenges by googling it (here's an [example for adding arrows](https://stackoverflow.com/questions/38008863/how-to-draw-a-nice-arrow-in-ggplot2)). 
Mucking about in illustrator is also astonishingly time consuming.

> The figure I need is still to complicated to code.

If the plot you want to make is really so complicated that you can't program it, ask yourself if you really need it that complicated. Figures with 20 subfigures are a bane of modern scientific publishing.

> I’m speaking as someone who has procrastinated a lot by making Mathematica draw all kinds of things.

It is very plausible that this stuff is difficult in Mathematica, but *everything* is difficult in Mathematica.

> I’m speaking as someone who has procrastinated a lot by making Python draw all kinds of things.

Yeah alright, I'll give you that one.
I view Python as the wrong level of abstraction for making figures - it's much better at doing heavy lifting in computations than making figures.