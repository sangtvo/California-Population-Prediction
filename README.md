# Project 04: California Population Prediction
> The United States Census Bureau provides annual estimates of the population size of each U.S. state and region that are made publicly available. This analysis aims to predict the size of its population in the state of California up to the year 2030 by creating a linear regression analysis with R.

Table of Contents
---
1. [General Information](#general-information)
2. [Summary](#summary)
3. [Tech Stack](#tech-stack)
4. [Data Preprocessing/Cleaning](#data-preprocessingcleaning)
5. [Data Visualization](#data-visualization)
6. [Data Analysis](#data-analysis)
7. [Modeling](#modeling)
8. [Solution](#solution)
9. [Key Takeaways](#key-takeaways)
10. [References](#references)

<a name="https://github.com/sangtvo/Seattle-PD-Funding-Eligibility#general-information"/>
<a name="https://github.com/sangtvo/Seattle-PD-Funding-Eligibility#summary"/>
<a name="https://github.com/sangtvo/Seattle-PD-Funding-Eligibility#tech-stack"/>
<a name="https://github.com/sangtvo/Seattle-PD-Funding-Eligibility#data-preprocessingcleaning"/>
<a name="https://github.com/sangtvo/Seattle-PD-Funding-Eligibility#data-visualization"/>
<a name="https://github.com/sangtvo/Seattle-PD-Funding-Eligibility#data-analysis"/>
<a name="https://github.com/sangtvo/Seattle-PD-Funding-Eligibility#modeling"/>
<a name="https://github.com/sangtvo/Seattle-PD-Funding-Eligibility#solution"/>
<a name="https://github.com/sangtvo/Seattle-PD-Funding-Eligibility#key-takeaways"/>
<a name="https://github.com/sangtvo/Seattle-PD-Funding-Eligibility#references"/>

General Information
---
The project is part of a graduate course (_R for Data Analysts_) at Western Governor's University. The data is from the [US Census Bureau](https://www.census.gov/programs-surveys/popest.html).

Summary
---


Tech Stack
---
* R Studio (tidyr, reshape2, readr, ggplot2)

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


Modeling
---