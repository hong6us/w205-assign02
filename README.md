# Query Project
- In the Query Project, you will get practice with SQL while learning about Google Cloud Platform (GCP) and BiqQuery. You'll answer business-driven questions using public datasets housed in GCP. To give you experience with different ways to use those datasets, you will use the web UI (BiqQuery) and the command-line tools, and work with them in jupyter notebooks.
- We will be using the Bay Area Bike Share Trips Data (https://cloud.google.com/bigquery/public-data/bay-bike-share). 

#### Problem Statement
- You're a data scientist at Ford GoBike (https://www.fordgobike.com/), the company running Bay Area Bikeshare. You are trying to increase ridership, and you want to offer deals through the mobile app to do so. What deals do you offer though? Currently, your company has three options: a flat price for a single one-way trip, a day pass that allows unlimited 30-minute rides for 24 hours and an annual membership. 

- Through this project, you will answer these questions: 
  * What are the 5 most popular trips that you would call "commuter trips"?
  
    I define "commuter trips" as the daily routine hours.  Based on the 2nd query, these are the top 5 popular trips.  8am, 5pm, 9am,       4pm, 6pm.
  * What are your recommendations for offers (justify based on your findings)?
  
    One of the recommandation is to provide friends discounts for the commuters.  They receive discount by bringing in friends to       subscribe.


## Assignment 02: Querying Data with BigQuery

### What is Google Cloud?
- Read: https://cloud.google.com/docs/overview/

### Get Going

- Go to https://cloud.google.com/bigquery/
- Click on "Try it Free"
- It asks for credit card, but you get $300 free and it does not autorenew after the $300 credit is used, so go ahead (OR CHANGE THIS IF SOME SORT OF OTHER ACCESS INFO)
- Now you will see the console screen. This is where you can manage everything for GCP
- Go to the menus on the left and scroll down to BigQuery
- Now go to https://cloud.google.com/bigquery/public-data/bay-bike-share 
- Scroll down to "Go to Bay Area Bike Share Trips Dataset" (This will open a BQ working page.)


### Some initial queries
Paste your SQL query and answer the question in a sentence.

- What's the size of this dataset? (i.e., how many trips) 
  983648
  ```sql
  SELECT count(*) FROM [bigquery-public-data:san_francisco.bikeshare_trips]
  ```
  
- What is the earliest start time and latest end time for a trip?

  2013-08-29 09:08:00 UTC
  ```
  SELECT min(start_date) FROM [bigquery-public-data:san_francisco.bikeshare_trips]
  ```
  2016-08-31 23:48:00 UTC
  ```
  SELECT max(end_date) FROM [bigquery-public-data:san_francisco.bikeshare_trips]
  ```
- How many bikes are there?
  700
  ```
  SELECT count(distinct bike_number) FROM [bigquery-public-data:san_francisco.bikeshare_trips]
  ```
### Questions of your own
- Make up 3 questions and answer them using the Bay Area Bike Share Trips Data.
- Use the SQL tutorial (https://www.w3schools.com/sql/default.asp) to help you with mechanics.

- Question 1: What are the most popular station pair?
  * Answer:  50 and 60 is the most popular pair
  * SQL query:
     ```
     SELECT count(*) as count, start_station_id, end_station_id FROM [bigquery-public-data:san_francisco.bikeshare_trips]
     Group by start_station_id, end_station_id
     Order by count DESC
     ```

- Question 2:  What are the most popular hours by subscriber type?
  * Answer: 8am, 5pm, 9am, 4pm, 6pm, and these trips are completed by subscribers.
  * SQL query:
     ```
     SELECT subscriber_type, hour(start_date) as hour, count(hour(start_date)) as count FROM [bigquery-public-data:san_francisco.bikeshare_trips]
     Group by hour, subscriber_type
     Order by count DESC
     ```


- Question 3: What are the longest trips by subscriber type "customer"?
  * Answer: Trip_ID 568474 completed 4797.33 hours
  * SQL query:
      ```
      SELECT Trip_id, start_date, end_date, round(duration_sec/3600, 2) as duration FROM [bigquery-public-data:san_francisco.bikeshare_trips]
      Where subscriber_type IN ("Customer")
      Order by duration DESC
      ```



