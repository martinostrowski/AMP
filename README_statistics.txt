readme:Metagenome ananlyses statistics overview

hierarchy of tests

1. Functional categories 
a. COG
b. SEED

2. Second level
a. KEGG Modules
b. SEED level 2

3. 3rd level
a. KEGG KO
b. SEED level 3


4. Individual

a. COG/NOG + description
b. SEED function


Statistics software

1. Deseq - quanitfying counts, normalised within program, p-adj for FDR detection
2. STAMP, two group statistics, FMultiple test correction FDR, Bonferroni


Plotting
1. NMDS plot of gene abundance in RGC

2. DESEq produces MA plots but not suitable for gene level presentation when the number of significant genes is high

3. STAMP, Extended error bar, difference in proportion plot is best for showing functional classes and subsets

4. individual plots to show count variation (boxplot?, or correlation for continuous variables)


