![CyclisticLogo](https://github.com/towhidrazu/Cyclistic_Bike_Share/blob/main/Cyclistic.jpg)

# Cyclistic_Bike_Share
Cyclistic Bike_Share- Data analysis with SQL &amp; Power BI


## INTRODUCTION
This is the final project in my Google Data Analytics Professional Certificate course. In this case study I will be analyzing a public dataset for a fictional company provided by the course. I will be using SQL & Power BI for this analysis. This is because SQL can handle large amount of data (5+ million rows of data in this project) very easily and Power BI is a very useful data visualization tool.

Data set for case study can be found here [Cyclistic Trip Data Download](https://divvy-tripdata.s3.amazonaws.com/index.html).

The data has been made available by Motivate International Inc. under this [license](https://www.divvybikes.com/data-license-agreement).

## BACKGROUND INFORMATION

### Scenario

fictitiously I am wirkign as data analyst in the marketing analyst team at Cyclistic, a bike-share compnay in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, my team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, my team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.

### About the company

In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of more than 600 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.

The company's marketing strategy relied on creating general awareness and appealing to broad consumer segments. The flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships help the company to attract more consumers and achieve its goal.

Cyclistic refers to its customers as 'casual' rides who purchase single-ride or full-day passes and as 'members' who purchase an annual subscription.

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Moreno believes that maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a very good chance to convert casual riders into members.


### Characters and teams

* Cyclistic:  A bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.

* Lily Moreno: The director of marketing and manager. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels.

* Cyclistic marketing analytics team: A team of data analysts who are responsible for collecting, analyzing, and reporting data that helps guide Cyclistic marketing strategy.

* Cyclistic executive team: The notoriously detail-oriented executive team will decide whether to approve the recommended marketing program.
Consumers can purchase access to Cylictic bikes using three options:

_The case study follows the six step data analysis process:_

### ❓ [Ask](#step-1-ask)
### 💻 [Prepare](#step-2-prepare)
### 🛠 [Process](#step-3-process)
### 📊 [Analyze](#step-4-analyze)
### 📋 [Share](#step-5-share)
### 🧗‍♀️ [Act](#step-6-act)

## Step 1: Ask

[Back to top](#introduction)

Three questions will guide the future marketing program:
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

**Moreno** (the director of marketing and my manager) has assigned me the first question to answer:

**How do annual members and casual riders use Cyclistic bikes differently?**

**Key tasks**

1. Identify the business task
   
* Finding out the difference in bike use between annual members and casual riders.

2. Consider key stakeholders
- Director of Marketing & my manager (Lily Moreno), Marketing Analytics team (The team where I belong to)

**Deliverable**

**A clear statement of the business task**

For completion of the business task our effort should be answering the following questions:

- What is the total numbers of rides of the both types of users?
- What is the total and average ride duration of the both types of users?
- What is the total numbers of rides, total and average ride duration of both types of users based on the day of the week and based of the month of the year?
- What is the numbers of riders per hour for both types of users?
- What is the peak hour for both types of users?
- What are mostly used stations for both types of users?
- Which bikes are preferred  by the users?
- Between weekdays and weekend when both types of users use bikes most?


## Step 2: Prepare

[Back to top](#introduction)

I will use Cyclistic’s historical trip data to analyze and identify trends. Link for Cyclistic trip data and information about license is given above.

**Key tasks**

1. Download data and store it appropriately.
* Data has been downloaded and stored on my computer. A copy of the data has been produced to work with.

2. Identify how it’s organized.
* The data is organized in CSV (comma-separated values) format under zip file.

3. Sort and filter the data.
* For the purpose of my analysis I have downloaded most recent 12 months file (October 2022 to September 2023). Unzip those and organize those in a separate folder.

4. Determine the credibility of the data
* For the purpose of this case study, the datasets are appropriate and will enable me to answer the business questions. But data-privacy issues will prohibit me from using rider's personally identifiable information and this will prevent me from determining if casual riders live in the
Cyclistic service area or if riders have purchased multiple single passes.


**Deliverable**

**A description of all data sources used**

* Source of data: [Cyclistic Trip Data Download](https://divvy-tripdata.s3.amazonaws.com/index.html)

**CREATING TABLE OF 13 COLUMNS TO IMPORT DATA FROM CSV FILES TO POSTGRE SQL**

```
# CODES for creating table with ride_id as Primary Key:

CREATE TABLE october (  

ride_id VARCHAR(50),  

rideable_type TEXT,  

started_at TIMESTAMP,  

ended_at TIMESTAMP,  

start_station_name VARCHAR(100),  

start_station_id VARCHAR(100),  

end_station_name VARCHAR (100),  

end_station_id VARCHAR (100),  

start_lat DECIMAL,  

start_lng DECIMAL,  

end_lat DECIMAL,  

end_lng DECIMAL,  

member_casual TEXT,  

PRIMARY KEY (ride_id))
```


**COPY data from CSV FILE TO newly created table**

It is mentionable that in the table named 'october' we have loaded only data of october. In next step we will add rest 11 months data in this 'october' table. Then we will rename the 'october' table as 'fullyear'.

```
COPY october(ride_id, rideable_type, started_at, ended_at, start_station_name,  

start_station_id, end_station_name, end_station_id, start_lat,  start_lng, end_lat, end_lng, member_casual)  

FROM 'E:\cyclistic\202210-divvy-tripdata.csv'  # location of CSV file in computer

DELIMITER ','  

CSV HEADER  # As CSV file containes header row
```

**To view first few rows of the whole table**

Now that I have imported october 2022 data to my newly created SQL table I will be using, I will take a look at at a glance to familiarize myself with the data and to check for errors.

```
SELECT *  

FROM october  

LIMIT 10
```

**Add November & subsequest months (11 months) data to existing table named october (This way we bring all 12 months (October 2022 to September 2023) data under 1 table)**

```
From PGadmin right click on table named October -> import/export data -> Under General from File Name,

select the CSV file -> From Options, turn on Header -> Press Ok  

# Note: This can also be done using Union All command after creating & importing data for each month's table.
```


**Renaming 'october' table as 'fullyear' table**

```
ALTER TABLE october RENAME TO fullyear
```


**Make a duplicate table named 'fullyear_backup' from existing table 'fullyear' in case we need in future**

```
CREATE TABLE fullyear_backup AS TABLE fullyear
```

## Step 3: Process

[Back to top](#introduction)

For this analysis I will be using SQL (PostgreSQL) and Power BI.

The whole 12 months of data contains 5+ millions of rows making it a huge dataset. To work with such a hugh dataset efficiently SQL is one of the best options as it can handle massive amount of data in good pace.

For visualization part I will be using MS Power BI which is a very widely used and powerful business intelligence tool and can produce effective visualizations.

**Deliverable**

**Documentation of any cleaning or manipulation of data**

Checking no. of rows in full year table

```
SELECT COUNT(*)
FROM fullyear

Ans: 5674399
```

Now I will check whether this dataset contains any duplicate entry based on column 'ride_id'

```
SELECT ride_id, COUNT(*)
FROM fullyear1
GROUP BY ride_id
HAVING COUNT(*) > 1

Result: null

# Thus, this dataset doesn't contain any duplicate value.
```

Now I will check whether this dataset contains any negative, zero or extremely large ride length (more than 24 hours) value

```
SELECT ride_id, (ended_at - started_at) AS ride_length
FROM fullyear
WHERE (ended_at - started_at) < '00:00:01' OR (ended_at - started_at) > '24:00:00'
ORDER BY ride_length

# From 17640 resulted values I can see this dataset containes 11695 negative and zero value.
And rest 5945 row contains ride length more than 24 hours.
These might happen due to testing or checking pupose.
Or this could happen due to any error.

For the purpose of our study we will discard those 17640 values from analysis. These are 0.31% of the total data.
```

**Creating a new table named fullyear1 for analysis with 5 new columns (ride_length, day_of_week, day_name, month_of_year, month_name) in addition to original columns filtering out ride length from 1 second to 24 hours.**

```
CREATE TABLE fullyear1 AS ( 

SELECT *, (ended_at - started_at) AS ride_length, EXTRACT('DOW' FROM started_at) AS day_of_week,  

CASE WHEN EXTRACT('DOW' FROM started_at) = '0' THEN 'Sunday' 

     WHEN EXTRACT('DOW' FROM started_at) = '1' THEN 'Monday' 

 WHEN EXTRACT('DOW' FROM started_at) = '2' THEN 'Tuesday' 

 WHEN EXTRACT('DOW' FROM started_at) = '3' THEN 'Wednesday' 

 WHEN EXTRACT('DOW' FROM started_at) = '4' THEN 'Thursday' 

 WHEN EXTRACT('DOW' FROM started_at) = '5' THEN 'Friday' 

 WHEN EXTRACT('DOW' FROM started_at) = '6' THEN 'Saturday' 

 END AS day_name,  

 EXTRACT('MON' FROM started_at) AS month_of_year, 

CASE WHEN EXTRACT('MON' FROM started_at) = '1' THEN 'January' 

 WHEN EXTRACT('MON' FROM started_at) = '2' THEN 'February' 

 WHEN EXTRACT('MON' FROM started_at) = '3' THEN 'March' 

 WHEN EXTRACT('MON' FROM started_at) = '4' THEN 'April' 

 WHEN EXTRACT('MON' FROM started_at) = '5' THEN 'May' 

 WHEN EXTRACT('MON' FROM started_at) = '6' THEN 'June' 

 WHEN EXTRACT('MON' FROM started_at) = '7' THEN 'July' 

 WHEN EXTRACT('MON' FROM started_at) = '8' THEN 'August' 

 WHEN EXTRACT('MON' FROM started_at) = '9' THEN 'September' 

 WHEN EXTRACT('MON' FROM started_at) = '10' THEN 'October' 

 WHEN EXTRACT('MON' FROM started_at) = '11' THEN 'November' 

 WHEN EXTRACT('MON' FROM started_at) = '12' THEN 'December' 

END AS month_name 

FROM fullyear 

WHERE (ended_at - started_at) BETWEEN '00:00:01' AND '24:00:00' 

ORDER BY started_at) 
```

*** Let's have a quick look on first 10 rows of data**

```
SELECT *
FROM fullyear1
LIMIT 10
```
![TopTenRows](https://github.com/towhidrazu/Cyclistic_Bike_Share/blob/main/TopTenRows.png)

**Now our dataset fullyear1 is ready to analyze. Thus we proceed to ANALYZE section.**


## Step 4: Analyze

[Back to top](#introduction)

**All the required data are now in one SQL table 'fullyear1' and ready for exploration.**

Our Analyze section comprises of answering all the questions we framed in Ask (step 1) phase to attain business task.

**What is the total numbers of rides of the both types of users?**

```
SELECT member_casual AS member_type, count(*)
FROM fullyear1
GROUP BY member_casual

RESULT:

Casual: 2077387
Member: 3579372
```

**What is the total ride duration of the both types of users?**

```
SELECT member_casual AS member_type, sum(ride_length)
FROM fullyear1
GROUP BY member_casual

RESULT:

Casual: 1 day 713964:46:09
Member:	720377:57:18
```

**What is the average ride duration of the both types of users?**

```
SELECT member_casual AS member_type, avg(ride_length)
FROM fullyear1
GROUP BY member_casual

RESULT:

Casual: 00:20:37.304156
Member: 00:12:04.529509

```
**What is the total numbers of rides of both types of users based on the day of the week?**

```
SELECT *
FROM crosstab('SELECT day_name, member_casual AS rider_type, COUNT(*) AS rides
FROM fullyear1
GROUP BY day_name, member_casual
ORDER BY CASE
	WHEN day_name = ''Sunday'' THEN 1
	WHEN day_name = ''Monday'' THEN 2
	WHEN day_name = ''Tuesday'' THEN 3
	WHEN day_name = ''Wednesday'' THEN 4
	WHEN day_name = ''Thursday'' THEN 5
	WHEN day_name = ''Friday'' THEN 6
	WHEN day_name = ''Saturday'' THEN 7
	END                                  # Custom Sorting
	, member_casual'
	, 'values (''casual''), (''member'')')
	AS (day_name text, casual bigint, member bigint)


RESULT:
 day_name       casual  member
"Sunday"	337183	400790
"Monday"	236159	485185
"Tuesday"	239686	552590
"Wednesday"	248298	569899
"Thursday"	272968	573983
"Friday"	315502	519058
"Saturday"	427591	477867
```

**What is the total rides duration of both types of users based on the day of the week?**

```
SELECT *
FROM crosstab('SELECT day_name, member_casual AS rider_type, SUM(ride_length) AS rides
FROM fullyear1
GROUP BY day_name, member_casual
ORDER BY CASE
	WHEN day_name = ''Sunday'' THEN 1
	WHEN day_name = ''Monday'' THEN 2
	WHEN day_name = ''Tuesday'' THEN 3
	WHEN day_name = ''Wednesday'' THEN 4
	WHEN day_name = ''Thursday'' THEN 5
	WHEN day_name = ''Friday'' THEN 6
	WHEN day_name = ''Saturday'' THEN 7
	END                                      # Custom Sorting
	, member_casual'
	, 'values (''casual''), (''member'')')
	AS (day_name text, casual interval, member interval)

RESULT:
day_name             casual        member
"Sunday"	"134524:21:02"	"89840:23:48"
"Monday"	"79698:37:26"	"92734:24:58"
"Tuesday"	"73127:25:28"	"106528:27:55"
"Wednesday"	"1 day 72180:13:29"	"109195:33:43"
"Thursday"	"82291:27:18"	"110587:35:58"
"Friday"	"105656:17:24"	"104268:03:13"
"Saturday"	"166486:24:02"	"107223:27:43"
```

**What is the average rides duration of both types of users based on the day of the week?**

```
SELECT *
FROM crosstab('SELECT day_name, member_casual AS rider_type, AVG(ride_length) AS rides
FROM fullyear1
GROUP BY day_name, member_casual
ORDER BY CASE
	WHEN day_name = ''Sunday'' THEN 1
	WHEN day_name = ''Monday'' THEN 2
	WHEN day_name = ''Tuesday'' THEN 3
	WHEN day_name = ''Wednesday'' THEN 4
	WHEN day_name = ''Thursday'' THEN 5
	WHEN day_name = ''Friday'' THEN 6
	WHEN day_name = ''Saturday'' THEN 7
	END                                   # Custom Sorting
	, member_casual'
	, 'values (''casual''), (''member'')')
	AS (day_name text, casual interval, member interval)

RESULT:

day_name             casual                  member
"Sunday"	"00:23:56.275441"	"00:13:26.969805"
"Monday"	"00:20:14.923192"	"00:11:28.075472"
"Tuesday"	"00:18:18.348372"	"00:11:34.009075"
"Wednesday"	"00:17:26.867913"	"00:11:29.778405"
"Thursday"	"00:18:05.289257"	"00:11:33.601305"
"Friday"	"00:20:05.579185"	"00:12:03.165798"
"Saturday"	"00:23:21.69237"	"00:13:27.765472"
```

**What is the total numbers of rides of both types of users based on the months of the year?**

```
SELECT *
FROM crosstab('SELECT month_name, member_casual, COUNT(*) AS rides
FROM fullyear1
GROUP BY month_name, member_casual
ORDER BY array_position(array[''January'',''February'',''March'',''April'',
			  ''May'',''June'', ''July'',''August'',''September'',''October''
			  ,''November'',''December''],month_name)                             #Custom sorting
			   , member_casual'
	, 'values (''casual''), (''member'')')
	AS (month_name text, casual bigint, member bigint)

RESULT:
month_name      casual  member
"January"	39917	150258
"February"	42930	147397
"March"	        62067	196432
"April"	        146974	279241
"May"	        229785	363718
"June"	        300517	418249
"July"	        330334	436039
"August"	310040	460240
"September"	260819	404473
"October"	208639	349559
"November"	100570	236891
"December"	44795	136875
```

**What is the total rides duration of both types of users based on the months of the year?**

```
SELECT *
FROM crosstab('SELECT month_name, member_casual, SUM(ride_length) AS rides
FROM fullyear1
GROUP BY month_name, member_casual
ORDER BY array_position(array[''January'',''February'',''March'',''April'',
			  ''May'',''June'', ''July'',''August'',''September'',''October''
			  ,''November'',''December''],month_name)                       #Custom sorting
			  , member_casual'
	, 'values (''casual''), (''member'')')
	AS (month_name text, casual interval, member interval)

RESULT:
month_name        casual            member
"January"	"9114:32:16"	"25206:25:17"
"February"	"11462:24:48"	"25703:08:17"
"March"	        "15883:58:37"	"33368:30:08"
"April"	        "50729:45:38"	"53335:36:30"
"May"	    "1 day 86287:37:00"	"77575:42:00"
"June"   	"109023:39:31"	"89597:47:01"
"July"	        "125904:07:32"	"95906:48:44"
"August"	"113316:33:56"	"100967:35:47"
"September"	"91951:29:36"	"85070:57:35"
"October"	"64229:43:31"	"67200:03:20"
"November"	"26056:23:38"	"42863:03:55"
"December"	"10004:30:06"	"23582:18:44"

```

**What is the average rides duration of both types of users based on the months of the year?**

```
SELECT *
FROM crosstab('SELECT month_name, member_casual, AVG(ride_length) AS rides
FROM fullyear1
GROUP BY month_name, member_casual
ORDER BY array_position(array[''January'',''February'',''March'',''April'',
			  ''May'',''June'', ''July'',''August'',''September'',''October''
			  ,''November'',''December''],month_name)      #Custom sorting
			  , member_casual'
	, 'values (''casual''), (''member'')')        
	AS (month_name text, casual interval, member interval)


RESULT:

month_name           casual                  member
"January"	"00:13:42.014079"	"00:10:03.915379"
"February"	"00:16:01.208665"	"00:10:27.769202"
"March"	        "00:15:21.299837"	"00:10:11.542967"
"April"	        "00:20:42.581259"	"00:11:27.607443"
"May"	        "00:22:32.228475"	"00:12:47.827053"
"June"	        "00:21:46.033173"	"00:12:51.196156"
"July"	        "00:22:52.110809"	"00:13:11.820282"
"August"	"00:21:55.764534"	"00:13:09.769136"
"September"	"00:21:09.176617"	"00:12:37.171566"
"October"	"00:18:28.263608"	"00:11:32.072583"
"November"	"00:15:32.713712"	"00:10:51.384118"
"December"	"00:13:24.022904"	"00:10:20.247116"

```
