# reproducible-data-analysis
A repository holding materials for a half day reproducibility course. The presentation for this course is [here](https://github.com/ben18785/simulated-data/blob/main/documents/reproducible_analysis.html).

# Recognising code smells
The first part of the course revolves around the concept of [code smells](https://refactoring.guru/refactoring/smells).
In it, we ask the course participants to examine the following R code snippets:

- [SIR model](https://github.com/ben18785/reproducible-data-analysis/blob/main/src/example_1.md). A refactored version is [here](https://github.com/ben18785/reproducible-data-analysis/blob/main/src/example_1_answer.md).
- [Vaccine function](https://github.com/ben18785/reproducible-data-analysis/blob/main/src/example_2.md). A refactored version is [here](https://github.com/ben18785/reproducible-data-analysis/blob/main/src/example_2.md).

The aim of this exercise is to critically assess this code.

# Reproducible data analysis
The second part of the exercises invites participants to perform a reproducible data analysis. The aim is produce an analysis of Eurovision song contest data. In case you are not familiar with Eurovision, it's an annual song contest where (European + a few other) countries put forward an entry. There are a number of [slightly random rules](https://eurovision.tv/about/how-it-works) but effectively it comes down to a "final" contest where 26 countries compete for the Eurovision crown: in the final, all countries that have taken part in the semi-finals or finals can vote. Nowadays, there is both public voting and voting by a country's jury. In this, each country gets to give its allocation of points -- 1, 2, 3, 4, 5, 6, 7, 8, 10 and 12 points -- to any of the other countries in the final. The overall winner is the country with the most votes.

The aim of the your analysis is to determine, "Are there political / cultural allegiances in voting?".

The analysis will be restricted to:

- examining jury voting patterns
- only the finals
- only those countries present in a high proportion of competitions

The goal of the exercise isn't to produce a perfect analysis: you only have a few hours! Rather, the aim is to produce an analysis illustrated through 2-4 figures that can be reproduced and understood by others. Things that you may want to consider:

- Creating a Github repository with a navigable structure
- Avoiding any direct modification of raw data
- Creating a directed acyclic graph (perhaps using Makefiles) that shows how your analysis was produced
- Defensive coding
- Code smells

The available data are:

- [Historical Eurovision data](https://github.com/ben18785/reproducible-data-analysis/blob/main/data/eurovision_song_contest_1975_2019v3.xlsx). (Originally taken from [data world](https://data.world/datagraver/eurovision-song-contest-scores-1975-2019).)
- [Country level data](https://github.com/ben18785/reproducible-data-analysis/blob/main/data/geo_cepii.csv): including, for example, the languages spoken by countries.
- [Inter-country data](https://github.com/ben18785/reproducible-data-analysis/blob/main/data/dist_cepii.csv): includes data on relationships between countries, for example the distances between them.

Both the country level data and inter-country data are taken from the [CEPII GeoDist database](http://www.cepii.fr/pdf_pub/wp/2011/wp2011-25.pdf).

# Rebuilding presentation
(Note mainly to self.) If you want to rebuild the presentation run: `pandoc -t revealjs -s -o reproducible_analysis.html reproducible_analysis.md -V revealjs-url=reveal.js/ -V  theme=oxrse`
