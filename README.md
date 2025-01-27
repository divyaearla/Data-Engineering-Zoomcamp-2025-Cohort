# Data-Engineering-Zoomcamp-2025-Cohort

Home work :

Week 1

Q1 : 
docker run -it --entrypoint bash python:3.12.8
pip --version

Q3: 
select count(*) from public.green_tripdata_2019 where trip_distance <= 1 
select count(*) from public.green_tripdata_2019 where trip_distance >1 and trip_distance <= 3 
select count(*) from public.green_tripdata_2019 where trip_distance >3 and trip_distance <= 7 
select count(*) from public.green_tripdata_2019 where trip_distance >7 and trip_distance <= 10
select count(*) from public.green_tripdata_2019 where trip_distance > 10 

Q4:
select date(lpep_pickup_datetime) from public.green_tripdata_2019 where trip_distance = (select max(trip_distance) from public.green_tripdata_2019) 

Q5: 
SELECT 
  distinct "Zone" 
FROM 
  public.zones 
WHERE 
  "LocationID" IN (
    SELECT 
      "PULocationID" 
    FROM 
      public.green_tripdata_2019 
    WHERE 
      DATE(lpep_pickup_datetime) = '2019-10-18' 
    GROUP BY 
      "PULocationID" 
    HAVING 
      SUM(total_amount) > 13000
  );

  
Q6:

SELECT "Zone" 
FROM public.zones 
WHERE "LocationID" = (
  SELECT "DOLocationID" 
  FROM public.green_tripdata_2019 
  WHERE 
    "PULocationID" = (SELECT "LocationID" FROM public.zones WHERE "Zone" = 'East Harlem North') 
    AND DATE_TRUNC('month', lpep_pickup_datetime) = '2019-10-01' 
  ORDER BY "tip_amount" DESC 
  LIMIT 1
);


