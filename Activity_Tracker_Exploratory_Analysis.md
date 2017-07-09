# Activity Tracker Reproducible Research
Stephanie Stallworth  
April 14, 2017  



##**Data Processing**

```r
# Unzip and read file
unzip("activity.zip")
activity<-read.csv("activity.csv")

# Format dates
activity$day <- weekdays(as.Date(activity$date))
activity$DateTime<-as.POSIXct(activity$date, format = "%Y-%m-%d")

# Omit NA
tActivity <- activity[!is.na(activity$steps), ]
```


##**Analysis**

###**What is mean total number of steps taken per day?**


```r
# Calculate total number of steps taken per day
sumTable <-  aggregate(steps ~ date, tActivity,sum)
colnames(sumTable) <- c("Date","Steps")
sumTable
```

```
         Date Steps
1  2012-10-02   126
2  2012-10-03 11352
3  2012-10-04 12116
4  2012-10-05 13294
5  2012-10-06 15420
6  2012-10-07 11015
7  2012-10-09 12811
8  2012-10-10  9900
9  2012-10-11 10304
10 2012-10-12 17382
11 2012-10-13 12426
12 2012-10-14 15098
13 2012-10-15 10139
14 2012-10-16 15084
15 2012-10-17 13452
16 2012-10-18 10056
17 2012-10-19 11829
18 2012-10-20 10395
19 2012-10-21  8821
20 2012-10-22 13460
21 2012-10-23  8918
22 2012-10-24  8355
23 2012-10-25  2492
24 2012-10-26  6778
25 2012-10-27 10119
26 2012-10-28 11458
27 2012-10-29  5018
28 2012-10-30  9819
29 2012-10-31 15414
30 2012-11-02 10600
31 2012-11-03 10571
32 2012-11-05 10439
33 2012-11-06  8334
34 2012-11-07 12883
35 2012-11-08  3219
36 2012-11-11 12608
37 2012-11-12 10765
38 2012-11-13  7336
39 2012-11-15    41
40 2012-11-16  5441
41 2012-11-17 14339
42 2012-11-18 15110
43 2012-11-19  8841
44 2012-11-20  4472
45 2012-11-21 12787
46 2012-11-22 20427
47 2012-11-23 21194
48 2012-11-24 14478
49 2012-11-25 11834
50 2012-11-26 11162
51 2012-11-27 13646
52 2012-11-28 10183
53 2012-11-29  7047
```

```r
# Create histogram of total number of steps taken per day
hist(sumTable$Steps, breaks = 5, xlab = "Steps", main = "Total Steps Per Day", col = "blue")
```

![](Activity_Tracker_Reproducible_Research_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
# Calculate and report the mean and median of the total steps taken per day
as.integer(mean(sumTable$Steps))
```

```
[1] 10766
```

```r
# Calculate median of the total steps taken per day
as.integer(median(sumTable$Steps))
```

```
[1] 10765
```
###**What is the average daily activity pattern?**


```r
# Time series plot of the 5-minute intervals and the average number of steps taken, averaged across all days

interval <- aggregate(steps ~ interval, tActivity, mean)
plot(interval$interval, 
     interval$steps, 
     type = "l",
     xlab = "Interval",
     ylab = "# of Steps",
     main = "Average Number of Steps Per Day By Interval")
```

![](Activity_Tracker_Reproducible_Research_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

###**When missing value are imputed, do mean values differ from prior calculations? What is the impact of imputing missing data on the estimates of the total daily number of steps?**

There are a number of days/intervals with missing values (coded as `NA`). The presence of missing days may introduce bias into summary calculations so a strategy was devised to address this missing data.


```r
# Calculate total number of missing values in the dataset 
sum(!complete.cases(activity))
```

```
[1] 2304
```

```r
# Average number of steps per day and interval
avgTable <- aggregate(steps ~ interval + day, tActivity, mean)

# Create dataset with NAs substituted
naData <- activity[is.na(activity$steps), ]

# Merge NA with average week day interval table to impute
newData <- merge(naData, avgTable, by = c("interval","day"))
```


A new data set that is equal to the original data set was then created the missing data imputed.

```r
# Fix original data set with missing values imputed

newData2 <- newData[,c(6,4,1,2,5)]
colnames(newData2) <- c("steps","date", "interval","day","DateTime")

# Merge NA averages and non NA data together
mergeData <- rbind(tActivity,newData2)

# Create sum of steps per date to compare with step 1
sumTable2 <- aggregate(mergeData$steps ~ mergeData$date, FUN=sum)
colnames(sumTable2)<- c("Date", "Steps")
```

Summary calculations were then performed on the new data set with no missing values.


```r
# Mean of number of steps with NA imputed
as.integer(mean(sumTable2$Steps))
```

```
[1] 10821
```

```r
# Median of Steps with NA data imputed
as.integer(median(sumTable2$Steps))
```

```
[1] 11015
```

```r
# Histogram of the total number of steps taken each day with NA data imputed
hist(sumTable2$Steps, breaks = 10, col = "blue", xlab = "Daily Steps", main = "Total Steps In A Day")
hist(sumTable$Steps, breaks = 10, col = "grey", xlab = "Daily Steps", main = "Total Steps In A Day", add=T) 
legend("topleft", c("Imputed", "NA"), fill = c("blue","grey"))
```

![](Activity_Tracker_Reproducible_Research_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

###**Are there differences in activity patterns between weekdays and weekends?**


```r
# Create new factor variable with two levels indicating whether a given date is a weekday or weekend day.

mergeData$DayCategory <- ifelse(mergeData$day %in% c("Saturday", "Sunday"), "Weekend", "Weekday")

# Create panel plot containing a time series plot of the 5-minute intervals and the average number of steps taken, averaged across all weekday days or weekend days.

library(ggplot2)

intervalTable2 <- aggregate(steps ~ interval + DayCategory,mergeData,mean)
ggplot(intervalTable2,aes(x = interval, y =steps))+geom_line() + facet_grid(DayCategory~.)+
    xlab("5 minute intervals")+
    ylab("Number of Steps")
```

![](Activity_Tracker_Reproducible_Research_files/figure-html/unnamed-chunk-7-1.png)<!-- -->



