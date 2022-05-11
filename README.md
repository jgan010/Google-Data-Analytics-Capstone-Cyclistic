# Google Data Analytics Capstone Case Study on Cyclistic Bike Share 
<p align="centre">
<img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Cyclistic%20Bike%20share%20logo.png" width=20% height=20%> 
</p>
### How does a bike-share navigate speedy success? 
This capstone case study on Cyclistic bike share is part of Google Data Analytics Professional course by Google on Coursera

### The data exploration, cleaning and analysis are done using: 
- Postgresql with PGAdmin4
- Tableau
- Excel

## Case Study Objective
Cyclistic, a bike share company in Chicago wants to understand how casual riders and annual members use Cyclistic bikes differently. These insights will be used to design a new marketing strategy to convert casual riders into annual member as the company believes that the company’s future success depends on maximizing the number of annual memberships 

## Brief background of case study company
A bike-share program that features more than 5,824 bicycles and 692 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.

## Limitation/Assumptions made of data available
- No information on where casual riders lives in the Cyclistic service area due to data-privacy issues prohibit the use of riders’ personally identifiable information.
- Analysis and insights will be limited on the casual rider’s behaviour as there are no data on types of purchase (single pass or full-day pass) and if there are multiple purchases from the same casual rider. 

## Data sources
Historical bike trip data provided by Motivate International Inc. under licence from [Divvy Bikes](https://ride.divvybikes.com/data-license-agreement). (The datasets have a different name because Cyclistic is a fictional company for the purpose of the Google Data Analytic Capstone project). Personal identifiable information are not available due to data-privacy. 

Dataset was downloaded from https://divvy-tripdata.s3.amazonaws.com/index.html. 
For the purpose of this analysis, 12 months of data from April 2021 to March 2022 will be analysed. The most recent data available was March 2022. Total data points is approximately 5.7M.

**Dataset was checked for credibility** 
- The dataset is reliable, original, cited as it is provided under licence as above.  
- Data is current as the most recent data used was March 2022
- There are missing data points for start station and end station and geographic latitude and longitude in the dataset therefore the data is not as comprehensive as it could have been. We will keep this in mind and account for these during data analysis.


## Data Exploration and cleaning using SQL
**Data exploration and cleaning are done using SQL query on PostgreSQL on pgAdmin4.** *Query code in txt file.*
- ride_id  was checked for duplicate  and was confirmed to be unique. 
- Removing rides that has end time before the start time. 
- SQL Query has revealed missing values in station name, station id, end latitude, end longitude. These are approximately 13% of the data points. These datapoints are:
    - not excluded in ride calculations to understand behaviour of the customers who are casual and members as it will give a more accurate representation of the bike usage.
    - are excluded in understanding the top 10 popular stations between customer who are casual and member to gain insights on location usage.
- Rides that are a minute and less are excluded – start and end location checked to be the same therefore would assume these are not valid rides. 
- SQL query revealed maximum ride duration as long as 38 days. It is likely that this may be an error or an outlier. However, rides that are more than 24 hours only made up approximately 0.07% therefore these rides are unlikely to affect the analysis. Therefore the data was kept in case of further question that arises during analysis.


**Documentation of any cleaning or manipulation of data**

    - Added columns for: 
      - ride month number column and month name column
      - season 
      - day name
      - weekend_weekday
      - ride start hour 
      - ride duration (is rounded to the nearest minute)
    - Added ‘Not available’ to start station name, start station id, end station name and end station id
    - The output of to_char() is a padded text with 9 characters, therefore, data was trimmed 
    - Exclude data that is negative ride duration. 
    - Data was grouped and summarised in SQL, and further processed in Tableau. 

    *(Important observation during analysis:  During analysis in Tableau, it was noticed that the analysis of the average ride duration did not ‘make sense’ against the counts in ride durations ‘bins’.  Rechecking the data against SQL query of raw data revealed that this observation is valid. Data was checked again and it was due to the grouped data which has a count column and this affected the ‘quick’ aggregation measure in Tableau. The resolution for this issue is to use the level of detail expressions in Tableau.)*
 
## Data Visualizaiton
Data analysis visualization is on [Tableau Google Data Analytics Capstone Cyclistic Bike share by Jun Gan](https://public.tableau.com/app/profile/jun.gan3045/viz/GoogleDataAnalyticsCapstoneCaseStudyHowDoesaBike-ShareNavigateSpeedySuccess_16517513915180/GoogleDataAnalyticsCapstoneCaseStudy1?publish=yes)

## Summary Analysis 
#### Cyclistic Riders 
Annual Members usage surpass casual riders by 11%. Both customers prefer classic bikes. 
<p align="centre"
  <img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Cyclistic%20Customers.png" width=50% height = "50%>
</p>

#### Season Usage
Bike usage peak during summer months for both casual riders and annual members with only slightly higher number of rides for casual riders. There is a significant decline in casual riders in winter months compared to annual members. Between October to December, the number of casual riders is 1.5 -2.6x less than annual members. 

<img src= "https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Number%20of%20Rides%20by%20Season.png" width=50% height=50%>

#### Ride Analysis
High usage of bikes by annual members during peak rush hours with rides averaging around 13.7 minutes. Half of the annual members (54.5%) tend to use the bikes for less than 10 minutes. The number of rides by annual members drop during weekends and are lower than casual members.  These suggests that annual members use the bikes for commuting to work. 
<p align="centre">
<img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Number%20of%20Rides%20by%20Hour.png" width=60% height=60%>   <img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Total%20Number%20of%20Rides%20by%20Week.png" width=40% height=40%>

<img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Average%20Ride%20Duration%20by%20Day.png" width=50% height=49%>    <img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Avg%20Ride%20Duration%20trend%20by%20season.png" width=50% height=50%>.   

<img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Number%20of%20rides%20by%20Ride%20duration%20(bins).png" width=50% height=50%>
</p>

Casual Riders on the other hand rides 2.2-2.5x longer than annual members throughout the week and with longer average ride duration (32.3min).  However, 30% of casual riders tend to use the bikes for 10 min or less suggesting that the bikes may be used for commuting similar to annual members. However, it is not possible to confirm this without additional data. 
 
The number of casual rides are lower than the annual member during the weekday but higher in the weekend and peaks during summer. In the summer, the average ride duration also peaks. This suggests that casual riders use the bikes for leisure and possibly a proportion of them are tourists. Start station location may give an indication if casual riders uses the bikes for leisure and touristic purposes. 

<p align="centre">
<img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Avg%20Ride%20Duration%20trend%20by%20season.png" width=50% height=50%>
</p>

#### Location of Start Station 
The most popular start station is Streeter Dr & Grand Ave. This happens to be a popular tourist location with parks and museam nearby. The location of start station for Casual riders are slightly more concentrated on the coast whereas annual members are slightly more evenly spread in the city indicated by the bubble size representing the total number of rides.
The bottom right corner of the map is the location of University of Chicago and the there is a higher number of annual members in this area compared to casual riders indicated by the circle size in the map. Likely this is also the case in the other parts of the city where the higher education institutes are located. It can be concluded that it is high possibility that a proportion of annual members are university students. However, this cannot be confirmed without further data on the demographics of the Cyclistic customers. 

<p align="centre">
<img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Map%20Casual%20riders.png" width=30% height=30%>       <img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Map%20Annual%20Members.png" width=30% height=30%>
<p>
    
<img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Top%2010%20Station.png" width=40% height=40%>

<img src="https://github.com/jgan010/Google-Data-Analytics-Capstone-Cyclistic/blob/main/Cyclistic%20Analysis%20Images/Number%20of%20rides%20table.png" width=80% height=80%>

## Conclusion: 
Bike usage peak during summer months. Annual members show peak usage at peak hours with ride duration averaging around 13 minutes.  Casual riders tend to use the bikes 2.2 – 2.5x longer than annual members. Higher numbers of casual riders around the coastal area whereas the number of annual members tends are more evenly spread across city and higher around university area. 30% of casual riders uses the bike for 10 min and less suggest possibility that these riders are commuters with potential to convert them to annual membership.  

## Recommendations based on insights
The possible recommendations based on the insights so far are: 
1.	Increase marketing campaign and advertisement in summer months, weekends, peak hours, top 10 most popular station for Casual Riders
2.	Offer trial membership and discounted membership if they continue after the trial to casual riders
3.	Consider implementing tiered annual membership with weekend options for those that prefers to use bikes in the weekends and for those that uses the bikes for commuting

**END OF ANALYSIS AND INSIGHTS**
