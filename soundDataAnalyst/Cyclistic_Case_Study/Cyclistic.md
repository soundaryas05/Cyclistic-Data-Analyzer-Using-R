---
title: 'Cyclistic Bike Share : Case Study using R'
output:
  html_document:
    df_print: paged
    keep_md: true
  pdf_document: default
---

# Introduction

This is a capstone project as a part of my Google Data Analytics Professional Certificate course. For the analysis I will be using R programming language and RStudio IDE as it can handle large amount of data and also for it's easy statistical analysis tools and data visualizations.

## Scenario 

You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company's future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.

## Objective

How do annual members and casual riders use Cyclistic bikes differently?  To Design marketing strategies aimed at converting casual riders into annual members.

## Key Stakeholders

-   Cyclistic executive team
-   My manager, Lily Moreno
-   Director of marketing
-   The rest of the marketing analytics team

## Data Analysis Steps followed in this project

-   Ask
-   Prepare
-   Process
-   Analyze
-   Share
-   Act

Each phase is approached with the help of a roadmap that has checklist of guiding questions and key tasks (which require code to complete) and deliverables.

## Ask

Three questions will guide the future marketing program: 1. How do annual members and casual riders use Cyclistic bikes differently? 2. Why would casual riders buy Cyclistic annual memberships? 3. How can Cyclistic use digital media to influence casual riders to become members?

Moreno has assigned you the first question to answer: How do annual members and casual riders use Cyclistic bikes differently?

### Key Tasks

1.  Identify the business task

-   The main objective is to build the best marketing strategies to turn casual bike riders into annual members by analyzing how the 'Casual' and 'Annual' customers use Cyclistic bike share differently.

2.  Consider key stakeholders

-   Cyclistic executive team, Director of Marketing (Lily Moreno), Marketing Analytics team.

### Deliverable

1.A clear statement of the business task

-   How do casual and annual riders use Cyclistic bike differently?

## Prepare

I will use Cyclistic's historical trip data to analyze and identify trends. The data has been made available by Motivate International Inc. under this [license](https://ride.divvybikes.com/data-license-agreement). Datasets are avilable [here](https://divvy-tripdata.s3.amazonaws.com/index.html).

### Key Tasks

1.Download data and store it appropriately.

