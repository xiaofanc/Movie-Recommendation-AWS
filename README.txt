# Movie Recommmendation with Spark
## Introduction

The project uses datasets (ml-latest) including 5-star rating and free-text tagging activity from [MovieLens](http://movielens.org), a movie recommendation service. The complete dataset contains 27753444 ratings and 1108997 tag applications across 58098 movies. These data were created by 283228 users between January 09, 1995 and September 26, 2018. This dataset was generated on September 26, 2018.

The Project is to build an ETL pipeline that extracts data from S3, processes them using Spark, stages them in Redshift, and transforms data into a set of dimensional tables.


## Project Datasets
* Test data: 's3://udacity-input/ml-latest-small'  
* Complete data: 's3://udacity-input/ml-latest'  


#### Movies Data File Structure (movies.csv)
--------------------------------------------

Movie information is contained in the file `movies.csv`. Each line of this file after the header row represents one movie, and has the following format:

* movieId, title, genres

Movie titles are entered manually or imported from <https://www.themoviedb.org/>, and include the year of release in parentheses. Errors and inconsistencies may exist in these titles.

Genres are a pipe-separated list, and are selected from the following:

* Action
* Adventure
* Animation
* Children's
* Comedy
* Crime
* Documentary
* Drama
* Fantasy
* Film-Noir
* Horror
* Musical
* Mystery
* Romance
* Sci-Fi
* Thriller
* War
* Western
* (no genres listed)


#### Ratings Data File Structure (ratings.csv)
----------------------------------------------

All ratings are contained in the file `ratings.csv`. Each line of this file after the header row represents one rating of one movie by one user, and has the following format:

* userId, movieId, rating, timestamp

The lines within this file are ordered first by userId, then, within user, by movieId. Ratings are made on a 5-star scale, with half-star increments (0.5 stars - 5.0 stars). Timestamps represent seconds since midnight Coordinated Universal Time (UTC) of January 1, 1970.


#### Tags Data File Structure (tags.csv)
----------------------------------------

All tags are contained in the file `tags.csv`. Each line of this file after the header row represents one tag applied to one movie by one user, and has the following format:

* userId, movieId, tag, timestamp

The lines within this file are ordered first by userId, then, within user, by movieId. Tags are user-generated metadata about movies. Each tag is typically a single word or short phrase. The meaning, value, and purpose of a particular tag is determined by each user. Timestamps represent seconds since midnight Coordinated Universal Time (UTC) of January 1, 1970.


## Schema for Movie Recommendation Analysis
Using the above datasets, I need to create a star schema optimized for queries on movie recommendation analysis. This includes the following tables.


### Fact Tables
* **movieratings** - (movieId, rating, release_year, rewards)
### Dimension Tables
* **movies** - (movieId, title, release_year)   
* **genres** - (movieId, genres)  
* **ratings** - (userId, movieId, rating, timestamp)  
* **time** - timestamps in ratings broken down into specific units (start_time, hour, day, week, month, year, weekday)


## Project Template
* **create_redshift_cluster.ipynb** create redshift cluster
* **etl.ipynb** read data from s3, staging to redshift, and create tables
* **dwh.cfg** contains AWS credentials       


## Project Steps
### Create user on AWS
* Get the access key and secret key, and put it into dwh.cfg


### Create redshift cluster
* Run create_redshift_cluster.ipynb


### Build ETL Pipeline
* Implement the logic in etl.ipynb to extract data from s3 
* Transform data into fact and dimension tables
* Load tables into redshift



