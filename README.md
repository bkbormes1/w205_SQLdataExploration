# Project 1: Query Project

- In the Query Project, you will get practice with SQL while learning about
  Google Cloud Platform (GCP) and BiqQuery. You'll answer business-driven
  questions using public datasets housed in GCP. To give you experience with
  different ways to use those datasets, you will use the web UI (BiqQuery) and
  the command-line tools, and work with them in Jupyter Notebooks.

#### Problem Statement

- You're a data scientist at Lyft Bay Wheels (https://www.lyft.com/bikes/bay-wheels), formerly known as Ford GoBike, the
  company running Bay Area Bikeshare. You are trying to increase ridership, and
  you want to offer deals through the mobile app to do so. 
  
- What deals do you offer though? Currently, your company has several options which can change over time.  Please visit the website to see the current offers and other marketing information. Frequent offers include: 
  * Single Ride 
  * Monthly Membership
  * Annual Membership
  * Bike Share for All
  * Access Pass
  * Corporate Membership
  * etc.

- Through this project, you will answer these questions: 

  * What are the 5 most popular trips that you would call "commuter trips"? 
  
  * What are your recommendations for offers (justify based on your findings)?

- Please note that there are no exact answers to the above questions, just like in the proverbial real world.  This is not a simple exercise where each question above will have a simple SQL query. It is an exercise in analytics over inexact and dirty data. 

- You won't find a column in a table labeled "commuter trip".  You will find you need to do quite a bit of data exploration using SQL queries to determine your own definition of a communter trip.  In data exploration process, you will find a lot of dirty data, that you will need to either clean or filter out. You will then write SQL queries to find the communter trips.

- Likewise to make your recommendations, you will need to do data exploration, cleaning or filtering dirty data, etc. to come up with the final queries that will give you the supporting data for your recommendations. You can make any recommendations regarding the offers, including, but not limited to: 
  * market offers differently to generate more revenue 
  * remove offers that are not working 
  * modify exising offers to generate more revenue
  * create new offers for hidden business opportunities you have found
  * etc. 

#### All Work MUST be done in the Google Cloud Platform (GCP) / The Majority of Work MUST be done using BigQuery SQL / Usage of Temporary Tables, Views, Pandas, Data Visualizations

A couple of the goals of w205 are for students to learn how to work in a cloud environment (such as GCP) and how to use SQL against a big data data platform (such as Google BigQuery).  In keeping with these goals, please do all of your work in GCP, and the majority of your analytics work using BigQuery SQL queries.

You can make intermediate temporary tables or views in your own dataset in BigQuery as you like.  Actually, this is a great way to work!  These make data exploration much easier.  It's much easier when you have made temporary tables or views with only clean data, filtered rows, filtered columns, new columns, summary data, etc.  If you use intermediate temporary tables or views, you should include the SQL used to create these, along with a brief note mentioning that you used the temporary table or view.

In the final Jupyter Notebook, the results of your BigQuery SQL will be read into Pandas, where you will use the skills you learned in the Python class to print formatted Pandas tables, simple data visualizations using Seaborn / Matplotlib, etc.  You can use Pandas for simple transformations, but please remember the bulk of work should be done using Google BigQuery SQL.

#### GitHub Procedures

In your Python class you used GitHub, with a single repo for all assignments, where you committed without doing a pull request.  In this class, we will try to mimic the real world more closely, so our procedures will be enhanced. 

Each project, including this one, will have it's own repo.

Important:  In w205, please never merge your assignment branch to the master branch. 

Using the git command line: clone down the repo, leave the master branch untouched, create an assignment branch, and move to that branch:
- Open a linux command line to your virtual machine and be sure you are logged in as jupyter.
- Create a ~/w205 directory if it does not already exist `mkdir ~/w205`
- Change directory into the ~/w205 directory `cd ~/w205`
- Clone down your repo `git clone <https url for your repo>`
- Change directory into the repo `cd <repo name>`
- Create an assignment branch `git branch assignment`
- Checkout the assignment branch `git checkout assignment`

The previous steps only need to be done once.  Once you your clone is on the assignment branch it will remain on that branch unless you checkout another branch.

The project workflow follows this pattern, which may be repeated as many times as needed.  In fact it's best to do this frequently as it saves your work into GitHub in case your virtual machine becomes corrupt:
- Make changes to existing files as needed.
- Add new files as needed
- Stage modified files `git add <filename>`
- Commit staged files `git commit -m "<meaningful comment about your changes>"`
- Push the commit on your assignment branch from your clone to GitHub `git push origin assignment`

