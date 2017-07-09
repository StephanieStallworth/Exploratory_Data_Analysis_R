# Tooth Growth Inferential Analysis
Stephanie Stallworth  
March 27, 2017  



### **Executive Summary**

This inferential analysis explores the `ToothGrowth` data set using the following steps:  

1. Basic exploratory data analysis
2. Summarize the data
3. Examine the effect of supp and dose on tooth growth using confidence intervals and hypothesis tests  
4. State conclusions and assumptions

###**Step 1: Exploratory data analysis**


```r
library(ggplot2)

data(ToothGrowth)

# Examine data set stucture
str(ToothGrowth)
```

```
'data.frame':	60 obs. of  3 variables:
 $ len : num  4.2 11.5 7.3 5.8 6.4 10 11.2 11.2 5.2 7 ...
 $ supp: Factor w/ 2 levels "OJ","VC": 2 2 2 2 2 2 2 2 2 2 ...
 $ dose: num  0.5 0.5 0.5 0.5 0.5 0.5 0.5 0.5 0.5 0.5 ...
```

```r
# Determine number of observations
dim(ToothGrowth)
```

```
[1] 60  3
```

```r
# Coerce dose variable to doses
ToothGrowth$dose <- as.factor(ToothGrowth$dose)

# Examine data structure after conversion
str(ToothGrowth)
```

```
'data.frame':	60 obs. of  3 variables:
 $ len : num  4.2 11.5 7.3 5.8 6.4 10 11.2 11.2 5.2 7 ...
 $ supp: Factor w/ 2 levels "OJ","VC": 2 2 2 2 2 2 2 2 2 2 ...
 $ dose: Factor w/ 3 levels "0.5","1","2": 1 1 1 1 1 1 1 1 1 1 ...
```


###**Step 2: Summarize the data**

```r
# Summary statistics for all variables
summary(ToothGrowth)
```

```
      len        supp     dose   
 Min.   : 4.20   OJ:30   0.5:20  
 1st Qu.:13.07   VC:30   1  :20  
 Median :19.25           2  :20  
 Mean   :18.81                   
 3rd Qu.:25.27                   
 Max.   :33.90                   
```

```r
# Table of dose levels and delivery methods
table(ToothGrowth$dose, ToothGrowth$supp)
```

```
     
      OJ VC
  0.5 10 10
  1   10 10
  2   10 10
```

```r
# Exploratory plots
ggplot(ToothGrowth,aes(x = dose, y = len))+ geom_boxplot(aes(fill = dose))
```

![](Tooth_Growth_Statistical_Analysis_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
ggplot(ToothGrowth,aes(x = supp, y = len)) + geom_boxplot(aes(fill = supp))
```

![](Tooth_Growth_Statistical_Analysis_files/figure-html/unnamed-chunk-2-2.png)<!-- -->

###**Step 3: Examine the effect of supp and dose on tooth growth using confidence intervals and hypothesis tests **

A T-test was performed to check for group differences explained by supplement type.

```r
t.test(len ~ supp, data = ToothGrowth)
```

```

	Welch Two Sample t-test

data:  len by supp
t = 1.9153, df = 55.309, p-value = 0.06063
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.1710156  7.5710156
sample estimates:
mean in group OJ mean in group VC 
        20.66333         16.96333 
```
As shown above, the p value is 0.06 and the confidence interval contains 0. Thus, we can **not reject** the null hypothesis that different supplement types have no effect on tooth length.  

T-tests were then performed to determine if group differences are due to dose levels.


```r
# Subgroup does by their level pairs
ToothGrowth_Dose_0.5_1.0<-subset(ToothGrowth, dose %in% c(0.5, 1.0))
ToothGrowth_Dose_0.5_2.0<-subset(ToothGrowth, dose %in% c(0.5, 2.0))
ToothGrowth_Dose_1.0_2.0<-subset(ToothGrowth, dose %in% c(1.0, 2.0))

# Group Differences due to 0.5 to 1.0 dose levels
t.test(len ~ dose, data = ToothGrowth_Dose_0.5_1.0)
```

```

	Welch Two Sample t-test

data:  len by dose
t = -6.4766, df = 37.986, p-value = 1.268e-07
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -11.983781  -6.276219
sample estimates:
mean in group 0.5   mean in group 1 
           10.605            19.735 
```

```r
# Group Differences due to 0.5 to 2.0 dose levels
t.test(len ~ dose, data = ToothGrowth_Dose_0.5_2.0)
```

```

	Welch Two Sample t-test

data:  len by dose
t = -11.799, df = 36.883, p-value = 4.398e-14
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -18.15617 -12.83383
sample estimates:
mean in group 0.5   mean in group 2 
           10.605            26.100 
```

```r
# Group Differences due to 1.0 to 2.0 dose levels
t.test(len ~ dose, data = ToothGrowth_Dose_1.0_2.0)
```

```

	Welch Two Sample t-test

data:  len by dose
t = -4.9005, df = 37.101, p-value = 1.906e-05
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -8.996481 -3.733519
sample estimates:
mean in group 1 mean in group 2 
         19.735          26.100 
```
For all three tests, the p value is less than 0.05 and the confidence intervals does not contain zero.  Thus, we can **reject** the null hypothesis and conclude that increasing dose levels ***does*** in fact lead to an increase in tooth length.  

###**Step 4: State conclusions and assumptions**
 
Based on my analysis above my conclusions are as follows:  
1. Supplement type does not effect tooth growth  
2. Increasing dose levels does lead to increased tooth growth.  

This conclusion is based on the following assumptions:  
- The experiment was conducted using random assignment to control for confounding factors   
- The sample population is representative of the entire population  
- Variance for the t-tests are different for the two groups being compared  
