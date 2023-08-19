# Google Capstone Project: Project Process

## Overview

In this file I recorded all the step I followed and how I came to each conclusion.
It will include thought process, codes, graphes, and calculations. For the sake of brevity I will not include all the problems or mistakes I faced during my 
work on this project. However I will mention why I chose to follow certain methods over others.

## Business Task
Identify key behavioural differences between members and casual riders. Or in other words, How do annual members and casual riders use Cyclistic bikes differently?

I started by reading the case study file carefully which I uploaded as "Case-study-1.pdf". long story short, **Cycalistic"** is a fictional bike sharing company, and
I am a data analyst working in a team trying to solve a business problem. The business is looking to expand through converting casual users into members.

To find the main behavioural differences I will need to know how each user type behaves during the whole year.
Siginificant attributes were the following:
 - Ride length (Average ride length for both user types)
 - Count of rides for both members and casual users
 - Bike type
 - The date of the ride (When exactly was this ride recorded)

# Excel

I started by downloading the 12 files for all months in year 2022 (Jan till December). I created a CSV copy and xlsx copy for each for the 12 files (I also kept the 
original files as backup in case I needed them). I was rather familiar with Excel so processing the data in Excel was quite easy.

As instructed in the case study file, I created a column for the ride length and another column for the day of week. it took quite some time since there are 12 files.

I created column called "ride_length" and ” calculated the length of each ride by subtracting the column “started_at” from the column “ended_at”
(=D2-C2) and format as HH:MM:SS using Format > Cells > Time > 37:30:55.

Second column I called "day_of_week". formula used for calculating the week day was (=WEEKDAY(C2)). this returned values from 1-7. 1 being Sunday and 7 being Saturday.

