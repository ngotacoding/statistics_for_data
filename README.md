# IBM-Statistics-for-Data-Science

This is the final project for the [Statistics for Data Science Course by IBM](
https://www.coursera.org/learn/statistics-for-data-science-python) on [Coursera](https://www.coursera.org/)

## Project Overview

Statistics is an integral part in obtaining and communicating insights in Data Science. As part of a course focused on the Statistics used in Data Science, this final project was designed to evaluate the understanding of statistical concepts and their implementation in Python. The project uses Numpy, Pandas, Statsmodels and Scipy for data wrangling, whereas Matplotlib and Seaborn are used for data visualization.

The data used is the [Boston Housing Dataset](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-ST0151EN-SkillsNetwork/labs/boston_housing.csv') with 12 Features and 506 observations.

## Results of Statistical Analysis

First, the researcher was required to discern the importance of Charles River on the location of towns and the influence this had on Median Value of Houses. The researcher found out that only 35 towns did border Charles River, while 471 did not.

The researcher then utilized a T-Test to check statistical importance of bordering Charles River on the Median Value of houses. A `P-Value of 0.004`, which is lower than the required 0.05, proved that the median value of houses bordering Charles River is different from the Median Value of Houses that do not border Charles River. As such, the researcher rejected their null hypothesis.

Descritizing the age of the houses into three groups, "35 years and younger", "between 35 and 70 years" and "70 years and older", the researcher sought to answer the question on whether the differences in age groups have a statistical impact on the Median Value of houses. Utilizing an analysis of Variance(ANOVA) of the age groups yielded a p-value of `1.711e-15`, which is way lower than the required 0.05. The researcher's null hypothesis, was again rejected, as the median values of houses were found to differ depending on age of the house.
