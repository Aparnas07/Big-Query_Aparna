1.	To find the most popular Citibike stations for starting trips:
'''SQL
SELECT start_station_id, COUNT(*) AS trip_count
FROM `bigquery-public-data.new_york_citibike.citibike_trips`
GROUP BY start_station_id
ORDER BY trip_count DESC
LIMIT 10;
'''
![image](https://github.com/Aparnas07/Big-Query_Aparna/assets/159004909/dd46f8b6-a97f-4aa7-b8f0-6d85c5045930)

2.	To identify the busiest months for Citibike usage
3.	'''SQL
4.	SELECT
  EXTRACT(MONTH FROM starttime) AS month,
  COUNT(*) AS trip_count
FROM `bigquery-public-data.new_york_citibike.citibike_trips`
GROUP BY month
ORDER BY trip_count DESC;

'''![image](https://github.com/Aparnas07/Big-Query_Aparna/assets/159004909/ef674e29-88d2-45ce-8b90-a14fec281bc0)

3. To Compare bike usage between genders during rush hour
4. '''SQL
5. SELECT
  gender,
  COUNT(*) AS trip_count
FROM `bigquery-public-data.new_york_citibike.citibike_trips`
WHERE
  EXTRACT(HOUR FROM starttime) IN (7, 8, 17, 18)
GROUP BY gender
ORDER BY gender;

'''![image](https://github.com/Aparnas07/Big-Query_Aparna/assets/159004909/cc8ecd4d-ae31-478d-b0c6-303c842a8764)

4. To find the most common trip routes taken by users
5. '''SQL
6. SELECT
  start_station_id,
  end_station_id,
  COUNT(*) AS trip_count
FROM `bigquery-public-data.new_york_citibike.citibike_trips`
GROUP BY start_station_id, end_station_id
ORDER BY trip_count DESC
LIMIT 10

'''![image](https://github.com/Aparnas07/Big-Query_Aparna/assets/159004909/fe1e12ec-c781-4273-8cb8-646d4e103ef4)

5.	To identify the most frequent bike user types:
6.	'''SQL
7.	
6.	SELECT
7.	  usertype,
8.	  COUNT(*) AS trip_count
9.	FROM `bigquery-public-data.new_york_citibike.citibike_trips`
10.	GROUP BY usertype
11.	ORDER BY trip_count DESC
12.	LIMIT 10;

13.	'''![image](https://github.com/Aparnas07/Big-Query_Aparna/assets/159004909/7bc4656e-32f9-4fab-9bad-eeed45cacfcc)

14.	6. TO Compare bike usage between subscription and casual riders during peak hours
15.	'''SQL
16.	
SELECT
  usertype,
  COUNT(*) AS trip_count
FROM `bigquery-public-data.new_york_citibike.citibike_trips`
WHERE EXTRACT(HOUR FROM starttime) IN (7, 8, 17, 18)
GROUP BY usertype;

'''![image](https://github.com/Aparnas07/Big-Query_Aparna/assets/159004909/d847159f-4e49-4879-bebb-a603f44c5d31)


7. To find the busiest weekdays and weekends for Citibike usage throughout the year
8. '''SQL
9. SELECT
  CASE
    WHEN EXTRACT(DAYOFWEEK FROM starttime) IN (2, 3, 4, 5) THEN 'Weekday'
    ELSE 'Weekend'
  END AS day_type,
  EXTRACT(DATE FROM starttime) AS trip_date,
  COUNT(*) AS trip_count
FROM `bigquery-public-data.new_york_citibike.citibike_trips`
GROUP BY day_type, trip_date
ORDER BY day_type, trip_count DESC;

'''![image](https://github.com/Aparnas07/Big-Query_Aparna/assets/159004909/ad322502-91be-4b70-9c80-4addaba04108)

8. To find the most popular origin-destination station pairs for Citibike trips
9. '''SQL
10. SELECT 
  start_station_id, 
  start_station_name,
  end_station_id,
  end_station_name,
  COUNT(*) AS trip_count
FROM `bigquery-public-data.new_york_citibike.citibike_trips`
GROUP BY start_station_id, start_station_name, end_station_id, end_station_name
ORDER BY trip_count DESC
LIMIT 10

'''![image](https://github.com/Aparnas07/Big-Query_Aparna/assets/159004909/d4d8d871-5b7e-4119-b6f8-796a66552760)

9. To find countries with total fertility rates in a specific year
10. '''SQL
11. SELECT afr.country_name, afr.total_fertility_rate
FROM `bigquery-public-data.census_bureau_international.age_specific_fertility_rates` AS afr
JOIN `bigquery-public-data.census_bureau_international.birth_death_growth_rates` AS bdg
ON afr.country_name = bdg.country_name
AND afr.year = bdg.year
WHERE afr.year = 2020
ORDER BY afr.total_fertility_rate DESC
LIMIT 10;

SELECT afr.country_name, afr.total_fertility_rate
FROM `bigquery-public-data.census_bureau_international.age_specific_fertility_rates` AS afr
JOIN `bigquery-public-data.census_bureau_international.birth_death_growth_rates` AS bdg
ON afr.country_name = bdg.country_name
AND afr.year = bdg.year
WHERE afr.year = 2020
ORDER BY afr.total_fertility_rate ASC
LIMIT 10;

'''![image](https://github.com/Aparnas07/Big-Query_Aparna/assets/159004909/94c3df3f-879d-450a-b393-056b1787e849)


10. Identify areas with the highest proportion of trees in poor health
11. '''SQL
12. SELECT zip_city, COUNT(*) AS total_trees, COUNT(CASE WHEN health = 'Poor' THEN 1 END) AS poor_trees,
  CAST(COUNT(CASE WHEN health = 'Poor' THEN 1 END) / COUNT(*) * 100 AS FLOAT64) AS percent_poor
FROM `bigquery-public-data.new_york_trees.tree_census_2015`
GROUP BY zip_city
ORDER BY percent_poor DESC
LIMIT 5;

'''![image](https://github.com/Aparnas07/Big-Query_Aparna/assets/159004909/8ae35c41-ede4-4f14-a90a-f5267a8ed9f7)









