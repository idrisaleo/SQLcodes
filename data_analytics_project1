-- getting an overview 
SELECT *
FROM GoogleProject..april

-- selecting useful columns 

SELECT ride_id, rideable_type, started_at, 
       ended_at, ABS(DATEDIFF(minute, started_at, ended_at))  AS trip_min,
	   ABS(DATEDIFF(minute, started_at, ended_at))/60 AS trip_hour,
	   DATENAME(WEEKDAY, "started_at") as day_of_week,
	   start_station_name, end_station_name, member_casual
FROM GoogleProject..april
ORDER BY trip_min DESC

-- merge tables
CREATE VIEW MembersRidePattern AS
SELECT april.ride_id, april.rideable_type, may.start_station_name, may.end_station_name, may.member_casual, 
       ABS(DATEDIFF(minute, april.started_at, april.ended_at))  AS trip_min,
	   ABS(DATEDIFF(minute, april.started_at, april.ended_at))/60  AS trip_hour
FROM GoogleProject..april april
INNER JOIN GoogleProject..may may
ON april.start_station_id = may.start_station_id
ORDER BY trip_min DESC


CREATE VIEW vis_tab AS
SELECT ride_id, rideable_type, started_at, 
       ended_at, ABS(DATEDIFF(minute, started_at, ended_at))  AS trip_min,
	   ABS(DATEDIFF(minute, started_at, ended_at))/60 AS trip_hour,
	   start_station_name, end_station_name, member_casual
FROM GoogleProject..april
