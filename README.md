# Association Rule Mining on Adult Census Income Dataset

This repository contains the implementation of a Data Mining Assignment, focusing on Association Rule Mining using the FP-Growth algorithm. The project involves comprehensive data exploration, preprocessing of the Adult Census Income dataset, and a from-scratch implementation of the FP-Growth algorithm to discover frequent itemsets and generate association rules.
The goal of this project is to mine association rules from the Adult Census Income dataset. Since the dataset contains a mix of numerical and categorical attributes, significant preprocessing is required to transform the data into a binary format suitable for frequent pattern mining. The core algorithm (FP-Growth) is implemented from scratch using only standard Python libraries and pandas, adhering to specific assignment constraints.

## Dataset
Adult Census Income Dataset, UCI Machine Learning Repository (Becker and Kohavi, 1996).


Description: Demographic information extracted from the 1994 US Census database.


Target: Predict whether an individual's income exceeds $50,000/year (used here for association analysis).


## Project Structure
```
.
├── data/
│   └── adult.csv                 # Original dataset
├── dist/
│   ├── adult_preprocessed.csv    # Preprocessed binary dataset
│   ├── freq_itemsets.txt         # Discovered frequent itemsets
│   └── rules.txt                 # Generated association rules
├── src/
│   ├── explore.py                # Data exploration script (notebook version provided)
│   ├── preprocess.py             # Preprocessing script (notebook version provided)
│   └── association_analysis.py   # FP-Growth implementation (notebook version provided)
├── README.md
```

## Methodology

1. Data Exploration
+ dentified numerical vs. categorical attributes.
+ Analyzed unique value counts per attribute.
+ Detected missing values (encoded as ? in categorical columns).
+ Calculated demographic statistics (e.g., percentage of US natives).

2. Preprocessing
To prepare the data for FP-Growth, the following transformations were applied:
+ Missing Value Imputation: Missing values in categorical attributes (workclass, occupation, native-country) were filled with the mode of the respective column.
+ Merging Infrequent Categories: Countries appearing fewer than 40 times were merged into a single category labeled 'Others'.
+ Categorical Binarization: One-Hot Encoding was applied to all categorical attributes (e.g., workclass=Private, education=Bachelors).
+ Continuous Attribute Discretization & Binarization:
	+ age: Equal Frequency Binning (12 intervals).
	+ education-num: Equal Width Binning (8 intervals).
	+ capital-gain: Custom Split Points (2000, 5700, 11500, 21500, 64000).
	+ capital-loss: Custom Split Points (900, 2000, 3100).
	+ hours-per-week: Equal Width Binning (5 intervals).
+ Attribute Removal: The fnlwgt attribute was removed to reduce complexity.
+ Final Feature Count: 120 binary attributes.

3. FP-Growth Implementation
The FP-Growth algorithm was implemented from scratch without using external mining libraries (e.g., mlxtend).
+ FP-Tree Construction:
	1. Scan dataset to find frequent items (min_support_count = 13,000).
	2. Sort items by descending support count.
	3. Build the FP-Tree by inserting transactions.
+ Pattern Mining:
	1. Extract conditional pattern bases for each frequent item.
	2. Construct conditional FP-Trees recursively.
	3. Generate frequent itemsets.
+ Rule Generation:
	+ Generated rules from frequent itemsets with a minimum confidence of 95%.
	+ Format: (Antecedent) -> (Consequent)


## Refrences
1. R. K. Barry Becker, Adult, UCI Machine Learning Repository, 1996. DOI: 10.24432/C5XW20
2. P.-N. Tan, M. Steinbach, and V. Kumar, Introduction to Data Mining (Always Learning), New International Edition. Harlow: Pearson, 2014, 732 pp. ISBN: 9781292026152
3. J. Han, Data Mining: Concepts and Techniques (Morgan Kaufmann Series in Data Management Systems), 3rd ed., M. Kamber and J. Pei, Eds. Waltham, MA: Morgan Kaufmann/Elsevier, 2012, 1703 pp. ISBN: 9780123814791
4. J. Han, J. Pei, and Y. Yin, "Mining frequent patterns without candidate generation," ACM SIGMOD Record, vol. 29, no. 2, pp. 1–12, May 2000. ISSN: 0163-5808. DOI: 10.1145/335191.335372