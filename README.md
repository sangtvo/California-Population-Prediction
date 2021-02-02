# Project 04: California Population Prediction
> The United States Census Bureau provides annual estimates of the population size of each U.S. state and region that are made publicly available. This analysis aims to predict the size of its population in the state of California up to the year 2030 by creating a linear regression analysis with R.

Table of Contents
---
1. [General Information](#general-information)
2. [Summary](#summary)
3. [Tech Stack](#tech-stack)
4. [Data Preprocessing/Cleaning](#data-preprocessingcleaning)
6. [Data Analysis](#data-analysis)
7. [Modeling](#modeling)
8. [Solution](#solution)

<a name="https://github.com/sangtvo/California-Population-Prediction#general-information"/>
<a name="https://github.com/sangtvo/California-Population-Prediction#summary"/>
<a name="https://github.com/sangtvo/California-Population-Prediction#tech-stack"/>
<a name="https://github.com/sangtvo/California-Population-Prediction#data-preprocessingcleaning"/>
<a name="https://github.com/sangtvo/California-Population-Prediction#data-analysis"/>
<a name="https://github.com/sangtvo/California-Population-Prediction#modeling"/>
<a name="https://github.com/sangtvo/California-Population-Prediction#solution"/>

General Information
---
The project is part of a graduate course (_R for Data Analysts_) at Western Governor's University. The data is from the [US Census Bureau](https://www.census.gov/programs-surveys/popest.html).

Summary
---
The California population grows roughly between 0.0010-0.002% per year and the equation to the linear regression model is Population = 37,198,671 + 258,094(year) based on the data set. By 2030, it is expected to have 42,618,653 reported citizens in the state of California.

Tech Stack
---
* R Studio
    * tidyr
    * reshape2
    * readr
    * ggplot2

Data Preprocessing/Cleaning
---
Since the data contains many states, I only need the California observation only which is "6" as a unique identifier in the data frame. In addition, I include only the years provided in the data.
```r
ca <- raw_data[raw_data$STATE == "6", 8:17]
```

The data frame is in a wide format with each year as an individual variable. However, I want year as one variable and converted into a narrow format. To do so, a melt function is needed from the reshape2 library.

```r
df <- melt(ca, variable.name = "Year", value.name = "Population")
str(df)
```

Converting the factor variable "Year" as numeric so that it is usable in a linear regression model.
```r
df$Year <- as.numeric(df$Year)
```

Data Analysis
---
![Scatterplot](https://github.com/sangtvo/California-Population-Prediction/blob/main/images/LRmodel.PNG?raw=true)

The scatterplot shows an upward positive trend and we expect that the population of California should continue to rise over the years. It is not likely for the trend to move downward unless some disastrous/unexpected events occur such as disease outbreaks or catastrophic weather. Based on the data, it seems that the population grows roughly between 0.001 - 0.002% every year. 

Since the x axis for years is converted to numeric, it is labeled as follows:

Year | Actual Year
:-------------------------:|:-------------------------:
1 | 2010
2 | 2011
3 | 2012
4 | 2013
5 | 2014
6 | 2015
7 | 2016
8 | 2017
9 | 2018
10 | 2019
11 | 2020
12 | 2021
13 | 2022
14 | 2023
15 | 2024
16 | 2025
17 | 2026
18 | 2027
19 | 2028
20 | 2029
21 | 2030

Linear Regression
---
Creating a linear regression model with the data frame. The linear equation is Population = 37,198,671 + 258,094(year). This means that a unit change in Year will increase by 258,094 for the California population.
```r
m1 <- lm(Population ~ Year, data=df)
summary(m1)
```

```
Call:
lm(formula = Population ~ Year, data = df)

Residuals:
    Min      1Q  Median      3Q     Max 
-267392  -72351    2792  104640  170808 

Coefficients:
            Estimate Std. Error t value             Pr(>|t|)    
(Intercept) 37198671     101688  365.81 < 0.0000000000000002 ***
Year          258094      16389   15.75          0.000000264 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 148900 on 8 degrees of freedom
Multiple R-squared:  0.9688,	Adjusted R-squared:  0.9648 
F-statistic:   248 on 1 and 8 DF,  p-value: 0.000000264
```

Predicting the population size for the next 10 years based on our linear regression model.
```r
p_year <- data.frame(Year=c(11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21))
predict(m1, newdata = p_year)
```

Solution
---
Based on the data, the predictions for California population are as follows:

Year | Actual Year | Population Size
:-------------------------:|:-------------------------:|:-------------------------:
11 | 2020 | 40,037,709
12 | 2021 | 40,295,803
13 | 2022 | 40,553,898
14 | 2023 | 40,811,992 
15 | 2024 | 41,070,086 
16 | 2025 | 41,328,181 
17 | 2026 | 41,586,275 
18 | 2027 | 41,844,370 
19 | 2028 | 42,102,464 
20 | 2029 | 42,360,558 
21 | 2030 | 42,618,653 

By 2030, the predicted population for the state of California is **42,618,653** reported citizens. However, there is a flaw in the data set because there may be citizens who have not reported their status living in the state. Some reasons can include that the citizens did not receive the reminder mail, forgot to file, or choose not to despite the fine. Additionally, the data can be slightly more accurate if more years were provided by the US Census Bureau since the prediction is based on the last 10 years. 

To see the full R notebook, check out [CA_Population Prediction.rMD](https://github.com/sangtvo/California-Population-Prediction/blob/main/Code/CA_Population%20Prediction.Rmd).