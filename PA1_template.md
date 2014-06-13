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


## What is mean total number of steps taken per day?



## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
