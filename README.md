# Google Capstone Project: Cyclistic Case study
## Cyclistic Bike Sharing

## Overview
**Cyclistic** is a ficitional bike sharing company that basically has two types of users, Members and casual Riders. While **Cyclistic** is trying to 
expand, the strategy is aimed towards converting casual users to members. This is believed to be the key to success in the industry of bike sharing.
for the company to develop the best startegy it needs to know the following:

 1. How do annual members and casual riders use Cyclistic bikes differently?
 2. Why would casual riders buy Cyclistic annual memberships?
 3. How can Cyclistic use digital media to influence casual riders to become members?

The goal of this project is to answer the first and most important question: (**How do annual members and casual riders use Cyclistic bikes differently?**)

### Note: this is not a detailed report. For extensive and detailed report see 

# Step 1: Ask

The main problem we are trying to solve is how we can expand the market share of **Cycalistic**. The designed strategy is to convert causual users into
members. My role as a data analyst is using the provided data to derive conclusions that will support the marketing team.

We need to identify behaviours and trends through out the year for each type of users. by observing and analysing the resources provided we can identify
trends for each period.

# Step 2: Prepare

The resources used in this project is a collection of data provided by google. I am only required to use the data for the previous 12 months (these are
the 12 months of the year 2022). (Note: The datasets have a different name because Cyclistic is a fictional company. For the purposes of this case study,
the datasets are appropriate and will enable you to answer the business questions. The data has been made available by
Motivate International Inc. under this https://ride.divvybikes.com/data-license-agreement. 

# Step 3: Process

First of all I have downloaded all 12 months Excel files. Then I created a CSV copy of all the files. For this project I used Excel to prepare the date 
for analysis. I also used R to combine all data files into one view. finally I used Tableau for the final vizualisation of my analysis.

cleaning the data included the following:
 1. removing duplicates
 2. removing rows containing null values
 3. excluding unneeded columns (ride_id, start_station_id, end_station_id, start_lat, start_lng, end_lat, end_lng)
![image](https://user-images.githubusercontent.com/121754948/222599979-8b2920f7-9b0e-4555-85ec-e4011de29726.png)

 4. new columns created: 
    ride_length: created by subtracting end time from start time
    day_of_week: from 1 to 7 (with 1 being monday and 7 being friday)
    month: from 1 to 12
    day: from 1 to 31 
    hour: 24h
    season: Winter, fall, summer, spring
    time of day (Morning, Afternoon, Evening, Night)

5. created another view for tableau with some columns are formated as Characters instead of numbers.

# Step 4: Analyze

I used R code to conduct the analysis for the following:
 - Total number of rides made by each user during the whole year.
 - Total rides by each bike type for both users.
 - Average ride length for each user type.
 - Total rides made in each month.
 - Total rides made in each season.
 - Total rides by day of month, week, time of day.

# Step 5: Share

The following is darft dashboard made for the project (**NOT FINAL!!**)

![image](https://user-images.githubusercontent.com/121754948/222603755-a0b7554e-b444-4661-8808-42f912b627be.png)

## Key finding:
- Majorty of users are members with 59.76%.
- Rush hours are the Afternoon hours where it peaks at exactly 5PM.
- Busiest season is the summer season espcially June and July.
- Classic bikes are favoured by types of Riders.

# Final Step: Act

Based on the finding I deduced that the best approachs to turn Casuals into members are as follows:
 - Invest in increasing the number of classic bikes while also boosting their quality
 - Offering discounts on rides and membership during busy months or weekends.
 - Expand the marketing campaign to include reviews from the members to allow them to share they experience with **Cyclistic**
