# README

A music streaming startup, Sparkify, has grown their user base and song database
even more and want to move their data warehouse to a data lake. Their data
resides in S3, in a directory of JSON logs on user activity on the app, as well
as a directory with JSON metadata on the songs in their app.

As their data engineer, you are tasked with building an ETL pipeline that
extracts their data from S3, processes them using Spark, and loads the data back
into S3 as a set of dimensional tables. This will allow their analytics team to
continue finding insights in what songs their users are listening to.

This project builds an ETL pipeline for a data lake hosted on S3. Data is loaded
from S3, processed into analytics tables using Spark, and loaded back into S3.
The Spark process is deployed on a cluster using AWS.

## Data

The data for this project is available on Amazon S3.

- Song data: s3://udacity-dend/song_data
- Log data: s3://udacity-dend/log_data

Sample data is available in the `data/` folder.

### Log Data

The JSON logs on user activity have the following structure.

![log data](log-data.png)

### Song Data

Below is an example of what a single song file, TRAABJL12903CDCF1A.json looks
like.

```JSON
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null,
"artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud",
"song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff",
"duration": 152.92036, "year": 0}
```

## Schema

Star schema optimized for queries on song play analysis. This includes the
following tables.

### Fact Table

| songplays | | |
|---|---|---|
songplay_id | IntegerType | PRIMARY KEY
start_time | TimestampType | FOREIGN KEY
user_id | StringType | FOREIGN KEY
level | StringType
song_id | StringType | FOREIGN KEY
artist_id | StringType | FOREIGN KEY
session_id | StringType
location | StringType
user_agent | StringType

### Dimension Tables

| users | | |
|---|---|---|
user_id | StringType | PRIMARY KEY
first_name | StringType
last_name | StringType
gender | StringType
level | StringType

| songs | | |
|---|---|---|
song_id | StringType | PRIMARY KEY
title | StringType
artist_id | StringType
year | TimestampType
duration | DoubleType

| artists | | |
|---|---|---|
artist_id | StringType | PRIMARY KEY
artist_name | StringType
artist_location | StringType
artist_latitude | DecimalType
artist_longitude | DecimalType

| time | | |
|---|---|--|
start_time | TimestampType | PRIMARY KEY
hour | IntegerType
day | IntegerType
week | IntegerType
month | IntegerType
year | IntegerType
weekday | IntegerType

## Usage

### Configuration

Set up a config file `dl.cfg` that uses the following schema. Put
in the information for your IAM-Role that can read and write S3 buckets.

```cfg
[S3]
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
```

### ETL pipeline

Simply run the ETL script.

```bash
python etl.py
```

If the ETL pipeline was successful, a preview of the output data will be
displayed.
