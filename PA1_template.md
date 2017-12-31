Programming assignment in Reproducible Research
===============================================

### First read the file in

    unzip("repdata_activity.zip")
    data <- read.csv("activity.csv")

### Then create a histogram of sum of steps per day

    #Calculate the values
    result <- aggregate(data$steps, by=list(data$date), sum)
    result$x <- as.numeric(as.character(unlist(result$x)))
    result <- na.omit(result)
    colnames(result) <- c("Date","Sum_steps")
    library(ggplot2)

    ## Warning: package 'ggplot2' was built under R version 3.4.3

    ggplot(result, aes(x = Date,y = Sum_steps)) + geom_bar(stat = "identity", colour = result$Date, fill = "white" ) + xlab("Date") + ylab("Steps sum count") + ggtitle("Sum of steps per day") + theme(axis.text.x = element_text(angle = 90, hjust = 1))

![](PA1_template_files/figure-markdown_strict/histo%20file-1.png)

### Then show the mean and median of steps per day

    #Calculate the mean and median
    mean(result$Sum_steps)

    ## [1] 10766.19

    median(result$Sum_steps)

    ## [1] 10765

### Next calculate the daily activity pattern

    #Calculate activity
    average <- aggregate(data$steps, by = list(data$interval), mean, na.rm = TRUE)
    colnames(average) <- c("step_interval", "steps")

    #Plot averages
    ggplot(data = average, aes(x = step_interval, y = steps)) + geom_line() + xlab("5-minute interval") + ylab("Average number of steps") + ggtitle("Daily activity pattern")

![](PA1_template_files/figure-markdown_strict/activity%20pattern-1.png)

### Find the maximal value

    maximum <- average[which.max(average$steps),]
    maximum

    ##     step_interval    steps
    ## 104           835 206.1698

### Find the total number of NAs in this data.frame

    count <- is.na(data$steps)
    table(count)

    ## count
    ## FALSE  TRUE 
    ## 15264  2304

### Fill all the missing values in this dataframe and create a new one

    #Fill missing values
    data <- read.csv("activity.csv")
    for (i in 1:nrow(data)){
        if (is.na(data$steps[i])){
            data$steps[i] <- average$steps[which(data$interval[i] == average$step_interval)]}
    }
    total_steps <- aggregate(data$steps, by = list(data$date), sum, na.rm = TRUE)
    colnames(total_steps) <- c("interval","steps")

    #Plot a histogram
    ggplot(total_steps, aes(x = interval, y = steps)) + geom_histogram(stat = "identity") + xlab("5-minute interval") + ylab("Number of steps") + theme(axis.text.x = element_text(angle = 90, hjust = 1)) + ggtitle("Total steps per day with filled data")

    ## Warning: Ignoring unknown parameters: binwidth, bins, pad

![](PA1_template_files/figure-markdown_strict/missing%20values%20fill-1.png)

### Calculated the mean and median or result

    values <- as.numeric(as.character(unlist(total_steps$steps)))
    mean(values)

    ## [1] 10766.19

    median(values)

    ## [1] 10766.19

### Show differences between weekdays and weekends

    #New factor - "weekday" and "weekend" as a new column taken from the date
    data$weekdays <- weekdays(as.Date(data$date))
    data$weekdays <- ifelse(data$weekdays %in% c("Saturday", "Sunday"),"weekend", "weekday")

    #Plot a histogram
    plotted_data <- data
    average_values <- aggregate(steps ~ interval + weekdays, data = plotted_data, mean)
    ggplot(average_values, aes(interval, steps)) + geom_line(stat= "identity", color = "blue") + facet_grid(weekdays ~ .) + xlab("5-minute interval") + ylab("Number of steps") + geom_smooth(position = "identity", method = "auto")

    ## `geom_smooth()` using method = 'loess'

![](PA1_template_files/figure-markdown_strict/weekday%20and%20weekend-1.png)
