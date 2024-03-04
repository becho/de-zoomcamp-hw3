SELECT count(1), PUlocationID
FROM `stunning-maxim-411319.ny_tripdata_all.fhv_trips_201910` 
where PUlocationID is not null
group by PUlocationID
order by 1 asc

SELECT *
FROM `stunning-maxim-411319.dbt_vsantos.dim_zones` 
order by locationid
