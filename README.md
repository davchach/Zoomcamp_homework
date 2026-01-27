# Zoomcamp-homework

Homework module 1

Q1. 

docker run -it --entrypoint bash python:3.13
root@93a4f8f611d6:/# pip --version

Answer:
pip 25.3 from /usr/local/lib/python3.13/site-packages/pip (python 3.13)

Q2.

Hostname: db
Port: 5432
db:5432

Q3.

SELECT COUNT(*) AS short_trips
FROM public.green_tripdata_2025_11
WHERE lpep_pickup_datetime >= '2025-11-01'
  AND lpep_pickup_datetime <=  '2025-12-01'
  AND trip_distance <= 1;

Answer: 
"short_trips"
8007

Q4.

SELECT
  DATE(g."lpep_pickup_datetime") AS pickup_day,
  MAX(g."trip_distance")         AS longest_trip_distance
FROM public.green_tripdata_2025_11 g
WHERE g."trip_distance" < 100
GROUP BY 1
ORDER BY longest_trip_distance DESC;

Answer:
"pickup_day"	"longest_trip_distance"
"2025-11-14"	88.03

Q5.

SELECT
  z."Zone" AS pickup_zone,
  SUM(g."total_amount") AS total_amount_sum
FROM public.green_tripdata_2025_11 g
JOIN public.taxi_zone_lookup z
  ON g."PULocationID" = z."LocationID"
WHERE g."lpep_pickup_datetime" >= '2025-11-18'
  AND g."lpep_pickup_datetime" <  '2025-11-19'
GROUP BY z."Zone"
ORDER BY total_amount_sum DESC;

Answer:
"pickup_zone"	"total_amount_sum"
"East Harlem North"	9281.919999999996

Q6.

SELECT
  zd."Zone" AS dropoff_zone,
  MAX(g."tip_amount") AS max_tip_amount
FROM public.green_tripdata_2025_11 g
JOIN public.taxi_zone_lookup zp
  ON g."PULocationID" = zp."LocationID"
JOIN public.taxi_zone_lookup zd
  ON g."DOLocationID" = zd."LocationID"
WHERE zp."Zone" = 'East Harlem North'
  AND g."lpep_pickup_datetime" >= '2025-11-01'
  AND g."lpep_pickup_datetime" <  '2025-12-01'
GROUP BY zd."Zone"
ORDER BY max_tip_amount DESC;

Answer:
"dropoff_zone"	"max_tip_amount"
"Yorkville West"	81.89