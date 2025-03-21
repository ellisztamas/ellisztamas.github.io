---
title: "Separate project folders from manuscripts in data analysis projects"
---
18th January 2023

Data analysis projects typically involve a lot of files for data, code and results.
This quickly turns into a mess if you don't have some kind of structure.

Guides for managing data projects ([here's an example](https://www.britishecologicalsociety.org/wp-content/uploads/2019/06/BES-Guide-Reproducible-Code-2019.pdf?utm_source=web&utm_medium=web&utm_campaign=better_science), starting on page 4) usually suggest having a clear folder structure (which you should) but usually imply that a simple structure will serve for the whole project.

However, this does not acknowledge the conflicting reality of managing a data analysis project:

1. For day-to-day project work we need a folder structure that allows for the **flexibility of trying out things that may or may not work**. This needs to be something that can evolve over time.
2. When we publish something we need to provide a clear repository documenting how we reached the conclusions we claim in the paper. This needs to be **concise and transparent** so reviewers and readers can verify what we have done.

There is a **fundamental contradiction** between these two stages of research that I have never seen discussed.
The problem is confounded by the fact that the second point is usually all you will see of someone else's work, but the first point is where we spend most of our actual time.
That creates the illusion that everyone else is writing beautiful concise code that springs forth fully formed like Venus from the sea, while your own project is a rambling mess.

A simple way to resolve this contradiction is to separate the two stages of doing research.

1. Start with a clear [project structure]({% link _posts/2023-01-19-folder-structure.md %}) which can evolve through time.
2. When it comes to write it up, create a new folder and recreate the steps needed to process the data, run the analyses and create the figures.

This way you can have the best of both worlds: a flexible project structure for day-to-day work, and a clear, concise repository for the manuscript. I have Views on both of these stages:

1. [How to structure a research project]({% link _posts/2023-01-19-folder-structure.md %})
2. [Project folders for manuscripts]({% link _posts/2023-01-20-manuscript-folder.md %})