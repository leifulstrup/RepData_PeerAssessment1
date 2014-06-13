# Reproducible Research: Peer Assessment 1
Coursera.com JHU Reproducible Research Peer Assessment 1 Project.
Submitted by Leif Ulstrup.  June 12, 2014.


## Loading and preprocessing the data
Note: This code assumes that the activity.zip data file is in the current working directory.  If not, use setwd() to change the directory to the correct location.

Unzip the compressed activity log file...

```r
zipfile <- "activity.zip"
fileThere <- (zipfile %in% dir())
if(!fileThere){stop("Error:  activity.zip missing from directory")}
unzip(zipfile)
```

Read the activity.csv file into memory...

```r
activity <- read.csv("activity.csv")
```

Convert dates into date format for calculation purposes...

```r
activity$date <- as.Date(activity$date)
```

Compute the total steps per day...

```r
dailySteps <- tapply(activity$steps, activity$date, FUN=sum)
```

Create a histogram of the total number of steps taken each day


```r
hist(dailySteps, breaks = c(0,2500,5000,7500, 10000,12500,15000,17500,20000, 22500, 25000), main = paste("Subject Anonymous Activity (Steps) from Oct-Nov 2012"), xlab = "Steps/Day", ylab = "Number of Days" , ylim = c(0,20))
```

![plot of chunk plotHistogram](figure/plotHistogram.png) 



## What is mean total number of steps taken per day?


```r
theSummary <- summary(dailySteps, na.rm=TRUE)
print(theSummary)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##      41    8840   10800   10800   13300   21200       8
```

```r
theMean <- as.numeric(theSummary["Mean"])
textMean <- paste("The Mean Number of Steps/Day :", theMean)
print(theMean)
```

```
## [1] 10800
```

```r
print(textMean)
```

```
## [1] "The Mean Number of Steps/Day : 10800"
```

```r
theMedian <- as.numeric(theSummary["Median"])
textMedian <- paste("The Median Number of Steps/Day :", theMedian)
print(theMedian)
```

```
## [1] 10800
```

```r
print(textMedian)
```

```
## [1] "The Median Number of Steps/Day : 10800"
```

## What is the average daily activity pattern?

With 5 minute sampling periods there are 12/hour * 24 hours = 288 sample periods/day (0,5,10,15,...)


```r
require(data.table)
```

```
## Loading required package: data.table
```

```r
intervalsteps <- data.frame(interval = activity$interval, steps = activity$steps)
intervalstepsdt <- data.table(intervalsteps)
dtinterval <- intervalstepsdt[, mean(steps, na.rm= TRUE), by = interval]
setnames(dtinterval, "V1", "averageSteps")
plot(dtinterval$interval, dtinterval$averageSteps, type="l", main="Mean Steps/Sampling Interval (5m) for all days from Oct-Nov 2012", xlab = "5 minute interval periods in format HourMin (0 = 12am, 1200 = 12pm)", ylab = "Steps")
```

![plot of chunk dailypattern](figure/dailypattern.png) 

```r
maxsteps <- dtinterval[dtinterval$averageSteps == max(dtinterval$averageSteps, na.rm=TRUE)]
print(maxsteps)
```

```
##    interval averageSteps
## 1:      835        206.2
```

Time interval 835 has the maximum average steps per time period with 206.1698 average steps.



```r
plot(activity$interval, activity$steps, main="All Steps/Sampling Interval (5m) for all days from Oct-Nov 2012", xlab = "5 minute interval periods in format HourMin (0 = 12am, 1200 = 12pm)", ylab = "Steps")
```

![plot of chunk plotrawsteps ](figure/plotrawsteps .png) 

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
