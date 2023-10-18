# Cyclistic Bikes

## Business Task
Analyze Data from casual riders and annual members to discover trends in how they use Cyclistic bikes differently to determine how to maximize annual memberships.  

## Data Sources Used
For this case study, I used data from [Cyclistic’s historical data] (https://divvy-tripdata.s3.amazonaws.com/index.html) for the previous 12 months from May 2021 - April 2022 . The data is a public data set from Motivate International Inc. and was used under this [license.](https://divvybikes.com/data-license-agreement) The data is organized in excel spreadsheets by month. 

## Column Titles
ride_id
rideable_type
started_at
ended_at
start_station_name
start_station_id
end_station_name
end_station_id 
start_lat
start_lng
end_lat
end_lng
member_casual

The data does not have information about the customers to determine how much an individual uses the service nor any billing or credit card information to determine if customers live in the area. This will also mean that we cannot determine how many times a specific customer is using the service or if casual users convert to members. 

## Cleaning and Organizing the Data
For the cleaning process, I considered using google sheets, but it was evident that the amount of data in each spreadsheet slowed down the application so I decided to load my data into BigQuery. After loading my data, I created a new table, year_data, and combined the monthly data into one big table to make it easier to work with. 

![CS1](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/acf79f21-f92e-4473-a5cc-09d26fc3144b)


The next thing that I did was check for a variety of missing values in ride_id and rideable_type, both turned up with no missing values. 

![CP2](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/a5aa347b-9f28-4494-800c-252fad276dec)

I then checked for distinct rideable_type and came up with three: electric_bike, classic_bike, and docked_bike. 

![CP3](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/84b048e8-249d-40fe-9c83-d343287903a6)

Upon checking the website, there were only two types of bikes listed,  classic_bike and electric_bike. I emailed the source of the data and they confirmed that the classic_bike used to be called a docked_bike and they refer to the same bike so I replaced the instances of ‘docked_bike’ with ‘classic_bike’ for consistency. 

![CP4](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/05ecc423-8990-484f-848f-f0b0b246822f)

The next step was that I checked for missing values at the start or end times of a ride.

![CP](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/453c136e-7ddf-4b99-9808-5ad3a0d6b209)

There were no missing start or end times in the data. I then checked for duplicates in ride_id.

![CP5](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/2413b056-812a-4714-8324-fd0d099d56ff)

There were no duplicates in the ride_id, so I moved on to check the user type. I checked for missing values in member_casual as well as how many types were entered. 

![CP6](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/699dc692-b8ce-4184-95c3-2db9a66bc170)

No missing values and the two types entered were member or casual as expected. The next step I wanted to create was a column to calculate the length of each ride, titled ride_length.

![CP7](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/9caca8b7-8945-47bd-9c28-96d502e4ab40)

During this step I also removed rides less than 60 seconds as it could be false starts or trying to redock a bike. I also deleted trips over 24 hours as this could be for maintenance of the bike and bikes are marked as stolen after 24 hours. 

![CP8](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/58651a46-f2b1-4a56-b9f2-06c6ade06d3a)

I then added a column for the day of the week that the trip started and extracted the day of the week from the started_at column. 

![CP9](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/ed5dbb2f-5054-4240-ad59-18879ffe89bf)

I used this column to help me find the mode day of the week overall, by member, and casual riders. 

![CP10](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/4827ece3-00f3-4875-9bcb-73a3cc1ffad6)

The next thing I did was find the mean ride_length in minutes, max ride_length and average ride_length by user type. 

![CP11](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/55c288a9-b1d6-4752-bb2b-afa092a81d7e)

I also explored the mean ride length by day_of_week, and number of rides by day of the week by user type. 

![CP12](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/73dd2e34-f32f-4bd8-82a3-2bfea77af7a9)

I also wanted to see how the time of year affected rides. 

![CP13](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/f8e3ea95-92cc-409c-a072-5ebdd6877399)

From here I explored the total trips by user type and bike preference by user type. 

![CP14](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/115cdd70-72da-448f-95db-9f1edc1dac90)

Finally, I checked the top 5 start and end stations by user type. 

![CP15](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/abd5d226-b3d9-49ab-9534-b159347c55f9)

![CP16](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/28f15b0e-d957-47f8-9fb8-a8fcd6cc5df0)

## Summary of Analysis

Looking through the data, there are noticeable differences in how members and casual users use Cyclistic bikes. The charts below show the top 5 start and end stations by member type.

![Start Station Map1](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/8bfd784a-3cd4-47b7-8c2d-637c1045bdce)

![end_station_map](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/da4be19a-7ac7-4d1d-a527-0034c5d20ffd)

The most popular stations for casual users were concentrated near tourist attractions such as the beach, children’s museum, millennium park, theater and aquarium. Member stations were further from the coast and near more offices, likely being used to commute for work. Looking at the usage by day of the week and user type we can see that the work week is the most popular time for members while they take longer but fewer rides on the weekend. 




In contrast, casual users had the fewest rides during the week and the longest and greatest number of rides on the weekend. 




Casual users average double the ride length of members with casual users averaging 26 minute rides and members averaging 13 minute rides.

![Average_ridelength_usertype](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/b25fc75d-09a9-4f51-92ba-f0ba4db6d51f)

Weather appears to play a role in bike usage with rides dropping in winter months and peaking in the summer. Members take more trips than casual members except in June, July and August.

![Number of Rides by Month](https://github.com/KatherineeFlannery/Project1.md/assets/101511293/66e44f46-8b38-4c5e-a768-0c5a5a5f8b46)

Classic bikes are favored by both members and casual users, making up 60% of rides in each group.

<img width="328" alt="Screenshot 2023-10-18 122106" src="https://github.com/KatherineeFlannery/Project1.md/assets/101511293/5b75fb15-9d29-43a6-976f-44b27342d9b0">

## Recommendations
My top three recommendations to maximize annual memberships:

-- Since casual rider trips are longer than member riders, encourage them to sign up for a membership by charging a fee per minute of usage for casual rides to make the membership more appealing. 
-- Create a tier membership program that offers different levels of memberships for visitors vs locals. 
-- Advertise to casual users at the most popular start/end locations and offer incentives for signing up for a membership. 

