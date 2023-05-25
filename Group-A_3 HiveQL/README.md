DSBDAL Practical No: 3 Hive SQL Queries:

-- If Hive is not open, change the metastore_db file name to metastore_db_bkp
-- Run the following commands to install the Derby database
schematool -initSchema -dbType derby

-- Open terminal and start Hive
-- stop-all.sh
-- start-all.sh
-- hive
-- cd $HIVE_HOME
-- cd bin
-- hive
-- Browser - http://localhost:9870/

-- Create Database flights_data
CREATE DATABASE flight_data;

-- Create table flights
CREATE TABLE flights1 (
  flight_date DATE,
  airline_code INT,
  carrier_code STRING,
  origin STRING,
  dest STRING,
  depart_time INT,
  depart_delta INT,
  depart_delay INT,
  arrive_time INT,
  arrive_delta INT,
  arrive_delay INT,
  is_cancelled BOOLEAN,
  cancellation_code STRING,
  distance INT,
  carrier_delay INT,
  weather_delay INT,
  nas_delay INT,
  security_delay INT,
  late_aircraft_delay INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE;

-- Create table airlines
CREATE TABLE airlines1 (
  code INT,
  description STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE;

-- Create table carriers
CREATE TABLE carriers1 (
  code INT,
  description STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE;

-- Create table cancellation_reasons
CREATE TABLE cancellation_reasons1 (
  code INT,
  description STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE;

-- Load the dataset files
LOAD DATA LOCAL INPATH '${env:HOME}/flight_data/ontime_flights.tsv' OVERWRITE INTO TABLE flights1;
LOAD DATA LOCAL INPATH '${env:HOME}/flight_data/airlines.tsv' OVERWRITE INTO TABLE airlines1;
LOAD DATA LOCAL INPATH '${env:HOME}/flight_data/carriers.tsv' OVERWRITE INTO TABLE carriers1;
LOAD DATA LOCAL INPATH '${env:HOME}/flight_data/cancellation_reasons.tsv' OVERWRITE INTO TABLE cancellation_reasons1;

-- Perform join operations
SELECT a.description, AVG(f.depart_delay)
FROM airlines1 a
JOIN flights1 f ON a.code = f.airline_code
GROUP BY a.description;

SELECT c.description, AVG(f.depart_delay)
FROM carriers1 c
JOIN flights1 f ON c.code = f.carrier_code
GROUP BY c.description;

