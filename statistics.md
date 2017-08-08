Statistics
===

Chi-squared test
----

[Pearson's chi-squared test](https://en.wikipedia.org/wiki/Pearson%27s_chi-squared_test) evaluates how likely it is that observed differences between sets of categorical data (what I think of as "segments") arose by chance. TODO: Fill in details.

The p-value is the probability that the sample mean difference between two compared groups would be the same or greater that the actual observed results if the null hypothesis were true. Higher p-value: More likely that the difference between groups are random.

Requirements for applicability:

- 5 or more counts per cell. 5 or more in a 2x2 table, 5 or more in 80% of cells in larger tables, but no cells with 0.
- Observations must be independent of each other. Not for paired data. Unpaired data arise from separate individuals. Thus, if you want to find out how many people like X and how many people like Y, you cannot ask one person "do you like X or Y". Instead, ask one person "do you like X" and "do you like Y"?
