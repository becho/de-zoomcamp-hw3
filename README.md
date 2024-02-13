### homework 3
#### Below the code that I use to do the hw3. I use GCS Bucket and BigQuery Service from GCP to execute this.

CREATE OR REPLACE EXTERNAL TABLE `ny_taxi.external_gtd_2022`
OPTIONS(
  FORMAT = 'PARQUET',
  URIS = ['gs://mage-zoomcamp-santos/green_tripdata_2022-*.parquet']
);

CREATE OR REPLACE TABLE `ny_taxi.green_taxi_data_2022` AS
SELECT * FROM `ny_taxi.external_gtd_2022`;

select count(1) from `ny_taxi.external_gtd_2022`;

select count(distinct  PULocationID) from `ny_taxi.external_gtd_2022`;
select count(distinct  PULocationID) from `ny_taxi.green_taxi_data_2022`;

select count(1) from `ny_taxi.green_taxi_data_2022` where fare_amount = 0;

CREATE OR REPLACE TABLE `ny_taxi.gtd_2022_partitioned_clustered`
PARTITION BY DATE(lpep_pickup_datetime)
CLUSTER BY PULocationID AS
SELECT * FROM `ny_taxi.green_taxi_data_2022`;


SELECT DISTINCT PULocationID FROM `ny_taxi.green_taxi_data_2022`
WHERE DATE(lpep_pickup_datetime) BETWEEN '2022-06-01' AND '2022-06-30'; 

SELECT DISTINCT PULocationID FROM `ny_taxi.gtd_2022_partitioned_clustered`
WHERE DATE(lpep_pickup_datetime) BETWEEN '2022-06-01' AND '2022-06-30'; 

