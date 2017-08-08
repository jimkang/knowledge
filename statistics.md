Statistics
===

Chi-squared test
----

[Pearson's chi-squared test](https://en.wikipedia.org/wiki/Pearson%27s_chi-squared_test) evaluates how likely it is that observed differences between sets of categorical data (what I think of as "segments") arose by chance. TODO: Fill in details.

Requirements for applicability:

- 5 or more counts per cell. 5 or more in a 2x2 table, 5 or more in 80% of cells in larger tables, but no cells with 0.
- Observations must be independent of each other. Not for paired data. Unpaired data arise from separate individuals. Thus, if you want to find out how many people like X and how many people like Y, you cannot ask one person "do you like X or Y". Instead, ask one person "do you like X" and "do you like Y"?

Interpreting results:

- A p-value <= 0.05 is commonly interpreted as justification for rejecting the null hypothesis. But 0.05 is just a probability. There is nothing magic about 0.05.