Once you are done, go to the GitHub web interface and create a pull request comparing the assignment branch to the master branch.  Add your instructor, and only your instructor, as the reviewer.  The date and time stamp of the pull request is considered the submission time for late penalties. 

If you decide to make more changes after you have created a pull request, you can simply close the pull request (without merge!), make more changes, stage, commit, push, and create a final pull request when you are done.  Note that the last data and time stamp of the last pull request will be considered the submission time for late penalties.

Make sure you receive the emails related to your repository! Your project feedback will be given as comment on the pull request. When you receive the feedback, you can address problems or simply comment that you have read the feedback. 
AFTER receiving and answering the feedback, merge you PR to master. Your project only counts as complete once this is done.

---

## Parts 1, 2, 3

We have broken down this project into 3 parts, about 1 week's work each to help you stay on track.

**You will only turn in the project once at the end of part 3!**

- In Part 1, we will query using the Google BigQuery GUI interface in the cloud.

- In Part 2, we will query using the Linux command line from our virtual machine in the cloud.

- In Part 3, we will query from a Jupyter Notebook in our virtual machine in the cloud, save the results into Pandas, and present a report enhanced by Pandas output tables and simple data visualizations using Seaborn / Matplotlib.

---

## Part 1 - Querying Data with BigQuery

### SQL Tutorial

Please go through this SQL tutorial to help you learn the basics of SQL to help you complete this project.

SQL tutorial: https://www.w3schools.com/sql/default.asp

### Google Cloud Helpful Links

Read: https://cloud.google.com/docs/overview/

BigQuery: https://cloud.google.com/bigquery/

Public Datasets: Bring up your Google BigQuery console, open the menu for the public datasets, and navigate to the the dataset san_francisco.

- The Bay Bike Share has two datasets: a static one and a dynamic one.  The static one covers an historic period of about 3 years.  The dynamic one updates every 10 minutes or so.  THE STATIC ONE IS THE ONE WE WILL USE IN CLASS AND IN THE PROJECT. The reason is that is much easier to learn SQL against a static target instead of a moving target.

- (USE THESE TABLES!) The static tables we will be using in this class are in the dataset **san_francisco** :

  * bikeshare_stations

  * bikeshare_status

  * bikeshare_trips

- The dynamic tables are found in the dataset **san_francisco_bikeshare**

### Some initial queries

Paste your SQL query and answer the question in a sentence.  Be sure you properly format your queries and results using markdown. 

- What's the size of this dataset? (i.e., how many trips) <br/>
The size of the bikeshare_trips dataset is 983,648 rows.

SQL Query:  
```sql
#standardSQL
    SELECT Count(*) AS Size
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
```

Results: 
<br/>

| Row       | Size     | 
| :-------------: | :----------: | 
|  1 | 983648  | 
  
- What is the earliest start date and time and latest end date and time for a trip? <br/>

The earliest start date and time is August 29th, 2013 at 9:08 UTC and latest end date and time for a trip is August 31st, 2016 at 11:48PM UTC.

SQL Query:
```sql
#standardSQL
    SELECT min(start_date) AS Earliest_times, max(end_date) AS Latest_Time
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
```

Results:
<br/>

| Row       | Earliest_Time     | Latest_Time     |
| :-------------: | :----------: | :-----------: |
|  1 | 2013-08-29 09:08:00 UTC  | 2016-08-31 23:48:00 UTC   |

- How many bikes are there? <br/>
There are 700 bikes.

SQL Query:
```sql
#standardSQL
    SELECT count(distinct bike_number) AS Num_Bikes
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
```

Results:
<br/>

| Row       | Num_Bikes     | 
| :-------------: | :----------: | 
|  1 | 700  | 

### Questions of your own
- Make up 3 questions and answer them using the Bay Area Bike Share Trips Data.  These questions MUST be different than any of the questions and queries you ran above.

- Question 1: What is the average duration of a trip?
  * Answer: The average duration is 1018.93 seconds or ~17 minutes
  * SQL query:
  ```sql
#standardSQL
    SELECT avg(duration_sec) AS Avg_Duration
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
  ```
  * Results:
  <br/>

| Row       | Avg_Duration     | 
| :-------------: | :----------: | 
|  1 | 1018.9323467338004  | 


