Install Pig:
$ wget http://mirror.symnds.com/software/Apache/pig/pig-0.12.0/pig-0.12.0.tar.gz

Untar:
$ tar xvzf pig-0.12.0.tar.gz

To start Local Mode:
$ pig -x local

Load the CSV data using PIG STORAGE:
grunt> movies = LOAD '/home/cloudera/Desktop/movies_data.csv' USING PigStorage(',') as (id,name,year,rating,duration);

Dump the data:
grunt> DUMP movies;

 1.	Find the number of movies released between 1950 and 1960. 

grunt> movies_between_50_60 = FILTER movies by year>1950 and year<1960;
grunt> Dump movies_between_50_60;

2.	Find the number of movies having rating more than 4. 

grunt> movies_greater_than_four = FILTER movies BY (float)rating>4.0;
grunt> DUMP movies_greater_than_four;

3.	Find the movies whose rating are between 3 and 4. 

grunt> movies_rating_3_4 = FILTER movies BY rating>3.0 and rating<4.0;
grunt> Dump movies_rating_3_4;


4.	Find the number of movies with duration more than 2 hours (7200 second).

grunt> movies_duration_2_hrs = FILTER movies by duration > 7200;
grunt> Dump movies_duration_2_hrs;

5.	Find the list of years and number of movies released each year. 

grunt> grouped_by_year = group movies by year;
grunt> count_by_year = FOREACH grouped_by_year GENERATE group, COUNT(movies);
grunt> Dump count_by_year;

6.	Find the total number of movies in the dataset. 

grunt> group_all = GROUP count_by_year ALL;
grunt> sum_all = FOREACH group_all GENERATE SUM(count_by_year.$1);
grunt> DUMP sum_all;









