# IBM-Statistics-for-Data-Science

## Project Overview

Statistics is an integral part in obtaining and communicating insights in Data Science. As part of a course focused on the Statistics used in Data Science, this final project is designed to evaluate the understanding of statistical concepts and their implementation in Python.

## About the dataset

The data used is the [Boston Housing Dataset](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-ST0151EN-SkillsNetwork/labs/boston_housing.csv') with 12 Features and 506 observations.

## Results of Statistical Analysis

An alpha value of 0.05 is assumed for all statistical tests.

First, it is required to discern the importance of Charles River on the location of towns, and the influence the difference in location in reference to Charles River has on Median Value of Houses. Only 35 towns border Charles River while 471 do not, signifying that most towns are located away from Charles River. A T-Test to check the statistical importance of location in reference to Charles River on the Median Value of houses results in a `P-Value of 0.004`, which is lower than the assumed alpha value. This proves that the median value of houses bordering Charles River is different from the Median Value of Houses that do not border Charles River. As such, the null hypothesis is rejected.

Categorizing the age of the houses into three groups, "35 years and younger", "between 35 and 70 years" and "70 years and older", the question on whether the differences in age groups have a statistical impact on the Median Value of houses is asked. Utilizing an analysis of Variance(ANOVA) of the age groups yields a `p-value of 1.711e-15`, which is way lower than the assumed alpha value. Thus, the null hypothesis is rejected as the median values of houses is found to differ depending on age of the house.

A hunch is made that as nitric oxide concentrations increase in a town, the proportion of non-retail business acres within the town also increases. To prove this hunch, a pearson correlation test is used. A `p-value of 7.913e-98`, lesser than the assumed alpha value, results in the rejection of the null hypothesis while proving the hunch correct. Thus, there exists a relationship between Nitric Oxide Concentrations and the proportion of non-retail business acres in towns in Boston. A correlation coefficient of 0.764 identifies this relationship as a strong positive relationship between Nitric Oxide Concentrations and the proportion of non-retail business acres in towns.

Quizzed on the impact of an additional weighted distance to the five Boston employment centers on the median value of owner occupied homes, a regression analysis is used to find an answer. A `p-value of 1.21e-08`, lesser than the assumed alpha value, results in the rejection of the null hypothesis. The p-value proves the presence of an impact of the added weighted distance to the five Boston employment centers, on the median value of owner occupied homes. From an R<sup>2</sup> value of 0.062, an R Value of 0.249 is derived, which indicates the presence of a weak positive correlation between the weighted distance to the five Boston employment centres and the median value of owner occupied homes.

## Libraries and Tools used

The project uses [Numpy](https://numpy.org/doc/stable/), [Pandas](https://pandas.pydata.org/docs/), [Statsmodels](https://www.statsmodels.org/stable/index.html) and [Scipy](https://docs.scipy.org/doc/scipy/) for data wrangling, whereas [Matplotlib](https://matplotlib.org/stable/index.html) and [Seaborn](https://seaborn.pydata.org/) are used for data visualization. [Statsmodels](https://www.statsmodels.org/stable/index.html) is used for regression analysis. [Warnings](https://docs.python.org/3/library/warnings.html) is used to filter warning messages.

### Installing the libraries

[Warnings](https://docs.python.org/3/library/warnings.html) comes in the Python Standard Library.
The other libraries are installed using the `pip install` command.

```bash
pip install numpy
pip install pandas
pip install scipy
pip install matplotlib
pip install seaborn
pip install statsmodels
```

The specific library version can be specified by adding `==<version_number>` as a suffix. Replace `<version_number>` with library version specified.
e.g., `pip install pandas==1.3.3` to specify to pip to install version 1.3.3 of pandas.

Learn more on Python Standard Library [Here](https://docs.python.org/3/library/).

## Methodology

- Import the libraries.
  
  ```python
    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    import statsmodels.api as sm
    import scipy.stats as st
    import seaborn as sns
    import warnings
  ```

### Load data to pandas dataframe

 The data is loaded into a dataframe by running the code:

  ```python
  boston_url = 'https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-ST0151EN-SkillsNetwork/labs/boston_housing.csv'
  boston_df=pd.read_csv(boston_url)
  boston_df.rename(columns = {'Unnamed: 0':"#"}, inplace = True)
  ```

`boston_df.rename(columns = {'Unnamed: 0':"#"}, inplace = True)` renames the column `"Unnamed"` as `"#"`

### T-Test of Houses bound by Charles River and Houses not Bound

#### The hypotheses

- H<sub>o</sub> : ( *µ<sub>1</sub>=µ<sub>2</sub>* ) The means of the median values of houses bordering Charles River and houses that don't border Charles River are equal.
- H<sub>a</sub> : The means of median values of houses bordering Charles River and houses that don't border Charles River are not equal.

#### The Calculation

- First, the equality of variance is determined using the levene test. The null hypothesis for the levene test is that both input samples have equal variances. In python, run the following line of code:

  ```python
  st.levene(boston_df[boston_df["CHAS"]==0]["MEDV"],
          boston_df[boston_df["CHAS"]==1]["MEDV"], center = 'mean')
  ```
  
  - where:
    - `st.levene` is the function for levene test arithmetic in scipy.stats
    - `boston_df[boston_df["CHAS"]==0]["MEDV"]` are houses not bounded by the river
    - `boston_df[boston_df["CHAS"]==1]["MEDV"]` are houses bounded by the river
    - `center = mean` sets the levene test to compare the means of the two categories
  
  - A `p-value of 0.003`, less than the `required 0.05`, means we reject the null hypothesis, and that the population variances are not equal.
  - Find more on the `scipy.stats.levene` function [HERE](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.levene.html)
  
- The following code was run to calculate the T-test.
  
  ```python
  st.ttest_ind(boston_df[boston_df["CHAS"]==0]["MEDV"],
             boston_df[boston_df["CHAS"]==1]["MEDV"], equal_var = False)
  ```
  
  - where:
    - `st.ttest_ind` is the function for t-test calculation in scipy.stats
    - `boston_df[boston_df["CHAS"]==0]["MEDV"]` are houses not bounded by the river
    - `boston_df[boston_df["CHAS"]==1]["MEDV"]` are houses bounded by the river
    - `equal_var = False` means the T-Test done is for populations with difference variances. It is set to True when the populations have equal variances.
  - A `P-Value of 0.004`, which is lower than the `required 0.05`, proved that the median value of houses bordering Charles River is different from the Median Value of Houses that do not border Charles River. The null hypothesis is rejected.
  - Find more on the `scipy.stats.ttest_ind` function [HERE](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_ind.html)
  
### Analysis of Variance(ANOVA) of Age groups

#### The hypotheses

- H<sub>o</sub> : ( *µ<sub>1</sub>=µ<sub>2</sub>=µ<sub>3</sub>* )The means for median values of houses are equal regardless of the age.
- H<sub>a</sub> : The means for median values of houses differ depending on their age.

#### The calculation

  ```python
  f_statistic, p_value = st.f_oneway(under_35, over_70, btn_35_70)
  ```
  
- where:
  - `st.f_oneway` is the function for ANOVA calculation in scipy.stats
  - `under_35, over_70, btn_35_70` are the three discrete age groups

- A `P-value of 1.711e-15`, which is lower than the `required 0.05`, proves that the the median values of houses differ depending on age of the house. The null hypothesis is rejected.
- Find more on the `scipy.stats.f_oneway` function [HERE](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.f_oneway.html)

### Pearson Correlation of Nitric oxide concentrations and proportion of non-retail business acres per town

#### The hypothesis

- H<sub>o</sub> : There is no relationship between Nitric Oxide Concentrations and the proportion of non-retail business acres in town.
- H<sub>a</sub> : There is a relationship between Nitric Oxide Concentrations and the proportion of non-retail business acres in town.

#### The calculation

```python
  coef, p_value = st.pearsonr(boston_df["NOX"], boston_df["INDUS"])
  ```
  
- where:
  - `st.pearsonr` is the function for finding the pearson correlation in scipy.stats
  - `boston_df["NOX"]` is the Nitric Oxide Concentrations data
  - `boston_df["INDUS"]` is the proportion of non-retail business acres in town

- A `P-value of 7.913e-98`, which is lower than the `required 0.05` proves the existence of a relationship between Nitric Oxide Concentrations and the proportion of non-retail business acres in towns in Boston.
- A correlation coefficient, `coef` value, of 0.764 identifies the relationship as a strong positive relationship between Nitric Oxide Concentrations and the proportion of non-retail business acres in towns.
- Find more on the `scipy.stats.pearsonr` function [HERE](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.pearsonr.html)

### Regression analysis of effect of an additional weighted distance to the five Boston employment centres on the median value of owner occupied homes (MEDV)

#### The hypothesis

- H<sub>o</sub> : There is no impact on addition of a weighted distance to the five Boston employment centres on the median value of owner occupied homes
- H<sub>a</sub> : There is an impact on addition of a weighted distance to the five Boston employment centres on the median value of owner occupied homes

#### The calculation

```python

X = boston_df["DIS"]
y = boston_df["MEDV"]

X = sm.add_constant(X)
model = sm.OLS(y,X).fit()
predictions = model.predict(X)
model.summary()
  ```
  
- where:
  - `boston_df["DIS"]` is the independent variable, Weighted Distance to the Five Boston Employment Centres.
  - `boston_df["MEDV"]` is the dependent variable, Median Value of Owner Occupied Homes.
  - `sm.add_constant(X)` is the functions in statsmodels that adds intercept to the independent variable
  - `sm.OLS` is the function to calculate Ordinary Least Squares Regression in statsmodels
  - `.fit()` calculates the linear regression function for the data based on values of the independent (X) and dependent (y) variables.
  - `.predict(X)` uses the derived regression function to predict values of y for the given values of X.
  - model.summary() prints out the summary statistics which include the P-value and R-squared values.

- A `p-value of 1.21e-08` rejects the null hypothesis, and proves the presence of an impact of the added weighted distance to the five Boston employment centers on the median value of owner occupied homes.
- An R<sup>2</sup> value of 0.062 gives an R Value of 0.249 which indicates the presence of a weak positive correlation between the weighted distance to the five Boston employment centers and the median value of owner occupied homes..
- Find more on the `sm.OLS` function [HERE](https://www.statsmodels.org/dev/generated/statsmodels.regression.linear_model.OLS.html)

## About

This is the final project for the [Statistics for Data Science Course by IBM](
https://www.coursera.org/learn/statistics-for-data-science-python) on [Coursera](https://www.coursera.org/)