- Question 2: How many trips started or ended at the station Mezes?
  * Answer: 822 trips started or ended at Mezes station with an ID of 83.
  * SQL query:
  ```sql
#standardSQL
    SELECT count(*) AS Mezes_Trips
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    WHERE start_station_id = 83 OR end_station_id = 83
    ```
  * Results:
    <br/>

| Row       | Mezes_Trips     | 
| :-------------: | :----------: | 
|  1 | 822  | 

- Question 3: How many trips were taken by Subscribers?
  * Answer: There were 846,839 trips taken by subscribers.
  * SQL query:
  ```sql
#standardSQL
    SELECT count(*) AS Tot_Subscribers
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    WHERE subscriber_type = "Subscriber"
    ```
  * Results: 
    <br/>

| Row       | Tot_Subscribers     | 
| :-------------: | :----------: | 
|  1 | 846839  | 


### Bonus activity queries (optional - not graded - just this section is optional, all other sections are required)

The bike share dynamic dataset offers multiple tables that can be joined to learn more interesting facts about the bike share business across all regions. These advanced queries are designed to challenge you to explore the other tables, using only the available metadata to create views that give you a broader understanding of the overall volumes across the regions(each region has multiple stations)

We can create a temporary table or view against the dynamic dataset to join to our static dataset.

Here is some SQL to pull the region_id and station_id from the dynamic dataset.  You can save the results of this query to a temporary table or view.  You can then join the static tables to this table or view to find the region:
```sql
#standardSQL
select distinct region_id, station_id
from `bigquery-public-data.san_francisco_bikeshare.bikeshare_station_info`
```

- Top 5 popular station pairs in each region

- Top 3 most popular regions(stations belong within 1 region)

- Total trips for each short station name in each region

- What are the top 10 used bikes in each of the top 3 region. these bikes could be in need of more frequent maintenance.

---

## Part 2 - Querying data from the BigQuery CLI 

- Use BQ from the Linux command line:

  * General query structure

    ```sql
    bq query --use_legacy_sql=false '
        SELECT count(*)
        FROM
           `bigquery-public-data.san_francisco.bikeshare_trips`'
```

### Queries

1. Rerun the first 3 queries from Part 1 using bq command line tool (Paste your bq
   queries and results here, using properly formatted markdown):

  * What's the size of this dataset? (i.e., how many trips)
  * The size of the dataset is 983,648 rides.
  * bq query: 
    ```sql
    bq query --use_legacy_sql=false '
        SELECT count(*) AS Size
        FROM
           `bigquery-public-data.san_francisco.bikeshare_trips`'
```
  * Results:
  <br/>

| Size     | 
| :----------: | 
| 983,648  | 

  * What is the earliest start time and latest end time for a trip?
  * The earlist start time for a trip is August 29th, 2013 at 9:08AM UTC and the latest end time for a trip is August 31st, 2016 at 11:48PM UTC. 
  * bq query:
    ```sql
    bq query --use_legacy_sql=false '
        SELECT min(start_date) AS Earliest_Time, max(end_date) AS Latest_Time
        FROM
           `bigquery-public-data.san_francisco.bikeshare_trips`'
```
  * Results:
  <br/>

| Earliest_Time     | Latest_Time     | 
| :----------: | :----------: | 
| 2013-08-29 09:08:00  | 2016-08-31 23:48:00  | 

  * How many bikes are there?
  * There are 700 unique bikes.
  * bq query:
    ```sql
    bq query --use_legacy_sql=false '
        SELECT count(distinct bike_number) AS Num_Bikes
        FROM
           `bigquery-public-data.san_francisco.bikeshare_trips`'
```
  * Results:
  <br/>

| Num_Bikes     | 
| :----------: | 
| 700  | 

2. New Query (Run using bq and paste your SQL query and answer the question in a sentence, using properly formatted markdown):

  * How many trips are in the morning vs in the afternoon?
  * There are 412,339 morning trips and 571,309 evening trips, meaning there are 158,970 more trips in the evening than morning.

  * bq query: 
```sql
bq query --use_legacy_sql=false '
SELECT SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "12:00:00"
             THEN 1
             ELSE 0
         END
     ) AS Morning_Trips,
     SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) >= "12:00:00"
             THEN 1
             ELSE 0
         END
     ) AS Evening_Trips
     FROM `bigquery-public-data.san_francisco.bikeshare_trips`'
```

  * Results:
  <br/>
  
| Morining_Trips     | Evening_Trips     | 
| :----------: | :----------: | 
| 412,339  | 517,309  | 


### Project Questions
Identify the main questions you'll need to answer to make recommendations (list
below, add as many questions as you need).

