NYC Citibike Dashboard Performance Powered by Looker Studio
This project is a part of the learning of Business Intelligence Analyst in Binar Bootcamp Academy

WITH data as (SELECT tripduration,
starttime,
stoptime,
start_station_id,
start_station_name,
start_station_latitude,
start_station_longitude,
end_station_id,
end_station_name,
end_station_latitude,
end_station_longitude,
bikeid,
usertype,
birth_year,
gender,
customer_plan FROM `bigquery-public-data.new_york_citibike.citibike_trips`
WHERE tripduration is not null and birth_year is not null and birth_year > 1948 and gender != "unkown")
SELECT *,
2017-birth_year as age,
CASE WHEN 2017-birth_year between 0 and 10 then "0 - 10" 
when 2017-birth_year between 11 and 20 then "11 - 20" 
when 2017-birth_year between 21 and 30 then "21 - 30" 
when 2017-birth_year between 31 and 40 then "31 - 40" 
when 2017-birth_year between 41 and 50 then "41 - 50" 
when 2017-birth_year between 51 and 60 then "51 - 60" 
else "61+" end as age_category,
ROUND(SUM(tripduration/60),2) AS tripduration_minute,
ROUND(SUM(tripduration/3600),2) AS tripduration_hour,
FROM data
GROUP BY tripduration, 
starttime,
stoptime,
start_station_id,
start_station_name,
start_station_latitude,
start_station_longitude,
end_station_id,
end_station_name,
end_station_latitude,
end_station_longitude,
bikeid,
usertype,
birth_year,
gender,
customer_plan
