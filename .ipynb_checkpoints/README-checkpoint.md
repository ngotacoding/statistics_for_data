# IBM-Statistics-for-Data-Science

This is the final project for the [Statistics for Data Science Course by IBM](
https://www.coursera.org/learn/statistics-for-data-science-python) on [Coursera](https://www.coursera.org/)

## Project Overview

Statistics is an integral part in obtaining and communicating insights in Data Science. As part of a course focused on the Statistics used in Data Science, this final project was designed to evaluate the understanding of statistical concepts and their implementation in Python. The project uses Numpy, Pandas, Statsmodels and Scipy for data wrangling, whereas Matplotlib and Seaborn are used for data visualization.

The data used is the [Boston Housing Dataset](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-ST0151EN-SkillsNetwork/labs/boston_housing.csv') with 12 Features and 506 observations.

## Results of Statistical Analysis

From the statistical analysis, the researcher identified that most towns do not border Charles River, i.e., Only 35 towns border Charles River, 471 do not.

![Image 1](Images/Charles_River.png)

A T-Test was performed to check whether this status of bordering Charles River has statistical significance on the Median Value of houses. However, a `P-Value of 0.004`, which is lower than the required 0.05, proved that the median value of houses bordering Charles River is different from the Median Value of Houses that do not border Charles River. As such, the researcher rejected the null hypothesis.

Descritizing the age of the houses into three groups, "35 years and younger", "between 35 and 70 years" and "70 years and older", the researcher sought to identify whether the differences in age groups have a statistical impact on the Median Value of houses. An analysis of Variance(ANOVA) of the age groups yielded a p-value of `1.711e-15`, which is way lower than the required 0.05. The researcher's null hypothesis, The means for median values of houses are equal regardless of the age, was rejected as the opposite was proven true.