-   Data has been downloaded from [here](https://divvy-tripdata.s3.amazonaws.com/index.html) and copies have been stored securely on my computer

2.  Identify how it's organized.

-   All data is in comma-delimited (.CSV) format. Column names "ride_id", "rideable_type", "started_at", "ended_at", "start_station_name", "start_station_id", "end_station_name", "end_station_id", "start_lat", "start_lng", "end_lat", "end_lng", "member_casual" Total number of columns is 13.

3.Sort and filter the data

-   I have downloaded previous 12 months data. I have used May 2022 to Dec 2022 and Jan 2023 to April 2023.

4.Determine the credibility of the data

-   The data was gathered firsthand by the company on all its users. The data is reliable, organized, comprehensive, current and frequently updated, and cited under an open license.

5.Data Integrity

-   Datasets are given in rows and column names are uniquely identified with consistent entries in each field.

6.Data's Relevance to the Problem

-   Membership types, trip duration, Bookig station information, location data will be helpful in gaining insights for the business problem.

7.Problems with the Data

*blank or null values, Due to non-availability of Personal identificaiton details like address, credit card some information regarding the pass purchase won't be able to find.

### Deliverable

-   The data has been made available by Motivate International Inc. under this [license](https://ride.divvybikes.com/data-license-agreement). Datasets are avilable [here](https://divvy-tripdata.s3.amazonaws.com/index.html).

#### Collecting and combining all the data into a single data frame named tripdata_combined






```r
#install and load necessary packages
install.packages("tidyverse", repos = "http://cran.us.r-project.org")
```

```
## 
## The downloaded binary packages are in
## 	/var/folders/45/39m9mn_90czb8cqgm8rvnpm00000gn/T//RtmpK6O3BJ/downloaded_packages
```


```r
#tidyverse assists with data import, tidying, manipulation, and data visualization
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.2     ✔ readr     2.1.4
## ✔ forcats   1.0.0     ✔ stringr   1.5.0
## ✔ ggplot2   3.4.2     ✔ tibble    3.2.1
## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
## ✔ purrr     1.0.1     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```


```r
#janitor has simple functions for examining and cleaning dirty data
install.packages("janitor", repos = "http://cran.us.r-project.org")
```

```
## 
## The downloaded binary packages are in
## 	/var/folders/45/39m9mn_90czb8cqgm8rvnpm00000gn/T//RtmpK6O3BJ/downloaded_packages
```

```r
#fast and user friendly parsing of date-time data, extraction and updating of components of a date-time (years, months, days, hours, minutes, and seconds), algebraic manipulation on date-time and time-span objects

install.packages("lubridate", repos = "http://cran.us.r-project.org")
```

```
## 
## The downloaded binary packages are in
## 	/var/folders/45/39m9mn_90czb8cqgm8rvnpm00000gn/T//RtmpK6O3BJ/downloaded_packages
```


```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

```r
#Loading janitor and lubridate packages

library(lubridate)
```


```r
#Importing the last 12 months data into R studio

may22 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202205-divvy-tripdata 2.csv")
```

```
## Rows: 634858 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
jun22 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202206-divvy-tripdata 2.csv")
```

```
## Rows: 769204 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
jul22 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202207-divvy-tripdata 2.csv")
```

```
## Rows: 823488 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
aug22 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202208-divvy-tripdata 2.csv")
```

```
## Rows: 785932 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
sep22 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202209-divvy-publictripdata 2.csv")
```

```
## Rows: 701339 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
oct22 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202210-divvy-tripdata 2.csv")
```

```
## Rows: 558685 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
nov22 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202211-divvy-tripdata 2.csv")
```

```
## Rows: 337735 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
dec22 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202212-divvy-tripdata 2.csv")
```

```
## Rows: 181806 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
jan23 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202301-divvy-tripdata 2.csv")
```

```
## Rows: 190301 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
feb23 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202302-divvy-tripdata 2.csv")
```

```
## Rows: 190445 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
mar23 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202303-divvy-tripdata 2.csv")
```

```
## Rows: 258678 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
apr23 <- read_csv("~/Desktop/Google certification/Cyclistic_Case_Study/202304-divvy-tripdata 2.csv")
```

```
## Rows: 426590 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
## dbl  (4): start_lat, start_lng, end_lat, end_lng
## dttm (2): started_at, ended_at
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
#colnames() function is used to check the consistency of data
colnames(may22)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(jun22)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(jul22)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(aug22)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(sep22)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(oct22)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(nov22)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(dec22)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(jan23)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(feb23)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(mar23)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
colnames(apr23)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```


```r
#str() function is used to check the internal structure of the dataframe
str(may22)
```

```
## spc_tbl_ [634,858 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:634858] "EC2DE40644C6B0F4" "1C31AD03897EE385" "1542FBEC830415CF" "6FF59852924528F8" ...
##  $ rideable_type     : chr [1:634858] "classic_bike" "classic_bike" "classic_bike" "classic_bike" ...
##  $ started_at        : POSIXct[1:634858], format: "2022-05-23 23:06:58" "2022-05-11 08:53:28" ...
##  $ ended_at          : POSIXct[1:634858], format: "2022-05-23 23:40:19" "2022-05-11 09:31:22" ...
##  $ start_station_name: chr [1:634858] "Wabash Ave & Grand Ave" "DuSable Lake Shore Dr & Monroe St" "Clinton St & Madison St" "Clinton St & Madison St" ...
##  $ start_station_id  : chr [1:634858] "TA1307000117" "13300" "TA1305000032" "TA1305000032" ...
##  $ end_station_name  : chr [1:634858] "Halsted St & Roscoe St" "Field Blvd & South Water St" "Wood St & Milwaukee Ave" "Clark St & Randolph St" ...
##  $ end_station_id    : chr [1:634858] "TA1309000025" "15534" "13221" "TA1305000030" ...
##  $ start_lat         : num [1:634858] 41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num [1:634858] -87.6 -87.6 -87.6 -87.6 -87.6 ...
##  $ end_lat           : num [1:634858] 41.9 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num [1:634858] -87.6 -87.6 -87.7 -87.6 -87.7 ...
##  $ member_casual     : chr [1:634858] "member" "member" "member" "member" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(jun22)
```

```
## spc_tbl_ [769,204 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:769204] "600CFD130D0FD2A4" "F5E6B5C1682C6464" "B6EB6D27BAD771D2" "C9C320375DE1D5C6" ...
##  $ rideable_type     : chr [1:769204] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : POSIXct[1:769204], format: "2022-06-30 17:27:53" "2022-06-30 18:39:52" ...
##  $ ended_at          : POSIXct[1:769204], format: "2022-06-30 17:35:15" "2022-06-30 18:47:28" ...
##  $ start_station_name: chr [1:769204] NA NA NA NA ...
##  $ start_station_id  : chr [1:769204] NA NA NA NA ...
##  $ end_station_name  : chr [1:769204] NA NA NA NA ...
##  $ end_station_id    : chr [1:769204] NA NA NA NA ...
##  $ start_lat         : num [1:769204] 41.9 41.9 41.9 41.8 41.9 ...
##  $ start_lng         : num [1:769204] -87.6 -87.6 -87.7 -87.7 -87.6 ...
##  $ end_lat           : num [1:769204] 41.9 41.9 41.9 41.8 41.9 ...
##  $ end_lng           : num [1:769204] -87.6 -87.6 -87.6 -87.7 -87.6 ...
##  $ member_casual     : chr [1:769204] "casual" "casual" "casual" "casual" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(jul22)
```

```
## spc_tbl_ [823,488 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:823488] "954144C2F67B1932" "292E027607D218B6" "57765852588AD6E0" "B5B6BE44314590E6" ...
##  $ rideable_type     : chr [1:823488] "classic_bike" "classic_bike" "classic_bike" "classic_bike" ...
##  $ started_at        : POSIXct[1:823488], format: "2022-07-05 08:12:47" "2022-07-26 12:53:38" ...
##  $ ended_at          : POSIXct[1:823488], format: "2022-07-05 08:24:32" "2022-07-26 12:55:31" ...
##  $ start_station_name: chr [1:823488] "Ashland Ave & Blackhawk St" "Buckingham Fountain (Temp)" "Buckingham Fountain (Temp)" "Buckingham Fountain (Temp)" ...
##  $ start_station_id  : chr [1:823488] "13224" "15541" "15541" "15541" ...
##  $ end_station_name  : chr [1:823488] "Kingsbury St & Kinzie St" "Michigan Ave & 8th St" "Michigan Ave & 8th St" "Woodlawn Ave & 55th St" ...
##  $ end_station_id    : chr [1:823488] "KA1503000043" "623" "623" "TA1307000164" ...
##  $ start_lat         : num [1:823488] 41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num [1:823488] -87.7 -87.6 -87.6 -87.6 -87.6 ...
##  $ end_lat           : num [1:823488] 41.9 41.9 41.9 41.8 41.9 ...
##  $ end_lng           : num [1:823488] -87.6 -87.6 -87.6 -87.6 -87.7 ...
##  $ member_casual     : chr [1:823488] "member" "casual" "casual" "casual" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(aug22)
```

```
## spc_tbl_ [785,932 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:785932] "550CF7EFEAE0C618" "DAD198F405F9C5F5" "E6F2BC47B65CB7FD" "F597830181C2E13C" ...
##  $ rideable_type     : chr [1:785932] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : POSIXct[1:785932], format: "2022-08-07 21:34:15" "2022-08-08 14:39:21" ...
##  $ ended_at          : POSIXct[1:785932], format: "2022-08-07 21:41:46" "2022-08-08 14:53:23" ...
##  $ start_station_name: chr [1:785932] NA NA NA NA ...
##  $ start_station_id  : chr [1:785932] NA NA NA NA ...
##  $ end_station_name  : chr [1:785932] NA NA NA NA ...
##  $ end_station_id    : chr [1:785932] NA NA NA NA ...
##  $ start_lat         : num [1:785932] 41.9 41.9 42 41.9 41.9 ...
##  $ start_lng         : num [1:785932] -87.7 -87.6 -87.7 -87.7 -87.7 ...
##  $ end_lat           : num [1:785932] 41.9 41.9 42 42 41.8 ...
##  $ end_lng           : num [1:785932] -87.7 -87.6 -87.7 -87.7 -87.7 ...
##  $ member_casual     : chr [1:785932] "casual" "casual" "casual" "casual" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(sep22)
```

```
## spc_tbl_ [701,339 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:701339] "5156990AC19CA285" "E12D4A16BF51C274" "A02B53CD7DB72DD7" "C82E05FEE872DF11" ...
##  $ rideable_type     : chr [1:701339] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : POSIXct[1:701339], format: "2022-09-01 08:36:22" "2022-09-01 17:11:29" ...
##  $ ended_at          : POSIXct[1:701339], format: "2022-09-01 08:39:05" "2022-09-01 17:14:45" ...
##  $ start_station_name: chr [1:701339] NA NA NA NA ...
##  $ start_station_id  : chr [1:701339] NA NA NA NA ...
##  $ end_station_name  : chr [1:701339] "California Ave & Milwaukee Ave" NA NA NA ...
##  $ end_station_id    : chr [1:701339] "13084" NA NA NA ...
##  $ start_lat         : num [1:701339] 41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num [1:701339] -87.7 -87.6 -87.6 -87.7 -87.7 ...
##  $ end_lat           : num [1:701339] 41.9 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num [1:701339] -87.7 -87.6 -87.6 -87.7 -87.7 ...
##  $ member_casual     : chr [1:701339] "casual" "casual" "casual" "casual" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(oct22)
```

```
## spc_tbl_ [558,685 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:558685] "A50255C1E17942AB" "DB692A70BD2DD4E3" "3C02727AAF60F873" "47E653FDC2D99236" ...
##  $ rideable_type     : chr [1:558685] "classic_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : POSIXct[1:558685], format: "2022-10-14 17:13:30" "2022-10-01 16:29:26" ...
##  $ ended_at          : POSIXct[1:558685], format: "2022-10-14 17:19:39" "2022-10-01 16:49:06" ...
##  $ start_station_name: chr [1:558685] "Noble St & Milwaukee Ave" "Damen Ave & Charleston St" "Hoyne Ave & Balmoral Ave" "Rush St & Cedar St" ...
##  $ start_station_id  : chr [1:558685] "13290" "13288" "655" "KA1504000133" ...
##  $ end_station_name  : chr [1:558685] "Larrabee St & Division St" "Damen Ave & Cullerton St" "Western Ave & Leland Ave" "Orleans St & Chestnut St (NEXT Apts)" ...
##  $ end_station_id    : chr [1:558685] "KA1504000079" "13089" "TA1307000140" "620" ...
##  $ start_lat         : num [1:558685] 41.9 41.9 42 41.9 41.9 ...
##  $ start_lng         : num [1:558685] -87.7 -87.7 -87.7 -87.6 -87.6 ...
##  $ end_lat           : num [1:558685] 41.9 41.9 42 41.9 41.9 ...
##  $ end_lng           : num [1:558685] -87.6 -87.7 -87.7 -87.6 -87.6 ...
##  $ member_casual     : chr [1:558685] "member" "casual" "member" "member" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(nov22)
```

```
## spc_tbl_ [337,735 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:337735] "BCC66FC6FAB27CC7" "772AB67E902C180F" "585EAD07FDEC0152" "91C4E7ED3C262FF9" ...
##  $ rideable_type     : chr [1:337735] "electric_bike" "classic_bike" "classic_bike" "classic_bike" ...
##  $ started_at        : POSIXct[1:337735], format: "2022-11-10 06:21:55" "2022-11-04 07:31:55" ...
##  $ ended_at          : POSIXct[1:337735], format: "2022-11-10 06:31:27" "2022-11-04 07:46:25" ...
##  $ start_station_name: chr [1:337735] "Canal St & Adams St" "Canal St & Adams St" "Indiana Ave & Roosevelt Rd" "Indiana Ave & Roosevelt Rd" ...
##  $ start_station_id  : chr [1:337735] "13011" "13011" "SL-005" "SL-005" ...
##  $ end_station_name  : chr [1:337735] "St. Clair St & Erie St" "St. Clair St & Erie St" "St. Clair St & Erie St" "St. Clair St & Erie St" ...
##  $ end_station_id    : chr [1:337735] "13016" "13016" "13016" "13016" ...
##  $ start_lat         : num [1:337735] 41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num [1:337735] -87.6 -87.6 -87.6 -87.6 -87.6 ...
##  $ end_lat           : num [1:337735] 41.9 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num [1:337735] -87.6 -87.6 -87.6 -87.6 -87.6 ...
##  $ member_casual     : chr [1:337735] "member" "member" "member" "member" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(dec22)
```

```
## spc_tbl_ [181,806 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:181806] "65DBD2F447EC51C2" "0C201AA7EA0EA1AD" "E0B148CCB358A49D" "54C5775D2B7C9188" ...
##  $ rideable_type     : chr [1:181806] "electric_bike" "classic_bike" "electric_bike" "classic_bike" ...
##  $ started_at        : POSIXct[1:181806], format: "2022-12-05 10:47:18" "2022-12-18 06:42:33" ...
##  $ ended_at          : POSIXct[1:181806], format: "2022-12-05 10:56:34" "2022-12-18 07:08:44" ...
##  $ start_station_name: chr [1:181806] "Clifton Ave & Armitage Ave" "Broadway & Belmont Ave" "Sangamon St & Lake St" "Shields Ave & 31st St" ...
##  $ start_station_id  : chr [1:181806] "TA1307000163" "13277" "TA1306000015" "KA1503000038" ...
##  $ end_station_name  : chr [1:181806] "Sedgwick St & Webster Ave" "Sedgwick St & Webster Ave" "St. Clair St & Erie St" "Damen Ave & Madison St" ...
##  $ end_station_id    : chr [1:181806] "13191" "13191" "13016" "13134" ...
##  $ start_lat         : num [1:181806] 41.9 41.9 41.9 41.8 41.9 ...
##  $ start_lng         : num [1:181806] -87.7 -87.6 -87.7 -87.6 -87.7 ...
##  $ end_lat           : num [1:181806] 41.9 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num [1:181806] -87.6 -87.6 -87.6 -87.7 -87.7 ...
##  $ member_casual     : chr [1:181806] "member" "casual" "member" "member" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(jan23)
```

```
## spc_tbl_ [190,301 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:190301] "F96D5A74A3E41399" "13CB7EB698CEDB88" "BD88A2E670661CE5" "C90792D034FED968" ...
##  $ rideable_type     : chr [1:190301] "electric_bike" "classic_bike" "electric_bike" "classic_bike" ...
##  $ started_at        : POSIXct[1:190301], format: "2023-01-21 20:05:42" "2023-01-10 15:37:36" ...
##  $ ended_at          : POSIXct[1:190301], format: "2023-01-21 20:16:33" "2023-01-10 15:46:05" ...
##  $ start_station_name: chr [1:190301] "Lincoln Ave & Fullerton Ave" "Kimbark Ave & 53rd St" "Western Ave & Lunt Ave" "Kimbark Ave & 53rd St" ...
##  $ start_station_id  : chr [1:190301] "TA1309000058" "TA1309000037" "RP-005" "TA1309000037" ...
##  $ end_station_name  : chr [1:190301] "Hampden Ct & Diversey Ave" "Greenwood Ave & 47th St" "Valli Produce - Evanston Plaza" "Greenwood Ave & 47th St" ...
##  $ end_station_id    : chr [1:190301] "202480.0" "TA1308000002" "599" "TA1308000002" ...
##  $ start_lat         : num [1:190301] 41.9 41.8 42 41.8 41.8 ...
##  $ start_lng         : num [1:190301] -87.6 -87.6 -87.7 -87.6 -87.6 ...
##  $ end_lat           : num [1:190301] 41.9 41.8 42 41.8 41.8 ...
##  $ end_lng           : num [1:190301] -87.6 -87.6 -87.7 -87.6 -87.6 ...
##  $ member_casual     : chr [1:190301] "member" "member" "casual" "member" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(feb23)
```

```
## spc_tbl_ [190,445 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:190445] "CBCD0D7777F0E45F" "F3EC5FCE5FF39DE9" "E54C1F27FA9354FF" "3D561E04F739CC45" ...
##  $ rideable_type     : chr [1:190445] "classic_bike" "electric_bike" "classic_bike" "electric_bike" ...
##  $ started_at        : POSIXct[1:190445], format: "2023-02-14 11:59:42" "2023-02-15 13:53:48" ...
##  $ ended_at          : POSIXct[1:190445], format: "2023-02-14 12:13:38" "2023-02-15 13:59:08" ...
##  $ start_station_name: chr [1:190445] "Southport Ave & Clybourn Ave" "Clarendon Ave & Gordon Ter" "Southport Ave & Clybourn Ave" "Southport Ave & Clybourn Ave" ...
##  $ start_station_id  : chr [1:190445] "TA1309000030" "13379" "TA1309000030" "TA1309000030" ...
##  $ end_station_name  : chr [1:190445] "Clark St & Schiller St" "Sheridan Rd & Lawrence Ave" "Aberdeen St & Monroe St" "Franklin St & Adams St (Temp)" ...
##  $ end_station_id    : chr [1:190445] "TA1309000024" "TA1309000041" "13156" "TA1309000008" ...
##  $ start_lat         : num [1:190445] 41.9 42 41.9 41.9 41.8 ...
##  $ start_lng         : num [1:190445] -87.7 -87.6 -87.7 -87.7 -87.6 ...
##  $ end_lat           : num [1:190445] 41.9 42 41.9 41.9 41.8 ...
##  $ end_lng           : num [1:190445] -87.6 -87.7 -87.7 -87.6 -87.6 ...
##  $ member_casual     : chr [1:190445] "casual" "casual" "member" "member" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(mar23)
```

```
## spc_tbl_ [258,678 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:258678] "6842AA605EE9FBB3" "F984267A75B99A8C" "FF7CF57CFE026D02" "6B61B916032CB6D6" ...
##  $ rideable_type     : chr [1:258678] "electric_bike" "electric_bike" "classic_bike" "classic_bike" ...
##  $ started_at        : POSIXct[1:258678], format: "2023-03-16 08:20:34" "2023-03-04 14:07:06" ...
##  $ ended_at          : POSIXct[1:258678], format: "2023-03-16 08:22:52" "2023-03-04 14:15:31" ...
##  $ start_station_name: chr [1:258678] "Clark St & Armitage Ave" "Public Rack - Kedzie Ave & Argyle St" "Orleans St & Chestnut St (NEXT Apts)" "Desplaines St & Kinzie St" ...
##  $ start_station_id  : chr [1:258678] "13146" "491" "620" "TA1306000003" ...
##  $ end_station_name  : chr [1:258678] "Larrabee St & Webster Ave" NA "Clark St & Randolph St" "Sheffield Ave & Kingsbury St" ...
##  $ end_station_id    : chr [1:258678] "13193" NA "TA1305000030" "13154" ...
##  $ start_lat         : num [1:258678] 41.9 42 41.9 41.9 41.9 ...
##  $ start_lng         : num [1:258678] -87.6 -87.7 -87.6 -87.6 -87.7 ...
##  $ end_lat           : num [1:258678] 41.9 42 41.9 41.9 41.9 ...
##  $ end_lng           : num [1:258678] -87.6 -87.7 -87.6 -87.7 -87.7 ...
##  $ member_casual     : chr [1:258678] "member" "member" "member" "member" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
str(apr23)
```

```
## spc_tbl_ [426,590 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:426590] "8FE8F7D9C10E88C7" "34E4ED3ADF1D821B" "5296BF07A2F77CB5" "40759916B76D5D52" ...
##  $ rideable_type     : chr [1:426590] "electric_bike" "electric_bike" "electric_bike" "electric_bike" ...
##  $ started_at        : POSIXct[1:426590], format: "2023-04-02 08:37:28" "2023-04-19 11:29:02" ...
##  $ ended_at          : POSIXct[1:426590], format: "2023-04-02 08:41:37" "2023-04-19 11:52:12" ...
##  $ start_station_name: chr [1:426590] NA NA NA NA ...
##  $ start_station_id  : chr [1:426590] NA NA NA NA ...
##  $ end_station_name  : chr [1:426590] NA NA NA NA ...
##  $ end_station_id    : chr [1:426590] NA NA NA NA ...
##  $ start_lat         : num [1:426590] 41.8 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num [1:426590] -87.6 -87.7 -87.7 -87.7 -87.7 ...
##  $ end_lat           : num [1:426590] 41.8 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num [1:426590] -87.6 -87.7 -87.7 -87.7 -87.6 ...
##  $ member_casual     : chr [1:426590] "member" "member" "member" "member" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```


```r
#Merge all the individual monthly data frames into one large data frame. So that it will be easy to process and analyze the data. 

tripdata_combined <- bind_rows(may22, jun22, jul22, aug22, sep22, oct22, nov22, dec22, jan23, feb23, mar23)
```

## Process

Cleaning the data for further analysis.

### Key tasks

-   Check the data for errors.
-   Choose your tools.
-   Transform the data so you can work with it effectively.
-   Document the cleaning process.

### Deliverable

-   Documentation of any cleaning or manipulation of data


```r
#Inspecting the new data frame tripdata_combined 

colnames(tripdata_combined)
```

```
##  [1] "ride_id"            "rideable_type"      "started_at"        
##  [4] "ended_at"           "start_station_name" "start_station_id"  
##  [7] "end_station_name"   "end_station_id"     "start_lat"         
## [10] "start_lng"          "end_lat"            "end_lng"           
## [13] "member_casual"
```

```r
str(tripdata_combined)
```

```
## spc_tbl_ [5,432,471 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:5432471] "EC2DE40644C6B0F4" "1C31AD03897EE385" "1542FBEC830415CF" "6FF59852924528F8" ...
##  $ rideable_type     : chr [1:5432471] "classic_bike" "classic_bike" "classic_bike" "classic_bike" ...
##  $ started_at        : POSIXct[1:5432471], format: "2022-05-23 23:06:58" "2022-05-11 08:53:28" ...
##  $ ended_at          : POSIXct[1:5432471], format: "2022-05-23 23:40:19" "2022-05-11 09:31:22" ...
##  $ start_station_name: chr [1:5432471] "Wabash Ave & Grand Ave" "DuSable Lake Shore Dr & Monroe St" "Clinton St & Madison St" "Clinton St & Madison St" ...
##  $ start_station_id  : chr [1:5432471] "TA1307000117" "13300" "TA1305000032" "TA1305000032" ...
##  $ end_station_name  : chr [1:5432471] "Halsted St & Roscoe St" "Field Blvd & South Water St" "Wood St & Milwaukee Ave" "Clark St & Randolph St" ...
##  $ end_station_id    : chr [1:5432471] "TA1309000025" "15534" "13221" "TA1305000030" ...
##  $ start_lat         : num [1:5432471] 41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num [1:5432471] -87.6 -87.6 -87.6 -87.6 -87.6 ...
##  $ end_lat           : num [1:5432471] 41.9 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num [1:5432471] -87.6 -87.6 -87.7 -87.6 -87.7 ...
##  $ member_casual     : chr [1:5432471] "member" "member" "member" "member" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   ride_id = col_character(),
##   ..   rideable_type = col_character(),
##   ..   started_at = col_datetime(format = ""),
##   ..   ended_at = col_datetime(format = ""),
##   ..   start_station_name = col_character(),
##   ..   start_station_id = col_character(),
##   ..   end_station_name = col_character(),
##   ..   end_station_id = col_character(),
##   ..   start_lat = col_double(),
##   ..   start_lng = col_double(),
##   ..   end_lat = col_double(),
##   ..   end_lng = col_double(),
##   ..   member_casual = col_character()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

```r
head(tripdata_combined)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["ride_id"],"name":[1],"type":["chr"],"align":["left"]},{"label":["rideable_type"],"name":[2],"type":["chr"],"align":["left"]},{"label":["started_at"],"name":[3],"type":["dttm"],"align":["right"]},{"label":["ended_at"],"name":[4],"type":["dttm"],"align":["right"]},{"label":["start_station_name"],"name":[5],"type":["chr"],"align":["left"]},{"label":["start_station_id"],"name":[6],"type":["chr"],"align":["left"]},{"label":["end_station_name"],"name":[7],"type":["chr"],"align":["left"]},{"label":["end_station_id"],"name":[8],"type":["chr"],"align":["left"]},{"label":["start_lat"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["start_lng"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["end_lat"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["end_lng"],"name":[12],"type":["dbl"],"align":["right"]},{"label":["member_casual"],"name":[13],"type":["chr"],"align":["left"]}],"data":[{"1":"EC2DE40644C6B0F4","2":"classic_bike","3":"2022-05-23 23:06:58","4":"2022-05-23 23:40:19","5":"Wabash Ave & Grand Ave","6":"TA1307000117","7":"Halsted St & Roscoe St","8":"TA1309000025","9":"41.89147","10":"-87.62676","11":"41.94367","12":"-87.64895","13":"member"},{"1":"1C31AD03897EE385","2":"classic_bike","3":"2022-05-11 08:53:28","4":"2022-05-11 09:31:22","5":"DuSable Lake Shore Dr & Monroe St","6":"13300","7":"Field Blvd & South Water St","8":"15534","9":"41.88096","10":"-87.61674","11":"41.88635","12":"-87.61752","13":"member"},{"1":"1542FBEC830415CF","2":"classic_bike","3":"2022-05-26 18:36:28","4":"2022-05-26 18:58:18","5":"Clinton St & Madison St","6":"TA1305000032","7":"Wood St & Milwaukee Ave","8":"13221","9":"41.88224","10":"-87.64107","11":"41.90765","12":"-87.67255","13":"member"},{"1":"6FF59852924528F8","2":"classic_bike","3":"2022-05-10 07:30:07","4":"2022-05-10 07:38:49","5":"Clinton St & Madison St","6":"TA1305000032","7":"Clark St & Randolph St","8":"TA1305000030","9":"41.88224","10":"-87.64107","11":"41.88458","12":"-87.63189","13":"member"},{"1":"483C52CAAE12E3AC","2":"classic_bike","3":"2022-05-10 17:31:56","4":"2022-05-10 17:36:57","5":"Clinton St & Madison St","6":"TA1305000032","7":"Morgan St & Lake St","8":"TA1306000015","9":"41.88224","10":"-87.64107","11":"41.88578","12":"-87.65102","13":"member"},{"1":"C0A3AA5A614DCE01","2":"classic_bike","3":"2022-05-04 14:48:55","4":"2022-05-04 14:56:04","5":"Carpenter St & Huron St","6":"13196","7":"Sangamon St & Washington Blvd","8":"13409","9":"41.89456","10":"-87.65345","11":"41.88316","12":"-87.65110","13":"member"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
summary(tripdata_combined)
```

```
##    ride_id          rideable_type        started_at                    
##  Length:5432471     Length:5432471     Min.   :2022-05-01 00:00:06.00  
##  Class :character   Class :character   1st Qu.:2022-06-29 13:55:55.50  
##  Mode  :character   Mode  :character   Median :2022-08-20 11:23:00.00  
##                                        Mean   :2022-09-03 04:26:19.95  
##                                        3rd Qu.:2022-10-21 08:47:40.00  
##                                        Max.   :2023-03-31 23:59:28.00  
##                                                                        
##     ended_at                     start_station_name start_station_id  
##  Min.   :2022-05-01 00:05:17.0   Length:5432471     Length:5432471    
##  1st Qu.:2022-06-29 14:17:21.5   Class :character   Class :character  
##  Median :2022-08-20 11:44:08.0   Mode  :character   Mode  :character  
##  Mean   :2022-09-03 04:45:24.2                                        
##  3rd Qu.:2022-10-21 09:00:16.5                                        
##  Max.   :2023-04-03 11:41:11.0                                        
##                                                                       
##  end_station_name   end_station_id       start_lat       start_lng     
##  Length:5432471     Length:5432471     Min.   :41.64   Min.   :-87.84  
##  Class :character   Class :character   1st Qu.:41.88   1st Qu.:-87.66  
##  Mode  :character   Mode  :character   Median :41.90   Median :-87.64  
##                                        Mean   :41.90   Mean   :-87.65  
##                                        3rd Qu.:41.93   3rd Qu.:-87.63  
##                                        Max.   :42.07   Max.   :-87.52  
##                                                                        
##     end_lat         end_lng       member_casual     
##  Min.   : 0.00   Min.   :-88.14   Length:5432471    
##  1st Qu.:41.88   1st Qu.:-87.66   Class :character  
##  Median :41.90   Median :-87.64   Mode  :character  
##  Mean   :41.90   Mean   :-87.65                     
##  3rd Qu.:41.93   3rd Qu.:-87.63                     
##  Max.   :42.37   Max.   :  0.00                     
##  NA's   :5538    NA's   :5538
```

```r
nrow(tripdata_combined)
```

```
## [1] 5432471
```

```r
dim(tripdata_combined)
```

```
## [1] 5432471      13
```

The following code chunks are used for the Data Cleaning process.


```r
install.packages("geosphere", repos = "http://cran.us.r-project.org")
```

```
## 
## The downloaded binary packages are in
## 	/var/folders/45/39m9mn_90czb8cqgm8rvnpm00000gn/T//RtmpK6O3BJ/downloaded_packages
```

```r
library(geosphere)
```

##### Now the dataframe has date_time column that needs to be extracted into separate components. Adding date, month, year, day_of_week columns. ride_length, ride_distance to the dataframe.


```r
tripdata_combined <- tripdata_combined %>% 
   # extract year
  mutate(year = format(as.Date(started_at), "%Y")) %>% 
  #extract month
  mutate(month = format(as.Date(started_at), "%B")) %>% 
  # extract date
  mutate(date = format(as.Date(started_at), "%d")) %>% 
  # extract day of week
  mutate(day_of_week = format(as.Date(started_at), "%A")) %>% 
  
  #calcualting ride_length and start_time (strftime used to convert time objects to characters)
  mutate(ride_length = difftime(ended_at, started_at)) %>% 
  mutate(start_time = strftime(started_at, "%H"))
   
#converting ride_length into numeric format
tripdata_combined <- tripdata_combined %>% 
  mutate(ride_length = as.numeric(ride_length))

# to check it is right format
is.numeric(tripdata_combined$ride_length) 
```

```
## [1] TRUE
```

```r
# calculating ride_distance (distGeo is used to calculate the distance for two given points (latitude and longitude in this case))
tripdata_combined$ride_distance <- distGeo(matrix(c(tripdata_combined$start_lng, tripdata_combined$start_lat), ncol = 2), matrix(c(tripdata_combined$end_lng, tripdata_combined$end_lat), ncol = 2))

# adding ride distance in km
tripdata_combined$ride_distance <- tripdata_combined$ride_distance/1000 
```


```r
str(tripdata_combined)
```

```
## tibble [5,432,471 × 20] (S3: tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:5432471] "EC2DE40644C6B0F4" "1C31AD03897EE385" "1542FBEC830415CF" "6FF59852924528F8" ...
##  $ rideable_type     : chr [1:5432471] "classic_bike" "classic_bike" "classic_bike" "classic_bike" ...
##  $ started_at        : POSIXct[1:5432471], format: "2022-05-23 23:06:58" "2022-05-11 08:53:28" ...
##  $ ended_at          : POSIXct[1:5432471], format: "2022-05-23 23:40:19" "2022-05-11 09:31:22" ...
##  $ start_station_name: chr [1:5432471] "Wabash Ave & Grand Ave" "DuSable Lake Shore Dr & Monroe St" "Clinton St & Madison St" "Clinton St & Madison St" ...
##  $ start_station_id  : chr [1:5432471] "TA1307000117" "13300" "TA1305000032" "TA1305000032" ...
##  $ end_station_name  : chr [1:5432471] "Halsted St & Roscoe St" "Field Blvd & South Water St" "Wood St & Milwaukee Ave" "Clark St & Randolph St" ...
##  $ end_station_id    : chr [1:5432471] "TA1309000025" "15534" "13221" "TA1305000030" ...
##  $ start_lat         : num [1:5432471] 41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num [1:5432471] -87.6 -87.6 -87.6 -87.6 -87.6 ...
##  $ end_lat           : num [1:5432471] 41.9 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num [1:5432471] -87.6 -87.6 -87.7 -87.6 -87.7 ...
##  $ member_casual     : chr [1:5432471] "member" "member" "member" "member" ...
##  $ year              : chr [1:5432471] "2022" "2022" "2022" "2022" ...
##  $ month             : chr [1:5432471] "May" "May" "May" "May" ...
##  $ date              : chr [1:5432471] "23" "11" "26" "10" ...
##  $ day_of_week       : chr [1:5432471] "Monday" "Wednesday" "Thursday" "Tuesday" ...
##  $ ride_length       : num [1:5432471] 2001 2274 1310 522 301 ...
##  $ start_time        : chr [1:5432471] "16" "01" "11" "00" ...
##  $ ride_distance     : num [1:5432471] 6.084 0.602 3.846 0.805 0.915 ...
```


```r
#Remove bad data
# Remove data where ride_length is negative or 'zero' as it is not useful for analyzing

tripdata_clean <- tripdata_combined[!(tripdata_combined$ride_length <= 0),]
```




## Analyze

### Now all the required information are in one place and ready for exploration.

### Key tasks

-   Aggregate your data so it's useful and accessible.
-   Organize and format your data.
-   Perform calculations.
-   Identify trends and relationships.

### Deliverable

-   A summary of the analysis

Compare members and casual users


```r
str(tripdata_clean)
```

```
## tibble [5,431,963 × 20] (S3: tbl_df/tbl/data.frame)
##  $ ride_id           : chr [1:5431963] "EC2DE40644C6B0F4" "1C31AD03897EE385" "1542FBEC830415CF" "6FF59852924528F8" ...
##  $ rideable_type     : chr [1:5431963] "classic_bike" "classic_bike" "classic_bike" "classic_bike" ...
##  $ started_at        : POSIXct[1:5431963], format: "2022-05-23 23:06:58" "2022-05-11 08:53:28" ...
##  $ ended_at          : POSIXct[1:5431963], format: "2022-05-23 23:40:19" "2022-05-11 09:31:22" ...
##  $ start_station_name: chr [1:5431963] "Wabash Ave & Grand Ave" "DuSable Lake Shore Dr & Monroe St" "Clinton St & Madison St" "Clinton St & Madison St" ...
##  $ start_station_id  : chr [1:5431963] "TA1307000117" "13300" "TA1305000032" "TA1305000032" ...
##  $ end_station_name  : chr [1:5431963] "Halsted St & Roscoe St" "Field Blvd & South Water St" "Wood St & Milwaukee Ave" "Clark St & Randolph St" ...
##  $ end_station_id    : chr [1:5431963] "TA1309000025" "15534" "13221" "TA1305000030" ...
##  $ start_lat         : num [1:5431963] 41.9 41.9 41.9 41.9 41.9 ...
##  $ start_lng         : num [1:5431963] -87.6 -87.6 -87.6 -87.6 -87.6 ...
##  $ end_lat           : num [1:5431963] 41.9 41.9 41.9 41.9 41.9 ...
##  $ end_lng           : num [1:5431963] -87.6 -87.6 -87.7 -87.6 -87.7 ...
##  $ member_casual     : chr [1:5431963] "member" "member" "member" "member" ...
##  $ year              : chr [1:5431963] "2022" "2022" "2022" "2022" ...
##  $ month             : chr [1:5431963] "May" "May" "May" "May" ...
##  $ date              : chr [1:5431963] "23" "11" "26" "10" ...
##  $ day_of_week       : chr [1:5431963] "Monday" "Wednesday" "Thursday" "Tuesday" ...
##  $ ride_length       : num [1:5431963] 2001 2274 1310 522 301 ...
##  $ start_time        : chr [1:5431963] "16" "01" "11" "00" ...
##  $ ride_distance     : num [1:5431963] 6.084 0.602 3.846 0.805 0.915 ...
```


```r
# lets check summarised details about the cleaned dataset 
summary(tripdata_clean)
```

```
##    ride_id          rideable_type        started_at                    
##  Length:5431963     Length:5431963     Min.   :2022-05-01 00:00:06.00  
##  Class :character   Class :character   1st Qu.:2022-06-29 13:54:59.00  
##  Mode  :character   Mode  :character   Median :2022-08-20 11:22:00.00  
##                                        Mean   :2022-09-03 04:26:17.63  
##                                        3rd Qu.:2022-10-21 08:47:56.50  
##                                        Max.   :2023-03-31 23:59:28.00  
##                                                                        
##     ended_at                      start_station_name start_station_id  
##  Min.   :2022-05-01 00:05:17.00   Length:5431963     Length:5431963    
##  1st Qu.:2022-06-29 14:16:18.50   Class :character   Class :character  
##  Median :2022-08-20 11:43:08.00   Mode  :character   Mode  :character  
##  Mean   :2022-09-03 04:45:22.14                                        
##  3rd Qu.:2022-10-21 09:00:32.50                                        
##  Max.   :2023-04-03 11:41:11.00                                        
##                                                                        
##  end_station_name   end_station_id       start_lat       start_lng     
##  Length:5431963     Length:5431963     Min.   :41.64   Min.   :-87.84  
##  Class :character   Class :character   1st Qu.:41.88   1st Qu.:-87.66  
##  Mode  :character   Mode  :character   Median :41.90   Median :-87.64  
##                                        Mean   :41.90   Mean   :-87.65  
##                                        3rd Qu.:41.93   3rd Qu.:-87.63  
##                                        Max.   :42.07   Max.   :-87.52  
##                                                                        
##     end_lat         end_lng       member_casual          year          
##  Min.   : 0.00   Min.   :-88.14   Length:5431963     Length:5431963    
##  1st Qu.:41.88   1st Qu.:-87.66   Class :character   Class :character  
##  Median :41.90   Median :-87.64   Mode  :character   Mode  :character  
##  Mean   :41.90   Mean   :-87.65                                        
##  3rd Qu.:41.93   3rd Qu.:-87.63                                        
##  Max.   :42.37   Max.   :  0.00                                        
##  NA's   :5538    NA's   :5538                                          
##     month               date           day_of_week         ride_length     
##  Length:5431963     Length:5431963     Length:5431963     Min.   :      1  
##  Class :character   Class :character   Class :character   1st Qu.:    342  
##  Mode  :character   Mode  :character   Mode  :character   Median :    604  
##                                                           Mean   :   1144  
##                                                           3rd Qu.:   1083  
##                                                           Max.   :2483235  
##                                                                            
##   start_time        ride_distance     
##  Length:5431963     Min.   :   0.000  
##  Class :character   1st Qu.:   0.870  
##  Mode  :character   Median :   1.564  
##                     Mean   :   2.124  
##                     3rd Qu.:   2.770  
##                     Max.   :9817.319  
##                     NA's   :5538
```

### Conduct descriptive analysis


```r
## Conduct descriptive analysis
# descriptive analysis on 'ride_length'
# mean = straight average (total ride length / total rides)
# median = midpoint number of ride length array
# max = longest ride
# min = shortest ride

tripdata_clean %>% 
  summarise(average_ride_length = mean(ride_length), median_length = median(ride_length), 
            max_ride_length = max(ride_length), min_ride_length = min(ride_length))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["average_ride_length"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["median_length"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["max_ride_length"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["min_ride_length"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"1144.51","2":"604","3":"2483235","4":"1"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

### Compare members and casual users 
#### Members vs casual riders difference depending on total rides taken


```r
tripdata_clean %>% 
    group_by(member_casual) %>% 
    summarise(ride_count = length(ride_id), ride_percentage = (length(ride_id) / nrow(tripdata_clean)) * 100)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["member_casual"],"name":[1],"type":["chr"],"align":["left"]},{"label":["ride_count"],"name":[2],"type":["int"],"align":["right"]},{"label":["ride_percentage"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"casual","2":"2210779","3":"40.69945"},{"1":"member","2":"3221184","3":"59.30055"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
ggplot(tripdata_clean, aes(x = member_casual, fill=member_casual)) +
    geom_bar() +
    labs(x="Casuals vs Members", y="Number Of Rides", title= "Casuals vs Members distribution")
```

![](Cyclistic_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

-   We can see on the Casuals vs Members distribution chart, members possesing \~59%, and casual riders have \~41% of the dataset. So it is clearly visible that in the last 12 months, members used ride share \~18% more than casual riders.

#### Comparison between Members Causal riders depending on ride length (mean, median, minimum, maximum)


```r
tripdata_clean %>%
  group_by(member_casual) %>% 
  summarise(average_ride_length = mean(ride_length), median_length = median(ride_length), 
            max_ride_length = max(ride_length), min_ride_length = min(ride_length))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["member_casual"],"name":[1],"type":["chr"],"align":["left"]},{"label":["average_ride_length"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["median_length"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["max_ride_length"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["min_ride_length"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[{"1":"casual","2":"1713.111","3":"756","4":"2483235","5":"1"},{"1":"member","2":"754.265","3":"524","4":"93580","5":"1"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

-   From the above table we can conclude that casual riders took bike for longer rides than members, as the average trip duration / average ride length of member riders is lower than the average trip duration / average ride length of casual riders.

-   See total rides and average ride time by each day for members vs casual riders


```r
# lets fix the days of the week order.
tripdata_clean$day_of_week <- ordered(tripdata_clean$day_of_week, 
                                    levels=c("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"))

tripdata_clean %>% 
  group_by(member_casual, day_of_week) %>%  #groups by member_casual
  summarise(number_of_rides = n() #calculates the number of rides and average duration 
  ,average_ride_length = mean(ride_length),.groups="drop") %>% # calculates the average duration
  arrange(member_casual, day_of_week) #sort
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["member_casual"],"name":[1],"type":["chr"],"align":["left"]},{"label":["day_of_week"],"name":[2],"type":["ord"],"align":["right"]},{"label":["number_of_rides"],"name":[3],"type":["int"],"align":["right"]},{"label":["average_ride_length"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"casual","2":"Sunday","3":"370015","4":"2014.3136"},{"1":"casual","2":"Monday","3":"263611","4":"1705.9111"},{"1":"casual","2":"Tuesday","3":"256800","4":"1517.3264"},{"1":"casual","2":"Wednesday","3":"266188","4":"1447.1737"},{"1":"casual","2":"Thursday","3":"294934","4":"1486.0045"},{"1":"casual","2":"Friday","3":"324131","4":"1667.0831"},{"1":"casual","2":"Saturday","3":"435100","4":"1927.8113"},{"1":"member","2":"Sunday","3":"372495","4":"835.8309"},{"1":"member","2":"Monday","3":"450608","4":"726.5233"},{"1":"member","2":"Tuesday","3":"503864","4":"719.7505"},{"1":"member","2":"Wednesday","3":"513810","4":"716.4976"},{"1":"member","2":"Thursday","3":"512523","4":"728.7283"},{"1":"member","2":"Friday","3":"453854","4":"746.3761"},{"1":"member","2":"Saturday","3":"414030","4":"840.2064"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

####  Visualize total rides data by type and day of week


```r
tripdata_clean %>%  
  group_by(member_casual, day_of_week) %>% 
  summarise(number_of_rides = n(), .groups="drop") %>% 
  arrange(member_casual, day_of_week)  %>% 
  ggplot(aes(x = day_of_week, y = number_of_rides, fill = member_casual)) +
  labs(title ="Total rides by Members and Casual riders Vs. Day of the week") +
  geom_col(width=0.5, position = position_dodge(width=0.5)) +
  scale_y_continuous(labels = function(x) format(x, scientific = FALSE))
```

![](Cyclistic_files/figure-html/unnamed-chunk-20-1.png)<!-- -->

####  Visualize average ride time data by type and day of week


```r
tripdata_clean %>%  
  group_by(member_casual, day_of_week) %>% 
  summarise(average_ride_length = mean(ride_length), .groups="drop") %>%
  ggplot(aes(x = day_of_week, y = average_ride_length, fill = member_casual)) +
  geom_col(width=0.5, position = position_dodge(width=0.5)) + 
  labs(title ="Average ride time by Members and Casual riders Vs. Day of the week")
```

![](Cyclistic_files/figure-html/unnamed-chunk-21-1.png)<!-- -->

-   From the first chart above members took consistent trips throughout the week, but there is less rides in Sunday. For casual riders the most taken rides are in weekends, starting rise in Friday followed by Saturday and Sunday.

-   The average ride length for members are much much less than that of casual riders. Also it can be seen that weekend average ride length is much higher for casual riders along with total rides. So both of this facts can be correlated for casual riders. For members average ride length is about the same throughout the week (\<1000 sec).

### See total rides and average ride time by each month for members vs casual riders


```r
# First lets fix the days of the week order.
tripdata_clean$month <- ordered(tripdata_clean$month, 
                            levels=c("January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"))

tripdata_clean %>% 
  group_by(member_casual, month) %>%  
  summarise(number_of_rides = n(), average_ride_length = mean(ride_length), .groups="drop") %>% 
  arrange(member_casual, month)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["member_casual"],"name":[1],"type":["chr"],"align":["left"]},{"label":["month"],"name":[2],"type":["ord"],"align":["right"]},{"label":["number_of_rides"],"name":[3],"type":["int"],"align":["right"]},{"label":["average_ride_length"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"casual","2":"January","3":"40005","4":"1374.9935"},{"1":"casual","2":"February","3":"43014","4":"1391.6157"},{"1":"casual","2":"March","3":"62194","4":"1284.8811"},{"1":"casual","2":"May","3":"280387","4":"1852.3617"},{"1":"casual","2":"June","3":"369022","4":"1926.0914"},{"1":"casual","2":"July","3":"406013","4":"1756.8735"},{"1":"casual","2":"August","3":"358886","4":"1758.7909"},{"1":"casual","2":"September","3":"296664","4":"1679.2975"},{"1":"casual","2":"October","3":"208961","4":"1583.4578"},{"1":"casual","2":"November","3":"100742","4":"1278.0905"},{"1":"casual","2":"December","3":"44891","4":"1337.4632"},{"1":"member","2":"January","3":"150288","4":"621.7265"},{"1":"member","2":"February","3":"147422","4":"642.8881"},{"1":"member","2":"March","3":"196465","4":"626.5715"},{"1":"member","2":"May","3":"354423","4":"802.0459"},{"1":"member","2":"June","3":"400116","4":"840.0233"},{"1":"member","2":"July","3":"417403","4":"823.1640"},{"1":"member","2":"August","3":"426969","4":"803.1252"},{"1":"member","2":"September","3":"404603","4":"778.6192"},{"1":"member","2":"October","3":"349659","4":"717.5952"},{"1":"member","2":"November","3":"236935","4":"667.9508"},{"1":"member","2":"December","3":"136901","4":"637.2205"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

#### Visualize total rides data by type and month


```r
tripdata_clean %>%  
  group_by(member_casual, month) %>% 
  summarise(number_of_rides = n(),.groups="drop") %>% 
  arrange(member_casual, month)  %>% 
  ggplot(aes(x = month, y = number_of_rides, fill = member_casual)) +
  labs(title ="Total rides by Members and Casual riders Vs. Month", x = "Month", y= "Number Of Rides") +
  theme(axis.text.x = element_text(angle = 45)) +
  geom_col(width=0.5, position = position_dodge(width=0.5)) +
  scale_y_continuous(labels = function(x) format(x, scientific = FALSE))
```

![](Cyclistic_files/figure-html/unnamed-chunk-23-1.png)<!-- -->

####  Visualize average ride time data by type and month


```r
tripdata_clean %>%  
  group_by(member_casual, month) %>% 
  summarise(average_ride_length = mean(ride_length),.groups="drop") %>%
  ggplot(aes(x = month, y = average_ride_length, fill = member_casual)) +
  geom_col(width=0.5, position = position_dodge(width=0.5)) + 
  labs(title ="Average ride length by Members and Casual riders Vs. Month") +
  theme(axis.text.x = element_text(angle = 30))
```

![](Cyclistic_files/figure-html/unnamed-chunk-24-1.png)<!-- -->

-   The months June, July, August and September are the most busy time of the year among both members and casual riders. It is possible due to winter there is a significant drop in total rides in the months of November, December, January and February for both type of customers.

-   Average ride length of members is about the same \<1000 secs throughout the year. While casual riders average ride length is between 1000 - 2000 secs throughout the year.

#### Comparison between Members and Casual riders depending on ride distance


```r
tripdata_clean %>% 
  group_by(member_casual) %>% drop_na() %>%
  summarise(average_ride_distance = mean(ride_distance)) %>%
  ggplot() + 
  geom_col(mapping= aes(x= member_casual,y= average_ride_distance,fill=member_casual), show.legend = FALSE)+
  labs(title = "Mean travel distance by Members and Casual riders", x="Member and Casual riders", y="Average distance In Km")
```

![](Cyclistic_files/figure-html/unnamed-chunk-25-1.png)<!-- -->

-   From the above chart we can see that both riders travel about the same average distance. This similarity could be possible due to that member take (same ride time) rides throughout the week, but casual riders took rides mostly in weekends with higher ride time.

#### Analysis and visualization on cyclistic's bike demand by hour in a day


```r
tripdata_clean %>%
    ggplot(aes(start_time, fill= member_casual)) +
    labs(x="Hour of the day", title="Cyclistic's Bike demand by hour in a day") +
    geom_bar()
```

![](Cyclistic_files/figure-html/unnamed-chunk-26-1.png)<!-- -->

-   From the above chart we can see more members between 7am and 11am and more casual riders between 8am and 11am. Also there is a drop in the evening for both type of riders. This information needs to be checked on day basis.

#### Analysis and visualization on cyclistic's bike demand per hour by day of the week


```r
tripdata_clean %>%
    ggplot(aes(start_time, fill=member_casual)) +
    geom_bar() +
    labs(x="Hour of the day", title="Cyclistic's bike demand per hour by day of the week") +
    facet_wrap(~ day_of_week)
```

![](Cyclistic_files/figure-html/unnamed-chunk-27-1.png)<!-- -->

-   There is a lot of diferrence between the weekdays and weekends. There is a big increase of volume in the weekdays between 7am to 10am and another volume increase from 5pm to 7pm. We can hypothesize that members use the bikes as daily routine like going to work (same behaviour throughout the weekdays) and go back from work (5pm - 7pm). Weekends are completely different for members and casual riders, Friday, Saturday and Sunday there is huge peak in volume for casual riders, from this we can hypothesize that casual riders mostly use bike share for leisure activity in the weekends.


```r
#Analysis and visualization on cyclistic's bike demand per hour by month
tripdata_clean %>%
    ggplot(aes(start_time, fill=member_casual)) +
    geom_bar() +
    labs(x="Hour of the day", title="Cyclistic's bike demand per hour by month") +
    facet_wrap(~ month)
```

![](Cyclistic_files/figure-html/unnamed-chunk-28-1.png)<!-- -->

#### Analysis and visualization of Rideable type Vs. total rides by Members and casual riders


```r
tripdata_clean %>%
    group_by(rideable_type) %>% 
    summarise(count = length(ride_id))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["rideable_type"],"name":[1],"type":["chr"],"align":["left"]},{"label":["count"],"name":[2],"type":["int"],"align":["right"]}],"data":[{"1":"classic_bike","2":"2472729"},{"1":"docked_bike","2":"161626"},{"1":"electric_bike","2":"2797608"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
ggplot(tripdata_clean, aes(x=rideable_type, fill=member_casual)) +
    labs(x="Rideable type", title="Rideable type Vs. total rides by Members and casual riders") +
    geom_bar()
```

![](Cyclistic_files/figure-html/unnamed-chunk-29-1.png)<!-- -->

-   From the above viz we can see that members mostly use electric bikes, followed by classic bikes Docked bikes mostly used by casual riders. Electric bikes are more favored by casual riders.

#### Now analyze and visualize the dataset on coordinate basis


```r
#Lets check the coordinates data of the rides.
#adding a new data frame only for the most popular routes >200 rides
coordinates_df <- tripdata_clean %>% 
filter(start_lng != end_lng & start_lat != end_lat) %>%
group_by(start_lng, start_lat, end_lng, end_lat, member_casual, rideable_type) %>%
summarise(total_rides = n(),.groups="drop") %>%
filter(total_rides > 200)
```


```r
# now lets create two different data frames depending on rider type (member_casual)

casual_riders <- coordinates_df %>% filter(member_casual == "casual")
member_riders <- coordinates_df %>% filter(member_casual == "member")
```


```r
# Let's visualize the number of rides by rider type
tripdata_clean %>% 
  mutate(weekday = wday(started_at, label = TRUE)) %>% 
  group_by(member_casual, weekday) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(member_casual, weekday)  %>% 
  ggplot(aes(x = weekday, y = number_of_rides, fill = member_casual)) +
  geom_col(position = "dodge")
```

```
## `summarise()` has grouped output by 'member_casual'. You can override using the
## `.groups` argument.
```

![](Cyclistic_files/figure-html/unnamed-chunk-32-1.png)<!-- -->


### EXPORT SUMMARY FILE FOR FURTHER ANALYSIS

Create a csv file that we will visualize in **Excel**, **Tableau**, or my presentation software


```r
counts <- aggregate(tripdata_clean$ride_length ~ tripdata_clean$member_casual + tripdata_clean$day_of_week, FUN = mean)
write.csv(counts, file = "Cyclistic_bikeshare.csv")
counts2 <- tripdata_clean
write.csv(counts2, file = "cyclistic_bikeshare_version_2.csv")
```


## Share

This phase will be done by presentation, but here on Kaggle we can use Notebooks to share our analysis and visualizations.


### Key tasks

* Determine the best way to share your findings.
* Create effective data visualizations.
* Present your findings.
* Ensure your work is accessible.

#### Deliverable

* Supporting visualizations and key findings


#### Main insights and conclusions


* Members holds the biggest proportion of the total rides, ~19% higher than casuals riders.

* In all months we have more members than casual riders. In colder months casual riders drop significantly.

* For casual riders the biggest volume of data is on the the weekend.

* This could be possible that member use bikes for work commute purpose, this information can be backed by their bike usage in colder months, where there is significant drop in casual members in those months.

### How members use bike differently from casuals

* In general members have taken the higher number of rides compared to casual riders. There is a rise in total rides taken from April to September. During weekends there is a gradual increase in demand compared to the weekdays.

* Except weekends there is a considerable rise in total number of rides taken by members than casual riders. During weekends casual riders seems to be taking the total number of rides higher than the members. 

* Members have a high preference for electric bikes, followed by classic bike.

* Casuals riders have more ride length (ride duration) than members as they are taking bike for weekend riding.Members have a more fixed use for bikes for work commute activities. 

* Average ride length is calculated based on several criteria.
Weekdays - casual riders have higher ride length. It even more increases in weekends.
month - casual riders have higher ride length. It even more increased in summer months

* We have more members and casuals during the morning, mainly between 8am and 11am. And less riders between 6pm and 9pm.

* Bike demand based on hour of the day - Morning 8am to 11am is the peak demand hour. It decreases gradually throughout the evening. It gradually increases from early morning.

## Act

Act phase will be done by the Cyclistic's executive team, Director of Marketing (Lily Moreno), Marketing Analytics team on the basis of my analysis. (Data-driven decision making)


### Deliverable

#### Your top three recommendations based on your analysis

* Introduce a weekend membership plan and Target the casual riders for that plan. A special offers can be given for special holidays. So that they will be motivated to switch to membership plan. 

* During the riders active months, a targeted marketing campaign can be done to explain the benefits of membership. 
 
* Members are using both classic and electric bikes equally. But the casuals are using more electric bike than classic bike. If the considering the type of bike which is more beneficial for the company, targeted offers and discounts can be given to the particular bike type. 