- Question 1: How long is the average trip for subscribers?

- Question 2: What time of day / hour do most riders ride? - "peak riding hours"

- Question 3: What time of day / hour do most subscription riders ride? - "peak riding hours"

- Question 4: What is the average amount of bikes available per station during peak hours?

- Question 5: Do more customers that aren't subscribers ride a certain time of year?

- Question 6: How long to customers that aren't subscribers normally ride?

- Question 7: How far to subscribers travel on average at peak riding hours?

- Question 8: What are the most popular starting and ending stations during peak riding hours?

### Answers

Answer at least 4 of the questions you identified above You can use either
BigQuery or the bq command line tool.  Paste your questions, queries and
answers below.

- Question 1: How long is the average trip for subscribers?
  * Answer: The average duration of a subscriber's trip is about 10 minutes.
  * SQL query:
  ```sql
    SELECT AVG(duration_sec) AS Avg_Subscriber_Duration
        FROM `bigquery-public-data.san_francisco.bikeshare_trips`
        WHERE subscriber_type = "Subscriber"
    ```
| Row     | Avg_Subscriber_Duration     | 
| :----------: | :----------: | 
| 1  | 582.7642397197222  | 

- Question 2: What time of day / hour do most riders ride? - "peak riding hours"
  * Answer: Most riders ride from 7AM - 9AM in the morning and from 4PM - 6PM in the evening. This could mean that riders are biking to commute to and from work or school. There also were elevated ride times between 10AM - 3PM, which coinsides with daylight hours that are not during the high-voluming commuting times. This probably means people are more inclided to ride during the day, even if they aren't commuting to and from work or school.
  * SQL query:
  ```sql
  SELECT SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "1:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_12AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "2:00:00" AND time(CAST(start_date AS datetime) ) >= "1:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_1AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "3:00:00" AND time(CAST(start_date AS datetime) ) >= "2:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_2AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "4:00:00" AND time(CAST(start_date AS datetime) ) >= "3:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_3AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "5:00:00" AND time(CAST(start_date AS datetime) ) >= "4:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_4AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "6:00:00" AND time(CAST(start_date AS datetime) ) >= "5:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_5AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "7:00:00" AND time(CAST(start_date AS datetime) ) >= "6:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_6AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "8:00:00" AND time(CAST(start_date AS datetime) ) >= "7:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_7AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "9:00:00" AND time(CAST(start_date AS datetime) ) >= "8:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_8AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "10:00:00" AND time(CAST(start_date AS datetime) ) >= "9:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_9AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "11:00:00" AND time(CAST(start_date AS datetime) ) >= "10:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_10AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "12:00:00" AND time(CAST(start_date AS datetime) ) >= "11:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_11AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "13:00:00" AND time(CAST(start_date AS datetime) ) >= "12:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_12PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "14:00:00" AND time(CAST(start_date AS datetime) ) >= "13:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_1PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "15:00:00" AND time(CAST(start_date AS datetime) ) >= "14:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_2PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "16:00:00" AND time(CAST(start_date AS datetime) ) >= "15:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_3PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "17:00:00" AND time(CAST(start_date AS datetime) ) >= "16:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_4PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "18:00:00" AND time(CAST(start_date AS datetime) ) >= "17:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_5PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "19:00:00" AND time(CAST(start_date AS datetime) ) >= "18:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_6PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "20:00:00" AND time(CAST(start_date AS datetime) ) >= "19:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_7PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "21:00:00" AND time(CAST(start_date AS datetime) ) >= "20:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_8PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "22:00:00" AND time(CAST(start_date AS datetime) ) >= "21:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_9PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "23:00:00" AND time(CAST(start_date AS datetime) ) >= "22:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_10PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) >= "23:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_11PM
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    ```
  * Results: 
    <br/>
  
| Row     | Trips_12AM     | Trips_1AM     | Trips_2AM     |  Trips_3AM     |  Trips_4AM     |  Trips_5AM     |  Trips_6AM     | Trips_7AM     | Trips_8AM     |  Trips_9AM     |  Trips_10AM     |  Trips_11AM     |  Trips_12PM     |   Trips_1PM     |   Trips_2PM     |   Trips_3PM     |   Trips_4PM     |   Trips_5PM     |   Trips_6PM     |   Trips_7PM     |   Trips_8PM     |   Trips_9PM     |   Trips_10PM     |   Trips_11PM     | 
| :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: |
| 1  | 2929  |  1611  |  877  |  605  |  1398  |  5098  |  20519  |  67531  |  132464  |  96118  |  42782  |  40407  |  46950   | 43714  |  37852  |  47626  |  88755  |  126302  |  84569  |  41071  |  22747  |  15258  |  10270  |  6195  |

