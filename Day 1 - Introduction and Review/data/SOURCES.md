# Day 1 Data Sources

## penguins.csv

Body measurements of 344 penguins of three species, recorded at Palmer Station
in Antarctica between 2007 and 2009. The columns are species, island, bill
length in millimetres, bill depth in millimetres, flipper length in
millimetres, body mass in grams, and sex.

- **Source:** Horst AM, Hill AP, and Gorman KB (2020), the palmerpenguins R
  package. The copy here is the redistribution published in the seaborn sample
  data repository.
- **Original data:** Gorman KB, Williams TD, and Fraser WR (2014), Ecological
  sexual dimorphism and environmental variability within a community of
  Antarctic penguins, PLoS ONE 9(3):e90081.
- **Licence:** Creative Commons Zero, version 1.0.

## wine_quality.csv

Physicochemical measurements and sensory quality scores for red and white
variants of Portuguese Vinho Verde wine, 6497 rows in total, being 1599 red and
4898 white. The columns are eleven physicochemical measurements, a quality
score from 0 to 10, and a colour of either red or white.

- **Source:** Cortez P, Cerdeira A, Almeida F, Matos T, and Reis J (2009),
  Modeling wine preferences by data mining from physicochemical properties,
  Decision Support Systems 47(4):547 to 553. Obtained from the UCI Machine
  Learning Repository, dataset 186.
- **Licence:** Creative Commons Attribution 4.0 International, which requires
  that the citation above accompany any redistribution.

The repository publishes the red and the white wines as two semicolon-separated
files. They were concatenated into one comma-separated file, a `colour` column
was added to record which file each row came from, and spaces in the column
names were replaced with underscores. No row was altered, removed, or
reordered.
