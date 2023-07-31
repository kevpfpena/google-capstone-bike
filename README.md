![image](https://github.com/kevpfpena/google-capstone-bike/assets/84267369/21bac811-309d-4510-93f5-84c3d80c19f9)# google-capstone-project-bike
This report is for a hypothetical company called Cyclistic as part of the Google Data Analytics Program Capstone Project. The company is a bikeshare company and they believe that maximizing the amount of annual members will lead to future growth of the company. 

# Ask

The business task is to convert casual riders into annual members. I’ve been tasked to dive into historical data to compare both casual riders and annual members to identify any trends and differences between both categories and after doing so, offer recommendations based on the insights obtained from the data in order to help produce a marketing campaign to convert casual members to annual riders. 

# Prepare
The data in this case is provided by Motivate International Inc. under a license. The license allows the public to access, reproduce, analyze, copy, modify, distribute in your product or service and use the Data for any lawful purpose. This data is public, however the limitations are that the riders’ personal information are kept private meaning there is no way of connecting pass purchases to credit card numbers to determine if the casual riders live in the Cyclistic service area or they have multiple purchase passes. This also means that there is no way of knowing whether the same customer used multiple rides.

The data obtained was from July 2022 to June 2023. The data was organized in a folder and the naming convention used was YEARXX-divvy-tripdata where the YEAR is either 2022 or 2023 and the XX denotes the month (eg. 07 to denote July).

The data contains the following variables:
* ride_id - a unique 16 character ID for each ride
* rideable_type - the type of bike used: electric, classic or docked
* started_at - the date and time the trip started
* ended_at - the date and time the trip ended (when the bike was either docked or locked)
* start_station_id - a unique key for the starting station
* start_station_name - the name of the start station
* end_station_id - a unique key for the ending station
* end_station_name - the name of the ending station
* start_lat - latitude of the starting position
* start_lng - longitude of the starting position
* end_lat - latitude of the ending position
* end_lng - longitude of the ending position
* member_casual - indicates whether the rider was a member or casual rider

# Process
Before analysis, I need to clean the data and filter out the information I do not need. For this, I used SQL as I am quite familiar with Microsoft Excel and wanted to practice using SQL. In addition, there were millions of data so I felt it was appropriate to use SQL. I used Microsoft SQL Server Management Studio 19 for this as BigQuery had a 100MB file limit. 

First I combined the data into one table using the following code:
```
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
INTO CapstoneProject.dbo.combined_data
FROM CapstoneProject..['202207-divvy-tripdata$']
UNION
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202208-divvy-tripdata$']
UNION
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202209-divvy-tripdata$']
UNION
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202210-divvy-tripdata$']
UNION 
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202211-divvy-tripdata$']
UNION
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202212-divvy-tripdata$']
UNION
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202301-divvy-tripdata$']
UNION
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202302-divvy-tripdata$']
UNION
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202303-divvy-tripdata$']
UNION
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202304-divvy-tripdata$']
UNION 
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202305-divvy-tripdata$']
UNION 
SELECT ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_lat, start_lng, end_lat, end_lng, member_casual
FROM CapstoneProject..['202306-divvy-tripdata$']
```
The rest of the SQL code used can be found in [here](https://github.com/kevpfpena/google-capstone-bike/blob/14c1426fd61a54142609d27bafc12780c95e2001/google-capstone-project-sql).

The summary of the data cleaning steps I took were:
* Removed duplicates
* Checked ride_id for any errors (should have 16 characters only) and deleted those with errors.
* Updated null start_station_name and end_station_name with "Locked" for electric bikes as these bikes could be locked anywhere and may not be logged into the system and hence why null appears.
* Deleted records for classic and docked bikes with null start_station_name and end_station_name.
* Created a column called trip_duration which calculated the difference between the ended_at and started_at column. Displayed in minutes.
* Created a column called month_started, indicating the month when the trip started.
* Created a column called day_started, indicating the weekday (Mon-Sun) when the trip started.
* Deleted records of data where the trip_duration was greater than 24 hours and less than 1 minute.

# Analyze and Share
For this step, I also used SQL. Check the code file for more details. So, I needed to compare the differences between the casual and annual riders. To do that, I did the following first:
* Compared the total number of casual and member rides over the whole period.
* Compared the number of casual rides and member rides in each month.
* Compare the average trip duration in each month.

For visualization I used Tableau Public.

![image](https://github.com/kevpfpena/google-capstone-bike/assets/84267369/69b3c119-c846-4dfb-9642-e19f26fbb87d)
From the image, we can see that there were more member rides than casual rides from July 2022 to June 2023 (about 1.2 million more). Diving deeper into this, we can see the monthly rides for each customer type.

![image](https://github.com/kevpfpena/google-capstone-bike/assets/84267369/3d1158a6-1fd3-49af-a88c-647f49296ca5)
From this image, we can see that there were also more member rides in each month compared to casual rides. However, for both casual and members, the amount of rides peaks at around July and is at its lowest during December to February. This is likely due to the winter months (cold weather). Whereas the number of rides peak during the summer months could be due to good weather or summer holidays.

![image](https://github.com/kevpfpena/google-capstone-bike/assets/84267369/5a1ea9da-3dc9-437f-b1ca-a40ee351bf2e)
As for trip duration, we can see that the average trip duration for the members are shorter but also more consistent whereas the casual riders take longer trips but the trip duration falls off during the winter months (Dec-Jan) and gradually increases as it approaches summer (June-July). 

From this, a few insights can be obtained:
* This suggests that casual riders tend to make the most of their money by going on longer trips.
* The fact that member rides are still quite high during the winter months (Dec-Feb) suggests that some people use the bikes as their main mode of transportation. The consistent average trip durations over the year also indicate this.

To understand further and gain more insights. I analysed the data and looked at a few more things:
* Which days were most popular for each type of customer?
* On which days were the trips longest?

So I analysed and compared the number of rides on each weekday. 
![image](https://github.com/kevpfpena/google-capstone-bike/assets/84267369/c6ef580e-ff24-4cf2-a539-747ff230d9cc)
From the image, I found that member rides are much higher on Mon-Friday and decreases during Saturdays and Sundays. Casual riders are low during Mon-Thurs and slowly increases on Friday and peaks on Saturday before decreasing again on Sunday. This heavily suggests that members use the bikes as their main mode of transport (perhaps to work or school) whereas casual riders tend to use the bikes when they only need to or for fun or sport during the weekends.

![image](https://github.com/kevpfpena/google-capstone-bike/assets/84267369/5a70ecdd-ef34-47e2-bcff-ac8933554e83)
This image also shows that trips were longer on weekends for both casual riders and members. Likely due to more free time or having less commitments, the riders take longer trips during the weekends. 

As I found earlier that casual members took longer trips on average, I wanted to compare the number of trips that lasted over 30 minutes. 
![image](https://github.com/kevpfpena/google-capstone-bike/assets/84267369/f074e0fb-5999-4601-bd4a-9c68ffd745c6)
From this image, we can see that there is a big spike of casual riders taking longer trips during the summer months whilst there is a drop during the winter months. This further reiterates the suggestion that due to the summer holidays or good weather, people tend to choose to cycle casually, hence the spike in casual rides.

Finally, I wanted to undestand at what time do the riders start their trips. To do so, I compared the total number of rides over the entire period at different hours and found something interesting. 
![image](https://github.com/kevpfpena/google-capstone-bike/assets/84267369/12b45665-ba40-45a6-89fe-0593c0ebf71c)
From this visualization, it can be seen that there is a spike at 8:00 (8am) and 17:00 (5pm) for members. This confirms that members use the bikes as their main mode of transport as these times correspond to times where people go to work/school or leave work/school.

If you'd like to see a dashboard on my Tableau Public profile, click [here](https://public.tableau.com/views/GoogleDataAnalyticsCapstoneProjectBikeDataJuly2022-June2023/Dashboard1?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link).

# Act
The main findings were for each customer types are as follows:
### Casual riders
* Has a lot of rides in the summer months (June, July) while it is drastically low in the winter months (December - February).
* More rides at 17:00 (5pm) than any other time
* More rides on the weekends (especially Saturday) than the weekdays.
* Goes on longer trips on average.
* Tends to use the bikes for fun or during free time.

### Member riders
* Has a lot of rides in the summer months and while it decreases in the winter months, there are still at least more than 100k rides.
* More rides during the weeekdays than the weekends.
* Rides spike at around 8am and 5pm.
* Goes on shorter trips on average.
* Members likely use the bikes as main mode of transportation.

Therefore, in order to convert casual riders to members. My top 3 recommendations are:
1. Offer membership incentives for those who take longer trips (lower cost, free rides).
2. Offer membership discounts for rides during weekends on summer months.
3. Offer membership benefits such as lower costs for those who ride during off peak hours/seasons.

# Conclusion
To expand on the findings, if customer data could be obtained, more insights could be found so we could find out how many actual riders are there who ride casually and who are members. The analysis found that members have more rides but we also found that members were more likely to use the bikes as their main mode of transportation. So, this isnt a good representation of the number of member riders and casual riders. With this information, we can also find out which casual riders use the bikes often and analyse why do they not use a membership.

# My own thoughts
So, this is the end of the Capstone project for the google data analytics professional certificate. I took this course cause I had a lot of free time after graduating from university in mechanical engineering and I wanted to expand my skillset and learn something new. I learned alot from this course such as Excel, SQL, Tableau and R. However, I feel like I've only grazed the surface of data analytics and I hope to further improve and build on the skills I learned in this course to make more personal projects cause it was alot of fun.


