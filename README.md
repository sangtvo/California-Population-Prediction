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

**To expand the project even further as a business use case, how can the police department increase the chances of their eligibility for funding if not eligible?**

Summary
---


Tech Stack
---
* R Studio (tidyr, reshape2, readr, ggplot2)

Data Preprocessing/Cleaning
---
Since the data contains many states, I only need to look at the California observation only which is 6 as a unique identifier. 
```r
ca <- raw_data[raw_data$STATE == "6", 8:17]
```

Data Visualization
---
![Districts](https://github.com/sangtvo/Seattle-PD-Funding-Eligibility/blob/main/images/Districts.png?raw=true)
![AvgNumPerEvent](https://github.com/sangtvo/Seattle-PD-Funding-Eligibility/blob/main/images/Average%20Number%20of%20Officers%20Per%20Event.png?raw=true)
![AvgNumPerZone](https://github.com/sangtvo/Seattle-PD-Funding-Eligibility/blob/main/images/Average%20Number%20of%20Officers%20Per%20Zone.png?raw=true)
![NumofIncidentsbyDate](https://github.com/sangtvo/Seattle-PD-Funding-Eligibility/blob/main/images/Number%20of%20Incidents%20by%20Date.png?raw=true)
![NumofIncidentsbyDistrict](https://github.com/sangtvo/Seattle-PD-Funding-Eligibility/blob/main/images/Num%20of%20Incidents%20by%20District.png?raw=true)
![NumofIncidentsByEventType](https://github.com/sangtvo/Seattle-PD-Funding-Eligibility/blob/main/images/Num%20of%20Incidents%20by%20Event.png?raw=true)

Data Analysis
---
* The data is dated from March 26, 2016 to March 28, 2016 which happens to be a holiday weekend, Easter Sunday. By looking at the number of events per day, one will notice that there is a high level of activity on March 27, 2016, the day before Easter Sunday. This high volume of activity shows that there are many active people on the streets or at home, possibly preparing for family gatherings which can include non- resident family members traveling to Seattle. Such events can include Easter hunts, attending mass at a cathedral, or enjoying an Easter brunch during this time. With an increase amount of people and activity in the area, it is more likely that more incidents will be reported than any other weekend.
* The top 3 incidents are disturbances, traffic related calls, and suspicious circumstances. It is highly likely that these incidents occur due to congested traffic and overflowing of family gatherings. As Seattle is becoming a booming city in the tech hub world, companies are expanding their headquarters and bringing talented employees across the globe. In turn, homelessness is increasing due to unlivable wages and high rental/home costs (Balk 2019).
* The largest number of events that has occurred is in sector H. As a quick sample test, googling the coordinates (47.600876, -122.33027) which is classified as a disturbance event, shows that this incident was located in the heart of downtown Seattle, Pioneer Square specifically. Due to the fact that downtown is a buzzing city with an immense amount of people, it would make sense that crimes are reported more often in this zone.

Modeling
---