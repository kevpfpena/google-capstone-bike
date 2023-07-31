# google-capstone-project-bike
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



