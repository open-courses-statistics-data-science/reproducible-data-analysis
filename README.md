# reproducible-data-analysis
A repository holding materials for a half day reproducibility course.

# Recognising code smells
The first part of the course revolves around the concept of [code smells](https://refactoring.guru/refactoring/smells).
In it, we ask the course participants to examine the following R code snippets:

- [SIR model](https://github.com/ben18785/reproducible-data-analysis/blob/main/src/example_1.md). A refactored version is [here](https://github.com/ben18785/reproducible-data-analysis/blob/main/src/example_1_answer.md).
- [Vaccine function](https://github.com/ben18785/reproducible-data-analysis/blob/main/src/example_2.md). A refactored version is [here](https://github.com/ben18785/reproducible-data-analysis/blob/main/src/example_2.md).

The aim of this exercise is to critically evaluate this code and come up with a better way to write it.

# Reproducible data analysis
The second part of the exercises invites participants to perform a reproducible data analysis. The aim is produce an analysis of Eurovision song contest data. In case you are not familiar with Eurovision, it's an annual song contest where (European + a few other) countries put forward an entry. There are a number of [slightly random rules](https://eurovision.tv/about/how-it-works) but effectively it comes down to a "final" contest where 26 countries compete for the Eurovision crown: in the final, all countries that have taken part in the semi-finals or finals can vote. Nowadays, there is both public voting and voting by a country's jury. In this, each country gets to give its allocation of points -- 1, 2, 3, 4, 5, 6, 7, 8, 10 and 12 points -- to any of the other countries in the final. The overall winner is the country with the most votes.
