# MUSA-620-Week-7

Spacial databases continued / data reshaping with dplyr and tidyr ([notes](https://github.com/MUSA-620-Fall-2017/MUSA-620-Week-7/blob/master/week-7-data-frames-spatial-databases-continued.pptx))

![Fatal accidents in Philadelphia](https://blueshift.io/philly-accidents.png "Fatal accidents in Philadelphia")
The location of fatal traffic accidents in Philadelphia

### Queries used in class

*Joining Census data to the corresponding Census block group*

SELECT b.*, d.pop_total, d.pop_white, d.pop_black, d.pop_nativeamerican, d.pop_asian
FROM pa_block_group AS b
LEFT JOIN block_group_population AS d
ON b.gisjoin = d.gisjoin
WHERE b.countyfp = '101'


*Spatial join: for each Philadelphia Census block, find the distance of the nearest SEPTA rail station*

SELECT DISTINCT ON (b.gid) b.*, ST_Distance(b.geom, s.geom) as distance_to_station
FROM pa_block_group AS b, dvrpc_passenger_rail_stations AS s
WHERE b.countyfp = '101'
ORDER BY b.gid, ST_Distance(b.geom, s.geom)



