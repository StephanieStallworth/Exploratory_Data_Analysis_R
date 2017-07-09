# Central Limit Theorem Exploratory Analysis
Stephanie Stallworth  
March 27, 2017  
###**Executive Summary**
This analysis investigates the exponential distribution in R and compare it to the Central Limit Theorem. The exponential distribution will be simulated with rexp(n, lambda) where lamda is the rate parameter and the averages of 40 exponentials will be studied.    

Analysis objectives are as follows: 

1. Show the sample mean and compare it to the theoretical mean of the distribution
2. Show how the variable sample is and compare it to the theoretical variance of the distribution  
3. Show that the distribution is approximately normal

###**Data Processing**

```r
# Load package
library(ggplot2)

# Variable set up
n<-40
lamda<-0.2
numsim<-3000
set.seed(23456)
data<-matrix(rexp(n*numsim, rate = lamda), numsim)
data_mean<-apply(data, 1, mean)

# Create histogram of the data_mean variable
hist(data_mean, col ="darkgreen")
```

![](CTL_Exploratory_Analysis_files/figure-html/unnamed-chunk-1-1.png)<!-- -->



###**Objective 1: Show the sample mean and compare it to the thoretical mean of the distribution.**


```r
theoreticalMean<-1/lamda
print(paste("Theoretical mean of the distribution =", theoreticalMean))
```

```
## [1] "Theoretical mean of the distribution = 5"
```

```r
print(paste("Actual sample mean = ", round(mean(data_mean),4)))
```

```
## [1] "Actual sample mean =  4.9975"
```

###**Objective 2: Show how the variable sample is and compare it to the theoretical variance of the distribution.**

```r
theoreticalVar<-(1/lamda)^2/n
print(paste("Theoretical Variance of the distribution = ", theoreticalVar))
```

```
## [1] "Theoretical Variance of the distribution =  0.625"
```

```r
print(paste("Actual Variance based on simulations =", round(var(data_mean),4)))
```

```
## [1] "Actual Variance based on simulations = 0.6309"
```

```r
theoreticalSd<-1/lamda/sqrt(n)
print(paste("Theoretical Standard Deviation =", round(theoreticalSd,4)))
```

```
## [1] "Theoretical Standard Deviation = 0.7906"
```

```r
print(paste("Actual Standard Deviation based on simulation =", round(sd(data_mean),4)))
```

```
## [1] "Actual Standard Deviation based on simulation = 0.7943"
```

###**Objective 3: Show that the distribution is approximately normal.**

```r
plotData <- data.frame(data_mean)
```
Then a plot was created of the results

```r
#Create Plot
m<-ggplot(plotData, aes( x= data_mean))+
    geom_histogram(aes(y = ..density..), colour = "black",fill = "goldenrod")+
    geom_density(colour = "darkgreen", size = 2)

print(m)
```

![](CTL_Exploratory_Analysis_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

###**Conclusion**
Due to the Central Limit Theorem, the data appears to be very close to a normal distribution.