![image](https://user-images.githubusercontent.com/121754948/222917151-fff53bbc-4444-4f32-a280-cb388ee19094.png)

*other columns are hidden

Both new columns were created in both the csv and xlsx files (with extra columns created in the csv files which I will mention later)

For every month in Excel created pivot tables and charts to go with the analysis on (this took the longest):
 - Number of rides (members vs causuals)
 - Average ride length for each user type
 - Favourite bike type
 - Total rides by weekday
 - Total rides per hour
 - Total rides per month

![image](https://user-images.githubusercontent.com/121754948/222920096-d1090d28-ccc0-429a-b602-341d72f1acda.png)

This is an example for the month of January.
I figured out that combining all data sets of all months in one spreadsheet is impossible due to row limit. So I had to recreate all this in all 12 months.
I aslo added a slicers to filter between User types (members and casuals) and linked it to most pivot tables and all charts.
This was all done in the xlsx files 

The following conclusions were deriven from the all results the pivot tabels and charts yielded:
  - in each month, number of rides made by members were higher than rides made by casual users. However as the years progressed we started to see an increase in 
  the number of rides made by casuals.
  - Average ride length is significantly higher for casual users by almost triple by the begining of the year and remained higher.
  - Sundays happen to be the busiest weekday.
  - Classic bikes seems to be favoured by both user types. While docked bikes were never used by members.
  - 5PM was the rush hour in all months.

I originally planed to use SQL to perform the upcoming analysis but I figured out that R will be much quicker to process this big amount of data 
and I wanted to develop coding skills throguh extensive trial and error (Which did happed).

# R 

You can find the code in the file name "R analysis".
Link to my R Code [Here](https://github.com/AliYasser1/capstone-project/blob/main/R%20analysis)

## Preparing files

1. I installed necessary packages (nothing too fancy, just the usually used packages). 

 - tidyverse
 - hms
 - lubridate
 - data.table

2. I uploaded all 12 csv files to R using read_csv function, saved each in its own data frame for example:
jan_df <- jan_df <- read_csv("202201-divvy-tripdata.csv").

3. I then merged all of the individual files into one large file (which I could not do in Excel) using rbind to create one single View.

4. I copyed the data frame for reference and created a new one called project_date which should include all newly created columns

5. Originally I uploaded the raw csv files to R before creating the new columns (ride_lenght, day_of_week) but I had problems calculating ride_length since I could
not convert the data type of the columns (started_at, ended_at) from character to date. Therefor the fucntion "difftime" did not work
I went back and created these columns (along with extra columns) in the csv files and recreated the process once again.
The extra columns I created were the following:
 - month
 - day
 - hour

6. Then I added extra columns in R using "mutate" function
 - season (Winter, Fall, Summer, Spring)
 - time of day (Morning, Afternoon, Evening, Night)
 
7. I cleaned the data by doing the following:
 - Removing duplicate rows
 - Remove rows with NA values (blank rows)
 - Remove where ride_length is 0 or negative (ride_length should be a positive number)
 - Remove unnecessary columns: ride_id, start_station_id, end_station_id, start_lat, start_long, end_lat, end_lng

The analysis conducted afterwards are seprated into two stages:
1- calcualting totals for each attribute
2- calcuating average for each attribute to see how members differ from casual users.

8. The following was calcualted:
 - count of total rides = 4,369,282
 - total rides grouped by bike type
 - total rides by bike type, member type
 - total rides by month
 - total rides by season (I made a calculation for each season)
 - total rides by day of month
 - total rides by day of week
 - total rides by time of day

the following analysis shows the difference between members and causal users.
 - average ride length
 - average ride length by member typ
 - average ride length by bike type
 - average ride length by season
 - average ride length by month
 - average ride length by time of day
 - average ride length by hour

9. I craeted a new View for tableau where I mutated the following columns for the sake of better Vizualisation
 - month (to be displayed by month name rather than month number)
 - day of week (to be displayed as day name rather than day number)

I removed even 2 more unnecessary columns for the sake of optimising data size
columns removed: start_station_name,end_station_name

10. Finally I saved the files in csv format using the fwrite function: fwrite(project_tableau, "project_data.csv")

**I would like to note that comma separted values (csv) rounds the numbers to the nearest zero.**
This means the ride length was  rounded to minutes.

# Tableau

I chose Tableau for my Vizuallisation since I was more familiar with it and also it was covered in the course.

Link to my Final Tableau dashboard: [Here](https://public.tableau.com/app/profile/ali28508112/viz/GoogleCapstoneProjectCycalistic/FinalViz?publish=yes)

I created graphs mostly similar to those created at first in Excel. They incldued the following
 1- Total rides by user type
 2- Average ride length by user type
 3- Total rides by bike type
 4- Average ride length per weekday
 5- Total rides by hour
 6- Total rides by weekday
 7- Total rides by month

Filters were added on the side to toggle between user types, seasons, and time of day.


# Insights:

## Total rides and average ride length for each user type.

Members had more rides with 2,611,145 total rides or 59.67% and casual riders had 1,758,137 total rides or 40.24%.

![image](https://user-images.githubusercontent.com/121754948/222928370-cc207165-ebd4-4afe-8fa4-e2a1cfb94194.png)

##  Total rides by bike type.

Classic bikes tend to be the most favoured by both members and casual users where Docked bikes are the least favoured by 
casual users and were never used by members.

![image](https://user-images.githubusercontent.com/121754948/222928627-b727ef00-cf69-4e9c-a823-69db8c3d91cb.png)

## Total rides by Weekday.

It appears that Sundays had the highest volumn of rides with 705,323 total rides while Tuesday had the least total rides with 585,934 rides.

![image](https://user-images.githubusercontent.com/121754948/222928684-15a55420-a5b3-49e3-b029-3e08d15acbdc.png)

## Average Ride length by Weekday.

The highest average ride length for both users is Monday followed by Sunday, while the rest of the week seems to be significantlly lower.

![image](https://user-images.githubusercontent.com/121754948/222928740-9a622867-f401-4038-baf7-21638267a61d.png)

## Total rides by Month

It is shown that Summer season has the highest number of rides which peaks at July where Winter season has the least number of rides.

![image](https://user-images.githubusercontent.com/121754948/222928752-0a3c32f5-2c08-4eaf-81b1-14247537d68f.png)


## Total rides by Hour

The graph shows that the Afternoon was the busiest time along the year espeically at 5PM where the Night is the least busy time of day.

![image](https://user-images.githubusercontent.com/121754948/222928776-d98e5c1f-6c4a-480b-a321-ee774cccd6f1.png)

# Suggestions

These suggestions are deriven after examining the final insights of trends and behaviour of members and casual users.

 1. Invest in increasing the number of classic bikes while also boosting their quality
 2. Offering discounts on rides and membership during busy months or weekends.
 3. Expand the marketing campaign to include reviews from the members to allow them to share they experience with Cyclistic

### Thank you and I hope this was inspiring.
