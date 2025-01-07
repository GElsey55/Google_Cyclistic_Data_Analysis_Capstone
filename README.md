Cyclistic Case Study
================
Gregory Elsey
2025-01-07

# Introduction

This R Markdown document is the case study for the Google Data Analytics
course done through [Coursera](https://www.coursera.org/). This is the
capstone project for said course. This case study was primarily done
through R with Microsoft Excel being used briefly. If you want to work
with the rmd file for yourself, see the Prepare section for more
information on the data used for this case study.

## Scenario

You are a junior data analyst working on the marketing analyst team at
Cyclistic, a bike-share company in Chicago. The director of marketing
believes the company’s future success depends on maximizing the number
of annual memberships. Therefore, your team wants to understand how
casual riders and annual members use Cyclistic bikes differently. From
these insights, your team will design a new marketing strategy to
convert casual riders into annual members. But first, Cyclistic
executives must approve your recommendations, so they must be backed up
with compelling data insights and professional data visualizations.

### Characters and teams

● Cyclistic: A bike-share program that features more than 5,800 bicycles
and 600 docking stations. Cyclistic sets itself apart by also oering
reclining bikes, hand tricycles, and cargo bikes, making bike-share more
inclusive to people with disabilities and riders who can’t use a
standard two-wheeled bike. The majority of riders opt for traditional
bikes; about 8% of riders use the assistive options. Cyclistic users are
more likely to ride for leisure, but about 30% use the bikes to commute
to work each day.

● Lily Moreno: The director of marketing and your manager. Moreno is
responsible for the development of campaigns and initiatives to promote
the bike-share program. These may include email, social media, and other
channels.

● Cyclistic marketing analytics team: A team of data analysts who are
responsible for collecting, analyzing, and reporting data that helps
guide Cyclistic marketing strategy. You joined this team six months ago
and have been busy learning about Cyclistic’s mission and business
goals—as well as how you, as a junior data analyst, can help Cyclistic
achieve them.

● Cyclistic executive team: The notoriously detail-oriented executive
team will decide whether to approve the recommended marketing program.

### About the company

In 2016, Cyclistic launched a successful bike-share oering. Since then,
the program has grown to a eet of 5,824 bicycles that are geotracked and
locked into a network of 692 stations across Chicago. The bikes can be
unlocked from one station and returned to any other station in the
system anytime.

Until now, Cyclistic’s marketing strategy relied on building general
awareness and appealing to broad consumer segments. One approach that
helped make these things possible was the exibility of its pricing
plans: single-ride passes, full-day passes, and annual memberships.
Customers who purchase single-ride or full-day passes are referred to as
casual riders. Customers who purchase annual memberships are Cyclistic
members.

Cyclistic’s nance analysts have concluded that annual members are much
more protable than casual riders. Although the pricing exibility helps
Cyclistic aract more customers, Moreno believes that maximizing the
number of annual members will be key to future growth. Rather than
creating a marketing campaign that targets all-new customers, Moreno
believes there is a solid opportunity to convert casual riders into
members. She notes that casual riders are already aware of the Cyclistic
program and have chosen Cyclistic for their mobility needs.

Moreno has set a clear goal: Design marketing strategies aimed at
converting casual riders into annual members. In order to do that,
however, the team needs to beer understand how annual members and casual
riders dier, why casual riders would buy a membership, and how digital
media could aect their marketing tactics. Moreno and her team are
interested in analyzing the Cyclistic historical bike trip data to
identify trends.

# Google Data Analysis Process

This case study will use the Google data Analysis Process to complete
this case.

1.  Ask: Define the problem and confirm stakeholder expectations

2.  Prepare: Collect and store data for analysis

3.  Process: Clean and transform data to ensure integrity

4.  Analyse: Use data analysis tools to draw conclusions

5.  Share: Interpret and communicate results to others to make
    data-driven decisions

6.  Act: Put your insights to work in order to solve the original
    problem

# Ask

Task: Identify annual members and causal riders and analyze the
different riding habits of the two listed groups. Then, come up with
possible different ways on how to convert the casual rider to being a
member.

## Stakeholders:

Lily Moreno: The director of marketing and your manager.

Cyclistic marketing analytics team: A team of data analysts who collect,
analyze and report data that helps guide Cyclistic’s marketing strategy.

Cyclistic executive team: A detail-oriented executive team that will
decide whether to approve the marketing program you will recommend.

# Prepare

This case study uses Cyclistics public historical trip data to help
analyze and identify trends. The data is avaliable on [Motivate
International Inc.](https://divvy-tripdata.s3.amazonaws.com/index.html)
under this [license](https://divvybikes.com/data-license-agreement). If
you would like to download this case study yourself download the csvs
labeled 202312-divvy-tripdata to 202411-divvy-tripdata from the Motivate
International link to be able to work with the data for yourself.

The case study uses the csv files ranging from December 2023 to November
2024 that were contain the zip files of the Motivate International data
base. Microsoft Excel was used to make sure the data was all there. In
each of those files were 13 different variables

### Data Types Explination

The data set contains 13 different variables:

- ride_id: The id of the rideable being used
- rideable_type: The type of rideable used
- started_at: What day and time the ride began
- ended_at: What day and time the ride ended
- start_station_name: What station the ride began at
- start_station_id: The id of the starting station
- end_station_name: What station the ride ended at
- end_station_id: The id of the ending station
- start_lat: The beginning Latitude of the ride
- start_lng: The beginning Longitude of the ride
- end_lat: The ending Latitude of the ride
- end_lng: The ending Longitude of the ride
- member_casual: Whether the the rider is an annual member or a casual
  rider

# Process and Analyze

This section will contain both processing and analyzing the data, and is
where the r coding will take place.

First we must load the libraries that we will be used for this case
study.

``` r
# Load all needed libraries
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(janitor)
```

    ## 
    ## Attaching package: 'janitor'
    ## 
    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

``` r
library(lubridate)
```

Then the environment needs to be emptied in order for everything to work
properly (Note: If you are planning on downloading this markdown then
you will need to adjust this step to whatever directory you will be
using to run this code).

``` r
# Cleaning enviroment
rm(list=ls())
```

Now lets load all of the csvs and combine them into one big file for an
easier analysis!

``` r
# Csv calling and compiling into a single file
bike_rides <- list.files(path="./compiled csvs", full.names = TRUE) %>%
  lapply(read.csv) %>%
  bind_rows
```

``` r
# Head call to see combined data
head(bike_rides)
```

    ##            ride_id rideable_type          started_at            ended_at
    ## 1 C9BD54F578F57246 electric_bike 2023-12-02 18:44:01 2023-12-02 18:47:51
    ## 2 CDBD92F067FA620E electric_bike 2023-12-02 18:48:19 2023-12-02 18:54:48
    ## 3 ABC0858E52CBFC84 electric_bike 2023-12-24 01:56:32 2023-12-24 02:04:09
    ## 4 F44B6F0E8F76DC90 electric_bike 2023-12-24 10:58:12 2023-12-24 11:03:04
    ## 5 3C876413281A90DF electric_bike 2023-12-24 12:43:16 2023-12-24 12:44:57
    ## 6 28C0D6EFB81E1769 electric_bike 2023-12-24 13:59:57 2023-12-24 14:10:57
    ##   start_station_name start_station_id end_station_name end_station_id start_lat
    ## 1                                                                         41.92
    ## 2                                                                         41.92
    ## 3                                                                         41.89
    ## 4                                                                         41.95
    ## 5                                                                         41.92
    ## 6                                                                         41.91
    ##   start_lng end_lat end_lng member_casual
    ## 1    -87.66   41.92  -87.66        member
    ## 2    -87.66   41.89  -87.64        member
    ## 3    -87.62   41.90  -87.64        member
    ## 4    -87.65   41.94  -87.65        member
    ## 5    -87.64   41.93  -87.64        member
    ## 6    -87.63   41.88  -87.65        member

There’s almost 6 million objects within this data set! We need to weed
out any data that would hinder the analysis later on.

``` r
# Check to see if there are any extra pieces of data
unique(bike_rides$member_casual)
```

    ## [1] "member" "casual"

``` r
unique(bike_rides$rideable_type)
```

    ## [1] "electric_bike"    "classic_bike"     "electric_scooter"

There may be some unnecessary and null data within the data set, so lets
get rid of that.

``` r
# Getting rid of the extra data and null data
bike_rides <- drop_na(bike_rides)
```

There might also be some test data so lets make sure we aren’t missing
anything.

``` r
# Check for test cases
unique(bike_rides$start_station_name[grep("TEST", bike_rides$start_station_name)])
```

    ## character(0)

``` r
unique(bike_rides$end_station_name[grep("TEST", bike_rides$end_station_name)])
```

    ## character(0)

``` r
unique(bike_rides$start_station_name[grep("test", bike_rides$start_station_name)])
```

    ## character(0)

``` r
unique(bike_rides$end_station_name[grep("test", bike_rides$end_station_name)])
```

    ## character(0)

There doesn’t seem to be any test data, so we can go forward with
parsing the dates to make them easier to work with.

``` r
# Changing the format of started_at & ended_at to a date format
bike_rides$started_at <- lubridate::ymd_hms(bike_rides$started_at)
bike_rides$ended_at <- lubridate::ymd_hms(bike_rides$ended_at)
```

``` r
# Creating an hour column for both start and end hour
bike_rides$start_hour <- lubridate::hour(bike_rides$started_at)
bike_rides$end_hour <- lubridate::hour(bike_rides$ended_at)
```

``` r
# Parsing date from started_at and ended_at
bike_rides$start_date <- as.Date(bike_rides$started_at)
bike_rides$end_date <- as.Date(bike_rides$ended_at)
```

``` r
# Parsing month the bike was rented from started at
bike_rides$month <- format(as.Date(bike_rides$start_date), "%B")
```

``` r
# Parsing what day of the week the bike was rented
bike_rides$day_of_week <- format(as.Date(bike_rides$start_date), "%A")
```

Now lets order the Months and Days of the week to make them much easier
to work with

``` r
# Convert months order from December to November
bike_rides$month <- ordered(bike_rides$month, levels=c("December","January", "February", 
  "March", "April", "May", "June", "July", "August", "September", "October", 
  "November"))
# Convert days of week order to Sunday to Saturday
bike_rides$day_of_week <- ordered(bike_rides$day_of_week, levels=c("Sunday", 
  "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"))
```

You may have noticed that the order is from December to November and not
January to December. The reason it’s in this order is because the data
starts in December 2023, so we need to make sure that when we graph the
data we start from the earliest time frame, which happens to be in
December.

After parsing lets take a quick look at the data frame to see all of the
changes made.

``` r
# Check on data
head(bike_rides)
```

    ##            ride_id rideable_type          started_at            ended_at
    ## 1 C9BD54F578F57246 electric_bike 2023-12-02 18:44:01 2023-12-02 18:47:51
    ## 2 CDBD92F067FA620E electric_bike 2023-12-02 18:48:19 2023-12-02 18:54:48
    ## 3 ABC0858E52CBFC84 electric_bike 2023-12-24 01:56:32 2023-12-24 02:04:09
    ## 4 F44B6F0E8F76DC90 electric_bike 2023-12-24 10:58:12 2023-12-24 11:03:04
    ## 5 3C876413281A90DF electric_bike 2023-12-24 12:43:16 2023-12-24 12:44:57
    ## 6 28C0D6EFB81E1769 electric_bike 2023-12-24 13:59:57 2023-12-24 14:10:57
    ##   start_station_name start_station_id end_station_name end_station_id start_lat
    ## 1                                                                         41.92
    ## 2                                                                         41.92
    ## 3                                                                         41.89
    ## 4                                                                         41.95
    ## 5                                                                         41.92
    ## 6                                                                         41.91
    ##   start_lng end_lat end_lng member_casual start_hour end_hour start_date
    ## 1    -87.66   41.92  -87.66        member         18       18 2023-12-02
    ## 2    -87.66   41.89  -87.64        member         18       18 2023-12-02
    ## 3    -87.62   41.90  -87.64        member          1        2 2023-12-24
    ## 4    -87.65   41.94  -87.65        member         10       11 2023-12-24
    ## 5    -87.64   41.93  -87.64        member         12       12 2023-12-24
    ## 6    -87.63   41.88  -87.65        member         13       14 2023-12-24
    ##     end_date    month day_of_week
    ## 1 2023-12-02 December    Saturday
    ## 2 2023-12-02 December    Saturday
    ## 3 2023-12-24 December      Sunday
    ## 4 2023-12-24 December      Sunday
    ## 5 2023-12-24 December      Sunday
    ## 6 2023-12-24 December      Sunday

Now we should convert the ride length into a minute format for easier
calculations when we analyze the data.

``` r
# Calculate trip time into minutes
bike_rides$ride_length <- difftime(bike_rides$ended_at, bike_rides$started_at)
bike_rides$ride_length <- bike_rides$ride_length/60
bike_rides$ride_length <- round(bike_rides$ride_length, 2)
```

Now lets get a more in depth look into the changes we made.

``` r
# See all the new columns with str called
str(bike_rides)
```

    ## 'data.frame':    5898929 obs. of  20 variables:
    ##  $ ride_id           : chr  "C9BD54F578F57246" "CDBD92F067FA620E" "ABC0858E52CBFC84" "F44B6F0E8F76DC90" ...
    ##  $ rideable_type     : chr  "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
    ##  $ started_at        : POSIXct, format: "2023-12-02 18:44:01" "2023-12-02 18:48:19" ...
    ##  $ ended_at          : POSIXct, format: "2023-12-02 18:47:51" "2023-12-02 18:54:48" ...
    ##  $ start_station_name: chr  "" "" "" "" ...
    ##  $ start_station_id  : chr  "" "" "" "" ...
    ##  $ end_station_name  : chr  "" "" "" "" ...
    ##  $ end_station_id    : chr  "" "" "" "" ...
    ##  $ start_lat         : num  41.9 41.9 41.9 42 41.9 ...
    ##  $ start_lng         : num  -87.7 -87.7 -87.6 -87.7 -87.6 ...
    ##  $ end_lat           : num  41.9 41.9 41.9 41.9 41.9 ...
    ##  $ end_lng           : num  -87.7 -87.6 -87.6 -87.7 -87.6 ...
    ##  $ member_casual     : chr  "member" "member" "member" "member" ...
    ##  $ start_hour        : int  18 18 1 10 12 13 9 8 18 6 ...
    ##  $ end_hour          : int  18 18 2 11 12 14 9 8 18 6 ...
    ##  $ start_date        : Date, format: "2023-12-02" "2023-12-02" ...
    ##  $ end_date          : Date, format: "2023-12-02" "2023-12-02" ...
    ##  $ month             : Ord.factor w/ 12 levels "December"<"January"<..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ day_of_week       : Ord.factor w/ 7 levels "Sunday"<"Monday"<..: 7 7 1 1 1 1 1 1 2 1 ...
    ##  $ ride_length       : 'difftime' num  3.83 6.48 7.62 4.87 ...
    ##   ..- attr(*, "units")= chr "secs"

Looks like the conversion is successful, but now we need to do a quick
check for any ride times that lasted for 0 minutes to possibly remove
them. These pieces of data are useless, as they don’t give any insight
into the data we will be analyzing.

``` r
#remove ride times that are 0 minutes
bike_rides <- subset(bike_rides, ride_length > 0)
```

Finally, we need to convert the ride length to a numeric format to be
able to do calculations for the analysis we will be doing.

``` r
# Convert ride_length to numeric for calculations
bike_rides$ride_length <- as.numeric(as.character(bike_rides$ride_length))
bike_rides <- filter(bike_rides, ride_length > 0)
```

Now we are ready to really start taking a look at the data and analyze
it.

First lets see how many rides the casual and member riders did from
December to November.

``` r
# Begin summarizing and analyzing 
bike_rides %>% 
  group_by(member_casual) %>%
  summarise(Amount_of_rides = n())
```

    ## # A tibble: 2 × 2
    ##   member_casual Amount_of_rides
    ##   <chr>                   <int>
    ## 1 casual                2158707
    ## 2 member                3739381

It seems that there are more members riding than causal riders.Let’s now
take a look at the summaries of each groups ride length

``` r
# First we look at the general summary of the ride length
summary(bike_rides$ride_length)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    0.01    5.54    9.70   15.48   17.19 1509.37

``` r
# Then we compare the member_casual summaries
bike_rides %>%
  group_by(member_casual) %>%
  summarise(Minimum_ride_length = min(ride_length), Maximum_ride_length = max(ride_length))
```

    ## # A tibble: 2 × 3
    ##   member_casual Minimum_ride_length Maximum_ride_length
    ##   <chr>                       <dbl>               <dbl>
    ## 1 casual                       0.01               1509.
    ## 2 member                       0.01               1500.

``` r
bike_rides %>%
  group_by(member_casual) %>%
  summarise(Average_ride_length = mean(ride_length), Median_ride_length = median(ride_length))
```

    ## # A tibble: 2 × 3
    ##   member_casual Average_ride_length Median_ride_length
    ##   <chr>                       <dbl>              <dbl>
    ## 1 casual                       21.1              12   
    ## 2 member                       12.2               8.69

Now with those initial looks into the different users, lets start
getting into specifics.

``` r
# Checking amount of bike rides between Members vs Casuals
bike_rides %>%
  group_by(day_of_week, member_casual) %>%
  summarise(Amount_of_rides = n()) 
```

    ## `summarise()` has grouped output by 'day_of_week'. You can override using the
    ## `.groups` argument.

    ## # A tibble: 14 × 3
    ## # Groups:   day_of_week [7]
    ##    day_of_week member_casual Amount_of_rides
    ##    <ord>       <chr>                   <int>
    ##  1 Sunday      casual                 369935
    ##  2 Sunday      member                 418953
    ##  3 Monday      casual                 250875
    ##  4 Monday      member                 528209
    ##  5 Tuesday     casual                 231410
    ##  6 Tuesday     member                 568101
    ##  7 Wednesday   casual                 271241
    ##  8 Wednesday   member                 617738
    ##  9 Thursday    casual                 267642
    ## 10 Thursday    member                 580997
    ## 11 Friday      casual                 320123
    ## 12 Friday      member                 537955
    ## 13 Saturday    casual                 447481
    ## 14 Saturday    member                 487428

``` r
bike_rides %>% 
  group_by(month, member_casual) %>%
  summarise(Amount_of_rides = n()) 
```

    ## `summarise()` has grouped output by 'month'. You can override using the
    ## `.groups` argument.

    ## # A tibble: 24 × 3
    ## # Groups:   month [12]
    ##    month    member_casual Amount_of_rides
    ##    <ord>    <chr>                   <int>
    ##  1 December casual                  51494
    ##  2 December member                 172285
    ##  3 January  casual                  24339
    ##  4 January  member                 120149
    ##  5 February casual                  46957
    ##  6 February member                 175861
    ##  7 March    casual                  82218
    ##  8 March    member                 218967
    ##  9 April    casual                 131366
    ## 10 April    member                 282992
    ## # ℹ 14 more rows

``` r
# Checking the usage of different bike types between Member & Casual Riders
bike_rides %>%
  group_by(rideable_type) %>%
  summarise(Amount_of_rides = n())
```

    ## # A tibble: 3 × 2
    ##   rideable_type    Amount_of_rides
    ##   <chr>                      <int>
    ## 1 classic_bike             2762271
    ## 2 electric_bike            2991480
    ## 3 electric_scooter          144337

``` r
bike_rides %>%
  group_by(rideable_type, member_casual) %>%
  summarise(Amount_of_rides = n())
```

    ## `summarise()` has grouped output by 'rideable_type'. You can override using the
    ## `.groups` argument.

    ## # A tibble: 6 × 3
    ## # Groups:   rideable_type [3]
    ##   rideable_type    member_casual Amount_of_rides
    ##   <chr>            <chr>                   <int>
    ## 1 classic_bike     casual                 976298
    ## 2 classic_bike     member                1785973
    ## 3 electric_bike    casual                1097194
    ## 4 electric_bike    member                1894286
    ## 5 electric_scooter casual                  85215
    ## 6 electric_scooter member                  59122

After looking at the numbers of some of the data, let now visualize this
data for a clearer look

``` r
# Changing how the y-axis displays numbers for easier readability
options(scipen=10000)
```

First lets visualize the amount of Casual riders versus Member riders to
get a clearer understanding.

``` r
# Incorporating percentage to be shown on the pie chart
percent_bike_rides <- bike_rides %>%
  group_by(member_casual) %>%
  summarise(num_of_rides = n())
percent_bike_rides <- percent_bike_rides %>%
  mutate(percent=paste0(round(num_of_rides/sum(num_of_rides)*100,2), "%"))

# casual rider Vs member rider ride lengths pie graph
percent_bike_rides %>%
  group_by(member_casual) %>%
  ggplot(aes(x="", y = num_of_rides, fill = member_casual)) + geom_col(color = "black") +
  geom_text(aes(label = percent), position = position_stack(vjust = .5)) +
  coord_polar(theta = "y") +
  theme_void()
```

![](README_files/figure-gfm/pie%20graph-1.png)<!-- -->

Now lets look at when each group of riders go out and rent a rideable.

``` r
# casual rider vs member rider day of week popularity bar graph
bike_rides %>%
  group_by(member_casual, day_of_week) %>%
  summarise(num_of_rides = n()) %>%
  arrange(member_casual, day_of_week) %>%
  ggplot(aes(x = day_of_week, y = num_of_rides, fill = member_casual)) +
  geom_col(position = "dodge") + labs(title = "Total Number of Rides: Casual vs Member Riders by Day",
    x = "Week Day", y = "Number of Rides", fill='User Type')
```

    ## `summarise()` has grouped output by 'member_casual'. You can override using the
    ## `.groups` argument.

![](README_files/figure-gfm/bar%20graph%20day-1.png)<!-- -->

``` r
# casual rider vs member rider month popularity bar graph
bike_rides %>%
  group_by(member_casual, month) %>%
  summarise(num_of_rides = n()) %>%
  arrange(member_casual, month) %>%
  ggplot(aes(x = month, y = num_of_rides, fill = member_casual)) +
  geom_col(position = "dodge") + labs(title = "Total Number of Rides: Casual vs Member Riders by Month",
  x = "Month", y = "Number of Rides", fill='User Type') +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```

    ## `summarise()` has grouped output by 'member_casual'. You can override using the
    ## `.groups` argument.

![](README_files/figure-gfm/bar%20graph%20month-1.png)<!-- -->

We also should check on their average ride times to get a general idea
about each type of riders habits on how long they ride for.

``` r
# Average ride time per day of week calculation
avg_ride_time_daily <- bike_rides %>%
  group_by(member_casual, day_of_week) %>%
  summarise(avg_ride_time = mean(ride_length))
```

    ## `summarise()` has grouped output by 'member_casual'. You can override using the
    ## `.groups` argument.

``` r
# Average ride time per day of week calculation
avg_ride_time_daily %>%
  group_by(member_casual, day_of_week) %>%
  ggplot() + 
  geom_line(aes(x=day_of_week, y=avg_ride_time, group = member_casual, colour = member_casual)) +
  labs(title = "Average ride time: Casual vs Member Riders", colour='User type') +
  xlab("Day of Week") +
  ylab("Average Ride Time (Minutes)")
```

![](README_files/figure-gfm/line%20graph%20ride%20time%20day%20of%20week-1.png)<!-- -->

``` r
# Average ride time per month calculation monthly
avg_ride_time_monthly <- bike_rides %>%
  group_by(member_casual, month) %>%
  summarise(avg_ride_time = mean(ride_length))
```

    ## `summarise()` has grouped output by 'member_casual'. You can override using the
    ## `.groups` argument.

``` r
# Average ride time line graph montly
avg_ride_time_monthly %>%
  group_by(member_casual, month) %>%
  ggplot() + 
  geom_line(aes(x=month, y=avg_ride_time, group = member_casual, colour = member_casual)) +
  labs(title = "Average ride time: Casual vs Member Riders", colour='User type') +
  xlab("Month") +
  ylab("Average Ride Time (Minutes)") +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```

![](README_files/figure-gfm/line%20graph%20averrage%20ride%20time%20month-1.png)<!-- -->

Finally we’ll check which of the rideables are most popular between
casual and member riders.

``` r
# Comparing the popularity between rideables divided between member and casual riders.
bike_rides %>%
  group_by(rideable_type, member_casual) %>%
  summarise(num_of_rides = n()) %>%
  ggplot(aes(x = member_casual, y = num_of_rides, fill = rideable_type)) +
  geom_col(position = "dodge") + labs(title = "Total Number of Rides: Casual vs Member Riders by Rideable",
  x = "Month", y = "Number of Rides", fill='Rideable Type')
```

    ## `summarise()` has grouped output by 'rideable_type'. You can override using the
    ## `.groups` argument.

![](README_files/figure-gfm/rideable%20popularity%20bar%20graph-1.png)<!-- -->

# Share

### Observations

After taking a look at the data and some visualizations, there are some
conclusions we can make about said data.

Most users of Cyclistic’s services are already members of the program
with 63.4% of users from December 2023 to November 2024 being said
members, while only 36.6% are casual riders using Cyclistic’s services.

Casual riders were much more likely to rent a rideable on the weekend
with Saturday being the most popular day to do so with Sunday not too
far behind. Member riders were the opposite, as they are more likely to
ride during the week with Wednesday being the most popular day for them
to rent a rideable.

Both Casual and Member riders were much more likely to use a rideable
from May to October. This means that from late spring to early fall more
people were using Cyclistic’s services, with September being the most
popular month the rent for both groups.

Casual riders had a much higher overall average ride time during the
week with it spiking to almost 25 minutes on the weekend. On the other
hand, members have a much shorter average ride time, with them not even
breaking 15 minutes.

Casual Riders also had the highest average ride times between the months
of May and July. Meanwhile, Members would have their highest Average
ride times from May to August, but they were still much shorter on
average compared to casual riders.

Both Casual and Member riders prefer to use electric bikes over the 2
other options available.

### Hypothesises

Casual riders are much more likely to use Cyclistic’s services for
leisure because of them most likely riding during weekends and summer
and having an overall higher average ride time, the general peak of
outside leisure activities.

Member riders are more likely to use Cyclistic’s services for to get to
places for work/school due to them riding more often on weekdays, and
having overall shorter average ride time.

Electric bikes are the most popular rideable due to their convenience
and ability to get to places much quick and easier than traditional
bikes.

# Act

After analyzing the data provided, these are my 3 top recommendations to
help convert casual riders into becoming members:

1.  Start an advertising campaign between the months of May and
    September to help get the word out about Cyclistic. This can be done
    with an online advertising campaign through social media, and with
    fliers/posters on the stations themselves.

Late Spring to Early Fall are the most popular times to rent a bicycle,
so targeting that time frame will yield the greatest possible chance for
people wanting to use Cyclistic’s services. Also advertising online and
near the stations can bring awareness to Cyclistic’s services.

2.  Possible alongside the previously mentioned advertising campaign,
    start a program that gives a discount for becoming a member for at
    minimum 1 month to help get the casual users into Cyclistic’s
    ecosystem.

Making products and services cheaper is always more appealing to the
average customer and makes it appealing for any customer to start using
Cyclistic’s services.

3.  When buying/upgrading rideables, prioritize classic and electric
    bikes as those rideables are much more popular than electric
    scooters. Either buy/upgrade the rideables with the ratio of 2:2:1
    or 3:3:1 for electric bikes, classic bikes, and electric scooters
    respectively. The ratio that is overall better cost wise should be
    choose, but data on the cost of these processes much be collected
    and analyzed to determine the best ratio.

Riders, both members and casual, much prefer bicycles compared to
scooter, which should be taken into account when deciding to buy/upgrade
rideables.