<br/>

- Question 3: What time of day / hour do most subscription riders ride? - "peak riding hours"
  * Answer: For subscribers, peak morning riding hours are 7AM - 9AM. Peak evening riding hours are 4PM - 6PM. This most likely corresponds to when riders are commuting to and from work or school.
  * SQL query:
  ```sql
  SELECT SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "1:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_12AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "2:00:00" AND time(CAST(start_date AS datetime) ) >= "1:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_1AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "3:00:00" AND time(CAST(start_date AS datetime) ) >= "2:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_2AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "4:00:00" AND time(CAST(start_date AS datetime) ) >= "3:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_3AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "5:00:00" AND time(CAST(start_date AS datetime) ) >= "4:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_4AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "6:00:00" AND time(CAST(start_date AS datetime) ) >= "5:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_5AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "7:00:00" AND time(CAST(start_date AS datetime) ) >= "6:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_6AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "8:00:00" AND time(CAST(start_date AS datetime) ) >= "7:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_7AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "9:00:00" AND time(CAST(start_date AS datetime) ) >= "8:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_8AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "10:00:00" AND time(CAST(start_date AS datetime) ) >= "9:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_9AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "11:00:00" AND time(CAST(start_date AS datetime) ) >= "10:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_10AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "12:00:00" AND time(CAST(start_date AS datetime) ) >= "11:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_11AM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "13:00:00" AND time(CAST(start_date AS datetime) ) >= "12:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_12PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "14:00:00" AND time(CAST(start_date AS datetime) ) >= "13:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_1PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "15:00:00" AND time(CAST(start_date AS datetime) ) >= "14:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_2PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "16:00:00" AND time(CAST(start_date AS datetime) ) >= "15:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_3PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "17:00:00" AND time(CAST(start_date AS datetime) ) >= "16:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_4PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "18:00:00" AND time(CAST(start_date AS datetime) ) >= "17:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_5PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "19:00:00" AND time(CAST(start_date AS datetime) ) >= "18:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_6PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "20:00:00" AND time(CAST(start_date AS datetime) ) >= "19:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_7PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "21:00:00" AND time(CAST(start_date AS datetime) ) >= "20:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_8PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "22:00:00" AND time(CAST(start_date AS datetime) ) >= "21:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_9PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) < "23:00:00" AND time(CAST(start_date AS datetime) ) >= "22:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_10PM,
        SUM(
         CASE
             WHEN time(CAST(start_date AS datetime) ) >= "23:00:00"
             THEN 1
             ELSE 0
         END
        ) AS Trips_11PM
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    WHERE subscriber_type = "Subscriber"
    ```
  * Results: 
    <br/>
  
| Row     | Trips_12AM     | Trips_1AM     | Trips_2AM     |  Trips_3AM     |  Trips_4AM     |  Trips_5AM     |  Trips_6AM     | Trips_7AM     | Trips_8AM     |  Trips_9AM     |  Trips_10AM     |  Trips_11AM     |  Trips_12PM     |   Trips_1PM     |   Trips_2PM     |   Trips_3PM     |   Trips_4PM     |   Trips_5PM     |   Trips_6PM     |   Trips_7PM     |   Trips_8PM     |   Trips_9PM     |   Trips_10PM     |   Trips_11PM     | 
| :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: | :----------: |  :----------: |
| 1  | 2081  |  972  |  464  |  397  |  1238  |  4795  |  19574  |  64946  |  127171  |  89546  |  34532  |  29329  |  34442   |  30995  |  25115  |  34820  |  76051  |  114915  |  75798  |  35515  |  19006  |  12450  |  7985  |  4702  |

<br/>

- Question 4: What is the average amount of bikes available per station during peak hours?
  * Answer: Stations with IDs 87, 32, and 91 have the least amount of bikes available during peak hours with an average of less than five bikes. This means that there's a risk of not having enough bikes available. Stations with IDs 90, 2, 77, and 50 have the most amount of bikes avaiable during peak hours with over 12 bikes avaiable on average. These stations have more capacity for increased ridership. 
  * SQL query:
  ```sql
  SELECT avg(bikes_available) AS Bikes_Avail, station_id
    FROM `bigquery-public-data.san_francisco.bikeshare_status`
    WHERE (time(CAST(time AS datetime) ) < "9:00:00" AND  time(CAST(time AS datetime) ) >= "7:00:00") OR (time(CAST(time AS datetime) ) < "18:00:00" AND  time(CAST(time AS datetime) ) >= "16:00:00")
    GROUP BY station_id
    ORDER BY Bikes_Avail
    ```
  
