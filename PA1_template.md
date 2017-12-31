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

    #Calculate the means
    mean_steps <- aggregate(data$steps, by=list(data$date), mean)
    mean_steps <- na.omit(mean_steps)
    colnames(mean_steps) <- c("Date","Mean_steps")

    #Calculate medians (medians consider 0-s)
    data$steps <- as.numeric(as.character(unlist(data$steps)))
    median_steps <- aggregate(data$steps, by=list(data$date), median)
    colnames(median_steps) <- c("Date","Median_steps")
    median_steps <- na.omit(median_steps)

    #Bind the values to a single data frame.
    results <- cbind(mean_steps, median_steps$Median_steps)
    colnames(results) <- c("Date","Mean steps", "Median steps")

    #Show results in a table
    library(knitr)
    kable(results)

<table>
<thead>
<tr class="header">
<th></th>
<th align="left">Date</th>
<th align="right">Mean steps</th>
<th align="right">Median steps</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2</td>
<td align="left">2012-10-02</td>
<td align="right">0.4375000</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>3</td>
<td align="left">2012-10-03</td>
<td align="right">39.4166667</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>4</td>
<td align="left">2012-10-04</td>
<td align="right">42.0694444</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>5</td>
<td align="left">2012-10-05</td>
<td align="right">46.1597222</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>6</td>
<td align="left">2012-10-06</td>
<td align="right">53.5416667</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>7</td>
<td align="left">2012-10-07</td>
<td align="right">38.2465278</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>9</td>
<td align="left">2012-10-09</td>
<td align="right">44.4826389</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>10</td>
<td align="left">2012-10-10</td>
<td align="right">34.3750000</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>11</td>
<td align="left">2012-10-11</td>
<td align="right">35.7777778</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>12</td>
<td align="left">2012-10-12</td>
<td align="right">60.3541667</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>13</td>
<td align="left">2012-10-13</td>
<td align="right">43.1458333</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>14</td>
<td align="left">2012-10-14</td>
<td align="right">52.4236111</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>15</td>
<td align="left">2012-10-15</td>
<td align="right">35.2048611</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>16</td>
<td align="left">2012-10-16</td>
<td align="right">52.3750000</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>17</td>
<td align="left">2012-10-17</td>
<td align="right">46.7083333</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>18</td>
<td align="left">2012-10-18</td>
<td align="right">34.9166667</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>19</td>
<td align="left">2012-10-19</td>
<td align="right">41.0729167</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>20</td>
<td align="left">2012-10-20</td>
<td align="right">36.0937500</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>21</td>
<td align="left">2012-10-21</td>
<td align="right">30.6284722</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>22</td>
<td align="left">2012-10-22</td>
<td align="right">46.7361111</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>23</td>
<td align="left">2012-10-23</td>
<td align="right">30.9652778</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>24</td>
<td align="left">2012-10-24</td>
<td align="right">29.0104167</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>25</td>
<td align="left">2012-10-25</td>
<td align="right">8.6527778</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>26</td>
<td align="left">2012-10-26</td>
<td align="right">23.5347222</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>27</td>
<td align="left">2012-10-27</td>
<td align="right">35.1354167</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>28</td>
<td align="left">2012-10-28</td>
<td align="right">39.7847222</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>29</td>
<td align="left">2012-10-29</td>
<td align="right">17.4236111</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>30</td>
<td align="left">2012-10-30</td>
<td align="right">34.0937500</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>31</td>
<td align="left">2012-10-31</td>
<td align="right">53.5208333</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>33</td>
<td align="left">2012-11-02</td>
<td align="right">36.8055556</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>34</td>
<td align="left">2012-11-03</td>
<td align="right">36.7048611</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>36</td>
<td align="left">2012-11-05</td>
<td align="right">36.2465278</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>37</td>
<td align="left">2012-11-06</td>
<td align="right">28.9375000</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>38</td>
<td align="left">2012-11-07</td>
<td align="right">44.7326389</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>39</td>
<td align="left">2012-11-08</td>
<td align="right">11.1770833</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>42</td>
<td align="left">2012-11-11</td>
<td align="right">43.7777778</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>43</td>
<td align="left">2012-11-12</td>
<td align="right">37.3784722</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>44</td>
<td align="left">2012-11-13</td>
<td align="right">25.4722222</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>46</td>
<td align="left">2012-11-15</td>
<td align="right">0.1423611</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>47</td>
<td align="left">2012-11-16</td>
<td align="right">18.8923611</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>48</td>
<td align="left">2012-11-17</td>
<td align="right">49.7881944</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>49</td>
<td align="left">2012-11-18</td>
<td align="right">52.4652778</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>50</td>
<td align="left">2012-11-19</td>
<td align="right">30.6979167</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>51</td>
<td align="left">2012-11-20</td>
<td align="right">15.5277778</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>52</td>
<td align="left">2012-11-21</td>
<td align="right">44.3993056</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>53</td>
<td align="left">2012-11-22</td>
<td align="right">70.9270833</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>54</td>
<td align="left">2012-11-23</td>
<td align="right">73.5902778</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>55</td>
<td align="left">2012-11-24</td>
<td align="right">50.2708333</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>56</td>
<td align="left">2012-11-25</td>
<td align="right">41.0902778</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>57</td>
<td align="left">2012-11-26</td>
<td align="right">38.7569444</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>58</td>
<td align="left">2012-11-27</td>
<td align="right">47.3819444</td>
<td align="right">0</td>
</tr>
<tr class="even">
<td>59</td>
<td align="left">2012-11-28</td>
<td align="right">35.3576389</td>
<td align="right">0</td>
</tr>
<tr class="odd">
<td>60</td>
<td align="left">2012-11-29</td>
<td align="right">24.4687500</td>
<td align="right">0</td>
</tr>
</tbody>
</table>

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
