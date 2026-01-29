---
title: "University Dataset"
layout: single
permalink: /projects/university-dataset/
toc: true
toc_sticky: true
---

# University Dataset (2001-2022)
Project by Sasha Crawford and Dylan Tomza. 

## Introduction
For our project, we explored the relationships between college tuition fees, admission rates, SAT scores, control(private/public), and geographical region across the years 2001 to 2022. We were specifically curious about the how admission rates and SAT scores have changed over time, if there was a correlation between admission rates and SAT scores, and the difference between tuition in private and public institutions.

During our research, we discovered that SAT scores stayed consistent throughout most of the years then spiked until 2022 whereas admsission rates were steadily decreasing between 2001 and 2010 but increased from 2010 to 2022. In addition to this, we found that admission rates and SAT scores had a moderate linear relationship. Lastly, in order to inspect the relationships with public versus private instutions, we analyzed the differences bettwen in-state and out-of-state tuitions and observed that tuition was much lower for public institutions than that of private institutions.

Overall, the majority of these results were expected, however, we were surprised to see the spike in SAT scores as we expected them to be consistent across the board. We also expected a strong linear relationship between SAT scores and admission rates, but we only found these two variables to have a moderate linear realtionship.

## Data 
The university data is sourced from [Kaggle's U.S. University Dataset from 2001 to 2022](https://www.kaggle.com/datasets/ryusonoda/u-s-university-dataset-from-2001-to-2022?resource=download) dataset. Our dataset contains data collected from colleges regarding admission rates, in-state and out-of-state tuition, average SAT scores, whether the institution is public or private, its location, and years ranging from 2001 to 2022. The original dataset contains more than the columns we have listed, however, we did not need those columns and have omitted the data.

"These data are provided through federal reporting from institutions, data on federal financial aid, and tax information. These data provide insights into the performance of institutions that receive federal financial aid dollars, and the outcomes of the students of those institutions" ([College Scorecard Institution Data Documentation](https://collegescorecard.ed.gov/assets/InstitutionDataDocumentation.pdf)).

### Summary of Variables within the Collegedata Table
The collegedata table has 13 columns/variables and 58123 rows.  All variables are explained in this section.
Note that the table was read in from a csv, but had we created a formal SQLite database for the table, the schema would have been as follows.

**Database Schema**
```
CREATE TABLE "collegedata" (
        "unitid" INTEGER NOT NULL,
        "instnm" TEXT,
        "city" TEXT,
        "state" TEXT,
        "zip" INTEGER,
        "region" TEXT,
        "pred_deg" TEXT,
        "adm_rate" REAL,
        "sat_avg" REAL,
        "tuitionfee_in" INTEGER,
        "tuitionfee_out" INTEGER,
        "year" INTEGER NOT NULL,
        "control" TEXT,
        PRIMARY KEY("unitid", "year")
);
```

Here are the variables, their descriptions, their units, their types, and some descriptive statistics.

**Categoriacal Variables**
| Variable | Description |
|---------|-------------|
| unitid | The institution's unique id | 
| instnm | The institution's name |
| city | The name of the city that the institution is located. This column includes all U.S. states, Washington D.C., and U.S. territories (Puerto Rico, Guam, etc.) 
| state | The state/territory of the institution |
| zip | The ZIP Code of the institution |
| region | The region of U.S. that the institution is located |
| pred_deg | Predominant degree type offered by the institution |
| control | Institutional control classification (public, private nonprofit, private for-profit) |
| year | Year in which institutional data was collected |

**Quantitative Discrete Variables**
| Variable | Description |
|---------|-------------|
| tuitionfee_in | In-state tuition cost (USD) |
| tuitionfee_out | Out-of-state tuition cost (USD) |

**Quantitative Continuous Variables**
| Variable | Description |
|---------|-------------|
| adm_rate | Institutional admission rate (0–1 scale) |
| sat_avg | Average SAT score (adjusted to 1600 scale) |

## Results
When looking into this dataset, we chose to focus on SAT scores, admission rates, region, tuition, and the differences between public and private institutions. We found the region with the highest average SAT score to be the U.S. Service Schools when we expected it to be New England. We also found a sudden increase in average SAT scores among institutions in 2016 and that SAT scores seem to have a greater effect on admission rates for specifically private instutions. In addition to this, SAT scores and admission rates had a higher correlation among all institutions in 2022 than in 2001. When looking into the difference between in-state tuition for public and private institutions, we found the in-state tuition for all private institutions to be concentrated below \$20,000 in 2022 whereas in-state tuition for public institutions ranged anywhere from less than \$10,000 to greater than \$60,000. Lastly we found that Consumer Price Index (CPI) and in-state tuition have a very strong positive linear relationship for both public and private institutions, with correlation coefficients of 0.968 and 0.970 respectively.

### Admission Rates by Degree
The first thing we wanted to test was if there was any significant difference in admission rates among different predominate degrees by institution. By using a bar chart we can see the varying data for each degree.

<img width="954" height="710" alt="download" src="https://github.com/user-attachments/assets/e5a65c27-d7d5-4cf2-8ae8-d95f046402b0" />

*Figure 1: Addmision Rates by Degree Type from 2001-2022*

For the year 2022, we found that admission rates tended to be higher for institutions that offered a lower level of predominate degree. We speculate that as institutions offer a higher level of degree the acceptance is significantly more competitive, and therefore, a lower admission rate for applicaitons.

### How are SAT rates changing along with admisison rates over time?
Next, we wanted to analyze how average SAT scores and average admission rates have changed since 2001. We speculate that average SAT scores would remain consistent because the SAT is graded on a normal distribution. As for admission rates, we speculate that they will decrease over time because students are likely applying to more schools due to test optional submisisons, thus, institutions are rejecting more applications.

<img width="736" height="566" alt="download" src="https://github.com/user-attachments/assets/1e51ea69-6377-4099-a867-59f4f12e7f82" />

*Figure 2: Average Admission Rates compared to Average SAT scores from 2001-2022*

Since 2001, admission rates were steadily decreasing but this behavior reversed in the 2010s. The average admission rate in 2022 was similar to the average admission rate in 2001 despite the large decrease between 2001 and 2010. Between the years 2001 and 2010, the graph aligns with our speculation. However, overall the data does not represent what we initially surmised. We speculate that the dip in admission rates could have been influenced by an increase in the number of applications.

Average SAT scores remained consistent between 2001 and 2015 but suddenly spiked around 2016 and then again in 2021. The SAT was shortened in 2016 which we speculate could have contributed to the spike in scores around this time. In 2020, many institutions no longer required SAT submissions due to the COVID-19 pandemic, which may have contributed to colleges receiving higher SAT scores on average because students would be compelled to only submit higher SAT scores. This data does not align with our initial theory about average SAT scores.

### How does the correlation between SAT scores and admission rates differ for 2001 and 2022?
Based on the previous graph, we were curious about the relationship between SAT scores and admission rates in 2001 versus 2022. We speculate as average SAT scores increase, admission rates will decrease for both years because more selective institutions will likely require a higher test score. We will use a scatterplot to calculate the correlation between the two variables.

<img width="954" height="669" alt="download" src="https://github.com/user-attachments/assets/5f0c7f6a-7478-4eea-aef3-e407e5e207a4" />

*Figure 3: Correlation SAT vs admission rates: 2001 vs 2022*

There is a moderate negative linear relationship between average SAT scores and admission rates in 2022. The correlation coefficient is -0.44496 meaning as SAT scores increase, admission rates trend downwards. This, however, is not a perfect relationship as there are many examples of high average SAT scores but high admission rates and low average SAT scores but low admission rates. This aligns with our initial expectations for the relationship.

There is a weak negative realtionship between average SAT scores and admissions rates in 2001. The correlation coefficient is -0.3412 meaning as SAT scores incerase, admission rates decrease. This is similar behavior as in 2022 although the correlation between average SAT scores and admission rates is weaker in 2001.

### How does the correlation between SAT scores and admission rates differ between public and private institutions?
We found the correlation coefficent between SAT scores and admission rates to be stronger in 2022 than in 2001. To get a closer look at 2022, we decided to compare the correlation coefficients between SAT scores and admission rates for public and private institutions.

<img width="954" height="669" alt="download" src="https://github.com/user-attachments/assets/0fe0fc41-16fc-452f-a23f-715b0edc72bb" />

*Figure 4: Correlation differences: public vs private SAT scores and admission rates*

Private institutions have a moderate negative linear relationship between average SAT scores and admission rates. The correlation coefficient between the two variables is -0.484 meaning that as average SAT scores increase, admission rates generally decrease. This is expected as more selective institutions will be more likely to accept those with higher SAT scores, although it is not the determing factor.

Public institutionts have a weak negative linear relationship between average SAT scores and admission rates. The correlation coefficient bewtween the two variables is -0.304 meaning that as average SAT scores increase, admission rates generally decrease. This is similar behavior to private institutions but a weaker correlation. We speculate this could imply that private institutions weigh SAT scores more heavily in the admissions process than public institutions.

### How does tutition differ between private and public institutions?
We wanted to visualize the difference between private and public institutions' in-state tuition. We speculate that, on average, private institutions will have a significantly higher tuition in comparison to public institutions. This is because public institutions recieve state funding whereas private institutions do not. We will utilize multiple histograms to compare the percentage of public and private institutions in each in-state tuition bracket.

<img width="948" height="578" alt="download" src="https://github.com/user-attachments/assets/ac5b76da-a871-46b0-84b8-0adcb08a3c18" />

*Figure 5: Tuition: public vs private*

This histogram shows the distribution of colleges by in state tuition bracket. Nearly all the public institutions have an in-state tuition of less than $20,000, whereas private institutions can have in-state tuition as high as $70,000. We speculate that this may be a result of public institutions being funded by the state and private instutions only being funded by students' tuition and donations. This aligns with our initial speculation regarding the differences between in-state tuition for public and private institutions. We also found that there were two private institutions with years where in-state tuition was $0. These institutions were Webb Institute between 2001 and 2006, and in 2012, as well as Benefis Healthcare School of Radiologic Technology in 2003 and 2004. These values could however just be a result of incorrect reporting or null values so we cannot be sure these schools' tuition was actually free during these years.

We chose to use only in-state tuition for this histogram because we found both in-state and out-of-state tuition trends to be very similar and did not see any value in using both in our analysis.

### Is there a correlation between inflation and college tuition prices?
After seeing the massive difference in in-state tuition for public and private institutions we were curious if there was a correlation between tuition prices and inflation, and if there was, if there was a difference in the correlation for public and private institutions. In order to further understand the possible imapct inflation has on college tuition, we have joined our original dataset with another dataset that contains the Consumer Price Index (CPI) and information about inflation.

<img width="671" height="491" alt="download" src="https://github.com/user-attachments/assets/8f535deb-0df6-410b-9c68-c93bfca533ce" />

*Figure 6: Correlation: inflation vs tuition*

For both public and private institutions, there is a very strong positive linear relationship between CPI and average in-state tuition. The correlation coefficient for both is approximately 0.97 meaning in-state tuition generally increases when CPI does.

Although the correlation coefficient between these two variables is very similar between public and private institutions, in-state tuition seems to increase at a greater rate for private institutions compared to public institutions. Even though the correlation coefficents are very similar, the in-state tuition for public and private institutions gets further apart for higher CPI values.

## Conclusion 
In conclusion, we have identified that there are many trends to draw upon when researching college data. The usage of a bar chart we expected certificate degrees to have the highest acceptance rates at school whilst graduate degree institutions held the lowest admission rates. We speculate that the reason for this is due to the competitiveness of graduate programs.

Throughout our research on the relationships within our collegedata set, we had found that SAT scores did not remain consistent from 2001 to 2022. Instead, the data remained consistent from 2001 to 2016 then spiked at about 100 points each year until 2022. Based on our graphs, we speculated that this was due to the change of format of SAT scores -- SATs were now shorter since 2016. Futhermore, admission rates were fairly inconsistent with a steady descrease from 2001 to 2010 and an increase until 2022. It is possible that this trend is because there is higher number of students applying, and therefore, more applications to be rejected thus lowering admission rates.

Based on the trends for SAT scores and admission rates over the years, we were curious if there was a potential relationship between the two. To identify if there is a relationship, we utilized a scatterplot and found that there was a moderate linear relationship about SAT scores and admissions rates in 2022 and a weak linear relationship in 2001. The two correlated to a coefficient of about -.34 for 2001 and -.44 for 2022.

The correlation coefficients were quite different for the two years so we investigated further to see if the control of the instiution had any impact. To do this, we utilized the scatterplot for 2022 and divided between public and private institutions. We discovered there was a correlation coefficient -.48 for private institutions and a coefficient of -.30 for public institutions. This means that the relationship between admission rates and SAT scores has a stronger relationship in private institutions than that of public institutions.

Beyond that, public and private institutions are typically present in differing tuition brackets. To understand the distributions of tuition between the two, we explored a histogram of both and compared. It appeared that in-state tuition for public institutions was overall much lower than that of in-state tuition for private institutions. We speculate this is likely because private institutions recieve majority of their funding through tuition and donations whereas public institutions recieve money from not only tuitiont but the government too. In our research, we compared the private and public institutions to their out-of-state tuition and found that the results were about the same.

Lastly, the change in tuition could perhaps be impacted by the change in inflation over the years. We analyzed a scatterplot between average in-state tuition and the consumer price index. The graph presents a strong linear relationship between the two. Thus, there are a quite a variety of trends that can be drawn about college application data.

## Model Notebook 
Click the link below to run our notebook in Google Colab.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1NsTyTMA86fTWrcpy5V6pUvCdXAVWt10p?usp=sharing)
