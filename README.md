# Big Query SQL:
```
SELECT start_date,
    EXTRACT(HOUR FROM TIMESTAMP(started_at)) AS trip_start_hour,
    ROUND(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND) / 60.0, 1) AS trip_duration_minute
FROM `coogle-capstone-project.bike_rides.combined_table` limit 10;


CREATE TABLE `coogle-capstone-project.bike_rides.working` AS 
SELECT 
    start_date,
    CASE 
        WHEN EXTRACT(HOUR FROM TIMESTAMP(started_at)) = 0 THEN 24
        ELSE EXTRACT(HOUR FROM TIMESTAMP(started_at))
    END AS trip_start_hour,
    ROUND(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND) / 60.0, 1) AS trip_duration_minutes
FROM 
    `coogle-capstone-project.bike_rides.working``;

 ---  Create daily summary table

    SELECT start_date,
    trip_start_hour,
    count(*) as ride_count,
    min(trip_duration_minutes) min_duration,
     avg(trip_duration_minutes) as mean_duration,
     max(trip_duration_minutes) as max_duration
        FROM `coogle-capstone-project.bike_rides.working` 
        GROUP BY start_date,trip_start_hour;
```
