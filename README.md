# Hopkins_BuildingDataProducts
Quantifying the Spread: Measuring Strength and Direction of Predictors with the Summary Function

**Abstract**

By extending the basic ``summary()`` funciton, we can quickly highlight top predictors, even on extremely large data sets.

The idea is not to summarize the variable in of itself, but to split the data into two sets, one for each outcome and summarize each. Comparing the results from both sets will tell you how well you predictor behaves towards your outcome 
variable. The above plots shows the summary of two predictors and their individual spreads - clearly, this first plot is a powerful predictor as the spread between the green and red line is large, 
while the second one isn't.


This demonstation uses the classic Titanic data set from the University of Colorado.
