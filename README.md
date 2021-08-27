# District Spending and Reading Achievement Analysis
Measuring the impact of various funding sources on the reading proficiency of American students. 

By Alexis Kedo

## Summary 
How sure can we be that, when we're increasing various levels of annual funding to a school district, we're having an actual impact on reading achievement for that year? This analysis used a several different types of classification methods in an attempt to isolate which variables were able to predict accurately if a district's reading achievement level is 50% or higher. 

## Data 
The dataset came from Roy Gerrard's [U.S. Educational Finances](https://www.kaggle.com/noriuk/us-educational-finances) dataset on Kaggle and the [U.S. Department of Education's EdFacts 2018-2019 reading achievement](https://www2.ed.gov/about/inits/ed/edfacts/index.html) dataset. The final, cleaned dataset contained over 11,000 individual datapoints on unique school districts in the all 50 states.  

District achievement data was normally distributed, with the majority of districts reporting reading achievement at or around 50%. 

![reading] (https://github.com/alexiskedo/School-District-Analysis/blob/main/graphs/District%20Averages.png)

Eventually, the model was iterated evolved to include the following features: 
- TOTALREV = Total Revenue (raw number) - combo of Federal, State, and Local Revenue
- TFEDREV = Federal Revenue (raw number)
- FEDRCOMP = Compensatory (Title 1) Revenue
- TSTREV = State Revenue (raw number)
- TLOCREV = Local Revenue (raw number) 
- LOCRPROP = Property Taxes (Raw number)
- PCTTOTAL = Percentage of elementary-secondary revenue over total 
- PCTFTOT = Federal:Overall Revenue (percentage) - how much of an LEA's total revenue is comprised of money from Federal Sources
- PCTSTOT = State:Overall Revenue (percentage) - how much of a district's total revenue is comprised of money from state sources
- PCTLTOT = Local:Overall Revenue (percentage) how much of a district's total revenue is comprised of money from local sources 
- PCTLTAXP = taxes and parent government contributions (percentage)
- TCURSPND = Total current spending for elementary-secondary programs (Includes spending for instruction, student support services, and other (food services, enterprise operations). Does not include capital outlay expenditures (construction, land purchase, instructional equipment, state payments for captial outlay, payments to state, local governments or other school systems, and/or interest on school system debt). 
- TCURINST = Total current spending for instruction (raw number) 
- PPCSTOT = per pupil - total current spending (raw number)
- PPSALWG - per pupuil - total salaries and wages (raw number)
- PPITOTAL = per pupil - current total spending for instruction (raw number)
- PPISALWG - per pupil - salaries and wages for instruction (raw number)

## Methods 
Precision was used as an evaluation metric, as we wanted to minimize the number of low-performing districts that would be mistakenly labeled by our model as high-performing. 

A very simple majority class prediciton, logistic regression, K-nearest neighbors, random forest, and AdaBoost were all techniques that were used to arrive at our most accurate model (70% precision). 

## Results 
Our best-performing model received a precision score of 70%, which was an improvement on our baseline model-less prediciton of 51%. However, this score was dependent on the inclusion of variables that were less relevant for my client. 

![matrix](https://github.com/alexiskedo/School-District-Analysis/blob/main/graphs/Screen%20Shot%202021-08-27%20at%208.34.10%20AM.png)

## Evaluation 
As could be expected, the accuracy score of our model improved after we increased the number of features. However, I was initially hesitant to do this, because, as my initial business question stated, I wanted to pinpoint how different levels in state, local, and federal funding specifically impact reading achievement. In order to make my model more accurate (as well as mitigate multicollinearity, in the case of my non-ensemble models), I had to introduce new, different kinds of variables that I initially was trying to exclude (the impact of property taxes, for example). As the Department has no control over these kinds of variables, the inclusion of these makes my model less helpful to the client.

There are several things I could do to improve my model going forward. For one, virtually my entire dataset consisted of financial data. We all know several non-monetary factors (class size, student:teacher ratios, teachers' years of experience) that have an outsize, though debated, impact on learning. Adding these factors into my model might allow us to eliminate some of the extraneous variables I mentioned above, while still maintaining accuracy. I also think converting all variables that are expressed in raw dollar amounts into per-pupil ratios would be helpful to eliminating some noise (as it's not really how much a district spends, but how much they expend per student that is telling). Lastly, both funding and achievement impacts compound over time. Although classification models don't work well for time-series data, there might be away to combine several years' worth of financial and assessment data so that longitudinal trends can be more accurately captured.

## Repository Structure
```
├── graphs
├── District_Spending_and_Achievement.ipynb
├── functions.py
└── README.md
├── School District Spending Analysis.pdf

```