- Question 5: Do more customers that aren't subscribers ride a certain time of year?
  * Answer: Non-subscribing customers ride more often from May to October, with a maximum ridership of over 17,000 trips in September. This could mean that non subscribers ride in warmer months with more sunlight.
  * SQL query:
  ```sql
  SELECT  Count(*) AS Rides, EXTRACT(Month from Cast(start_date AS datetime)) AS Month
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    WHERE subscriber_type = "Customer"
    GROUP BY Month
    ORDER BY Month
    ```
- Question 6: How long do customers that aren't subscribers normally ride?
  * Answer: Non subscribers ride 62 minutes on average or close to an hour. This is important to call out because the average duration of subscriber rides is about 10 minutes. Promotions to target non-subscribers should could give discounts for longer rides.
  * SQL query:
  ```sql
  SELECT  avg(duration_sec) AS Avg_Duration
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    WHERE subscriber_type = "Customer"
    ```
  
- Question 7: What are the most popular starting and ending stations during peak riding hours?  
  * Answer: The most popular starting and ending stations are San Francisco Caltrain (Townsend and 4th) and San Francisco Caltrain 2 (330 Townsend) during peak hours. I also added in a filter to eliminate any trips that were to and from the same station. "Commuter trips" wouldn't begin and end at the same station, and I am trying to target the most popular commuter stations. 
  * SQL query:
```sql
SELECT  count(start_station_id) AS Start_Station_Count, start_station_name
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    WHERE ((time(CAST(start_date AS datetime) ) < "9:00:00" AND  time(CAST(start_date AS datetime) ) >= "7:00:00") OR (time(CAST(start_date AS datetime) ) < "18:00:00" AND  time(CAST(start_date AS datetime) ) >= "16:00:00")) AND start_station_id <> end_station_id
    GROUP BY start_station_name
    ORDER BY Start_Station_Count DESC
    
SELECT  count(end_station_id) AS End_Station_Count, end_station_name
    FROM `bigquery-public-data.san_francisco.bikeshare_trips`
    WHERE ((time(CAST(start_date AS datetime) ) < "9:00:00" AND  time(CAST(start_date AS datetime) ) >= "7:00:00") OR (time(CAST(start_date AS datetime) ) < "18:00:00" AND  time(CAST(start_date AS datetime) ) >= "16:00:00")) AND start_station_id <> end_station_id
    GROUP BY end_station_name
    ORDER BY End_Station_Count DESC
   ```
 
---

## Part 3 - Employ notebooks to synthesize query project results

### Get Going

Create a Jupyter Notebook against a Python 3 kernel named Project_1.ipynb in the assignment branch of your repo.

#### Run queries in the notebook 

At the end of this document is an example Jupyter Notebook you can take a look at and run.  

You can run queries using the "bang" command to shell out, such as this:

```
! bq query --use_legacy_sql=FALSE '<your-query-here>'
```

- NOTE: 
- Queries that return over 16K rows will not run this way, 
- Run groupbys etc in the bq web interface and save that as a table in BQ. 
- Max rows is defaulted to 100, use the command line parameter `--max_rows=1000000` to make it larger
- Query those tables the same way as in `example.ipynb`

Or you can use the magic commands, such as this:

```sql
%%bigquery my_panda_data_frame

select start_station_name, end_station_name
from `bigquery-public-data.san_francisco.bikeshare_trips`
where start_station_name <> end_station_name
limit 10
```

```python
my_panda_data_frame
```

#### Report in the form of the Jupter Notebook named Project_1.ipynb

- Using markdown cells, MUST definitively state and answer the two project questions:

  * What are the 5 most popular trips that you would call "commuter trips"? 
  
  * What are your recommendations for offers (justify based on your findings)?

- For any temporary tables (or views) that you created, include the SQL in markdown cells

- Use code cells for SQL you ran to load into Pandas, either using the !bq or the magic commands

- Use code cells to create Pandas formatted output tables (at least 3) to present or support your findings

- Use code cells to create simple data visualizations using Seaborn / Matplotlib (at least 2) to present or support your findings

### Resource: see example .ipynb file 

[Example Notebook](example.ipynb)

