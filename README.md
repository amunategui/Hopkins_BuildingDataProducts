# Hopkins_BuildingDataProducts
Quantifying the Spread: Measuring Strength and Direction of Predictors with the Summary Function

**Abstract**

By extending the basic ``summary()`` function, we can quickly highlight top predictors, even on extremely large data sets.

The idea is not to summarize the variable in of itself, but to split the data into two sets, one for each outcome in the classification model and summarize them. Comparing the results from both sets will tell you how well you predictor behaves towards your outcome variable. 

**Analysis**

This demonstation uses the classic Titanic data set from the University of Colorado. The five-number summary</a> displays the <b>min, max, 1st & 3rd quantile, mean, medium</b> of each variable.
<BR><BR>
Though extremely useful, this doesn't help us understand how our outcome variable interacts with its predictors. To remedy this, we split the data into two separate data sets, an outcome-positive data set, and an outcome-negative data set. Let's look at ``Sex.female``:


```r
df_survived_1 <- subset(titanicDF, Survived==1)
df_survived_0 <- subset(titanicDF, Survived==0)
summary(df_survived_1$Sex.female)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.000   0.000   1.000   0.684   1.000   1.000
```

```r
summary(df_survived_0$Sex.female)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.000   0.000   0.000   0.178   0.000   1.000
```
<BR><BR>
Now, a clearer picture emerges regarding that variable when using an outcome-specific perspective. We learn that almost 70% of those that survived were females, and that only 18% of those that died were females. I think you can see where I am going with this.
<BR><BR>
The shiny application creates a vector of summary information for both outcomes, overlaying them together and measuring the spread using the following logic:
<BR><BR>
If we generalize this spread into a single number by substracting each corresponding summary function, we are able to come up with some very telling data.


```r
spread <- ((Sex.Female_1[[1]] - Sex.Female_0[[1]]) +
             (Sex.Female_1[[2]] - Sex.Female_0[[2]]) +
             (Sex.Female_1[[3]] - Sex.Female_0[[3]]) +
             (Sex.Female_1[[4]] - Sex.Female_0[[4]]) +
             (Sex.Female_1[[5]] - Sex.Female_0[[5]]) +
             (Sex.Female_1[[6]] - Sex.Female_0[[6]]))
print(spread)
```

```
## [1] 2.506
```
<BR><BR>
<b>2.56</b> is a large spread, let's compare it with the weaker variable ``Title.Nothing``:


```r
Title.Nothing_0 <- (summary(df_survived_0$Title.Nothing))
Title.Nothing_0 <- c(Title.Nothing_0[1:6])
Title.Nothing_1 <- (summary(df_survived_1$Title.Nothing))
Title.Nothing_1 <- c(Title.Nothing_1[1:6])
stats <- data.frame('ind'=c(1:6), 'stats1'=Title.Nothing_1,'stats0'=Title.Nothing_0)
spread <- ((Title.Nothing_1[[1]] - Title.Nothing_0[[1]]) +
             (Title.Nothing_1[[2]] - Title.Nothing_0[[2]]) +
             (Title.Nothing_1[[3]] - Title.Nothing_0[[3]]) +
             (Title.Nothing_1[[4]] - Title.Nothing_0[[4]]) +
             (Title.Nothing_1[[5]] - Title.Nothing_0[[5]]) +
             (Title.Nothing_1[[6]] - Title.Nothing_0[[6]]))
print(spread)
```

```
## [1] 0.0366

Clearly, 2.506 from ``Sex.Female`` is a lot more important than 0.0366 from ``Title.Nothing``. This is exactly what the shiny application shows in a graph form that can be tweaked to remove stonger predictors to drill deep into the contribution of each variable.
