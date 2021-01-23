# SQL Learning and Training
### This is some of the exercises of ProgreSQL programming that i've done following the Stanford University's StanfordOnline course "Databases: Relational Databases and SQL" 
### Available at [edX](https://www.edx.org/course/databases-5-sql)

----
## Movie-Rating Query Exercises
#### [Database Schema](https://courses.edx.org/asset-v1:StanfordOnline+SOE.YDB-SQL0001+2T2020+type@asset+block/moviedata.html)

#### Find the titles of all movies directed by Steven Spielberg.

<font face="Courier New" size="2">
<font color = "blue">SELECT</font>&nbsp;<font color = "maroon">title</font>
<br/><font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">movie</font>
<br/><font color = "blue">WHERE</font>&nbsp;&nbsp;<font color = "maroon">director</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "red">'Steven&nbsp;Spielberg'</font>&nbsp;
</font>

#### Find all years that have a movie that received a rating of 4 or 5, and sort them in increasing order.

<font face="Courier New" size="2">
<font color = "blue">SELECT</font>&nbsp;<font color = "maroon">year</font>
<br/><font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">movie</font>
<br/><font color = "blue">WHERE</font>&nbsp;&nbsp;<font color = "maroon">mid</font>&nbsp;<font color = "blue">IN</font>&nbsp;<font color = "maroon">(</font><font color = "blue">SELECT</font>&nbsp;<font color = "maroon">mid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">WHERE</font>&nbsp;&nbsp;<font color = "maroon">stars</font>&nbsp;<font color = "silver">&gt;</font>&nbsp;<font color = "black">3</font><font color = "maroon">)</font>
<br/><font color = "blue">ORDER</font>&nbsp;&nbsp;<font color = "blue">BY</font>&nbsp;<font color = "maroon">year</font>&nbsp;<font color = "blue">ASC</font>&nbsp;
</font>


#### Find the titles of all movies that have no ratings.

<font face="Courier New" size="2">
<font color = "blue">SELECT</font>&nbsp;<font color = "maroon">title</font>
<br/><font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">movie</font>
<br/><font color = "blue">WHERE</font>&nbsp;&nbsp;<font color = "maroon">mid</font>&nbsp;<font color = "blue">NOT</font>&nbsp;<font color = "blue">IN</font>&nbsp;<font color = "maroon">(</font><font color = "blue">SELECT</font>&nbsp;<font color = "maroon">mid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font><font color = "maroon">)</font>&nbsp;
</font>

#### Some reviewers didn't provide a date with their rating. Find the names of all reviewers who have ratings with a NULL value for the date.

<font face="Courier New" size="2">
<font color = "blue">SELECT</font>&nbsp;<font color = "blue">NAME</font>
<br/><font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">reviewer</font>
<br/><font color = "blue">WHERE</font>&nbsp;&nbsp;<font color = "maroon">rid</font>&nbsp;<font color = "blue">IN</font>&nbsp;<font color = "maroon">(</font><font color = "blue">SELECT</font>&nbsp;<font color = "maroon">rid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">WHERE</font>&nbsp;&nbsp;<font color = "maroon">ratingdate</font>&nbsp;<font color = "blue">IS</font>&nbsp;<font color = "blue">NULL</font><font color = "maroon">)</font>&nbsp;
</font>


#### Write a query to return the ratings data in a more readable format: reviewer name, movie title, stars, and ratingDate. Also, sort the data, first by reviewer name, then by movie title, and lastly by number of stars.

<font face="Courier New" size="2">
<font color = "blue">SELECT</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">r</font><font color = "silver">.</font><font color = "blue">NAME</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">m</font><font color = "silver">.</font><font color = "maroon">title</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">t</font><font color = "silver">.</font><font color = "maroon">stars</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">t</font><font color = "silver">.</font><font color = "maroon">ratingdate</font>
<br/><font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">reviewer</font>&nbsp;<font color = "maroon">R</font>
<br/><font color = "blue">JOIN</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>&nbsp;<font color = "maroon">T</font>
<br/><font color = "blue">JOIN</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">movie</font>&nbsp;<font color = "maroon">M</font>
<br/><font color = "maroon">where</font>&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">r</font><font color = "silver">.</font><font color = "maroon">rid</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "maroon">t</font><font color = "silver">.</font><font color = "maroon">rid</font>
<br/><font color = "blue">AND</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">m</font><font color = "silver">.</font><font color = "maroon">mid</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "maroon">t</font><font color = "silver">.</font><font color = "maroon">mid</font>
<br/><font color = "blue">ORDER</font>&nbsp;<font color = "blue">BY</font>&nbsp;<font color = "maroon">r</font><font color = "silver">.</font><font color = "blue">NAME</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">m</font><font color = "silver">.</font><font color = "maroon">title</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">t</font><font color = "silver">.</font><font color = "maroon">stars</font>
</font>

#### For all cases where the same reviewer rated the same movie twice and gave it a higher rating the second time, return the reviewer's name and the title of the movie.

<font face="Courier New" size="2">
<font color = "blue">SELECT</font>&nbsp;<font color = "maroon">v</font><font color = "silver">.</font><font color = "blue">NAME</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">m</font><font color = "silver">.</font><font color = "maroon">title</font>
<br/><font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">reviewer</font>&nbsp;<font color = "maroon">v</font>
<br/><font color = "blue">JOIN</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">movie</font>&nbsp;<font color = "maroon">m</font>
<br/><font color = "maroon">where</font>&nbsp;&nbsp;<font color = "maroon">v</font><font color = "silver">.</font><font color = "maroon">rid</font>&nbsp;<font color = "blue">IN</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">(</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">SELECT</font>&nbsp;<font color = "maroon">r1</font><font color = "silver">.</font><font color = "maroon">rid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>&nbsp;<font color = "maroon">r1</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">JOIN</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>&nbsp;<font color = "maroon">r2</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">WHERE</font>&nbsp;&nbsp;<font color = "maroon">r1</font><font color = "silver">.</font><font color = "maroon">mid</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "maroon">r2</font><font color = "silver">.</font><font color = "maroon">mid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">AND</font>&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">r1</font><font color = "silver">.</font><font color = "maroon">rid</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "maroon">r2</font><font color = "silver">.</font><font color = "maroon">rid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">AND</font>&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">r1</font><font color = "silver">.</font><font color = "maroon">stars</font>&nbsp;<font color = "silver">&gt;</font>&nbsp;<font color = "maroon">r2</font><font color = "silver">.</font><font color = "maroon">stars</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">AND</font>&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">r1</font><font color = "silver">.</font><font color = "maroon">ratingdate</font>&nbsp;<font color = "silver">&gt;</font>&nbsp;<font color = "maroon">r2</font><font color = "silver">.</font><font color = "maroon">ratingdate</font><font color = "maroon">)</font>
<br/><font color = "blue">AND</font>&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">m</font><font color = "silver">.</font><font color = "maroon">mid</font>&nbsp;<font color = "blue">IN</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">(</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">SELECT</font>&nbsp;<font color = "maroon">r1</font><font color = "silver">.</font><font color = "maroon">mid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>&nbsp;<font color = "maroon">r1</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">JOIN</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>&nbsp;<font color = "maroon">r2</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">WHERE</font>&nbsp;&nbsp;<font color = "maroon">r1</font><font color = "silver">.</font><font color = "maroon">mid</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "maroon">r2</font><font color = "silver">.</font><font color = "maroon">mid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">AND</font>&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">r1</font><font color = "silver">.</font><font color = "maroon">rid</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "maroon">r2</font><font color = "silver">.</font><font color = "maroon">rid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">AND</font>&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">r1</font><font color = "silver">.</font><font color = "maroon">stars</font>&nbsp;<font color = "silver">&gt;</font>&nbsp;<font color = "maroon">r2</font><font color = "silver">.</font><font color = "maroon">stars</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">AND</font>&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">r1</font><font color = "silver">.</font><font color = "maroon">ratingdate</font>&nbsp;<font color = "silver">&gt;</font>&nbsp;<font color = "maroon">r2</font><font color = "silver">.</font><font color = "maroon">ratingdate</font><font color = "maroon">)</font>
</font>


#### For each movie that has at least one rating, find the highest number of stars that movie received. Return the movie title and number of stars. Sort by movie title.

<font face="Courier New" size="2">
<font color = "blue">SELECT</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">m</font><font color = "silver">.</font><font color = "maroon">title</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">t</font><font color = "silver">.</font><font color = "maroon">stars</font>
<br/><font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">movie</font>&nbsp;<font color = "maroon">m</font>
<br/><font color = "blue">JOIN</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">(</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">SELECT</font>&nbsp;<font color = "blue">DISTINCT</font>&nbsp;<font color = "maroon">mid</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "fuchsia"><i>Max</i></font><font color = "maroon">(</font><font color = "maroon">stars</font><font color = "maroon">)</font>&nbsp;<font color = "blue">AS</font>&nbsp;<font color = "maroon">stars</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">GROUP</font>&nbsp;<font color = "blue">BY</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">mid</font><font color = "maroon">)</font>&nbsp;<font color = "maroon">t</font>
<br/><font color = "maroon">where</font>&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">m</font><font color = "silver">.</font><font color = "maroon">mid</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "maroon">t</font><font color = "silver">.</font><font color = "maroon">mid</font>
<br/><font color = "blue">ORDER</font>&nbsp;<font color = "blue">BY</font>&nbsp;<font color = "maroon">m</font><font color = "silver">.</font><font color = "maroon">title</font>
</font>

#### For each movie, return the title and the 'rating spread', that is, the difference between highest and lowest ratings given to that movie. Sort by rating spread from highest to lowest, then by movie title.

<font face="Courier New" size="2">
<font color = "blue">SELECT</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">title</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">r</font><font color = "silver">.</font><font color = "maroon">ratingspread</font>
<br/><font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">movie</font>&nbsp;<font color = "maroon">M</font>
<br/><font color = "blue">JOIN</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">(</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">SELECT</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">mid</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "fuchsia"><i>Max</i></font><font color = "maroon">(</font><font color = "maroon">stars</font><font color = "maroon">)</font>&nbsp;<font color = "silver">-</font>&nbsp;<font color = "fuchsia"><i>Min</i></font><font color = "maroon">(</font><font color = "maroon">stars</font><font color = "maroon">)</font>&nbsp;<font color = "blue">AS</font>&nbsp;<font color = "maroon">ratingspread</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">GROUP</font>&nbsp;<font color = "blue">BY</font>&nbsp;<font color = "maroon">mid</font><font color = "maroon">)</font>&nbsp;<font color = "maroon">R</font>
<br/><font color = "maroon">where</font>&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">m</font><font color = "silver">.</font><font color = "maroon">mid</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "maroon">r</font><font color = "silver">.</font><font color = "maroon">mid</font>
<br/><font color = "blue">ORDER</font>&nbsp;<font color = "blue">BY</font>&nbsp;<font color = "maroon">ratingspread</font>&nbsp;<font color = "blue">DESC</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">title</font>
</font>

#### Find the difference between the average rating of movies released before 1980 and the average rating of movies released after 1980. (Make sure to calculate the average rating for each movie, then the average of those averages for movies before 1980 and movies after. Don't just calculate the overall average rating before and after 1980.)

<font face="Courier New" size="2">
<font color = "blue">SELECT</font>&nbsp;<font color = "fuchsia"><i>Avg</i></font><font color = "maroon">(</font><font color = "maroon">a</font><font color = "maroon">)</font>&nbsp;<font color = "silver">-</font>&nbsp;<font color = "fuchsia"><i>Avg</i></font><font color = "maroon">(</font><font color = "maroon">b</font><font color = "maroon">)</font>
<br/><font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">(</font><font color = "blue">SELECT</font>&nbsp;<font color = "maroon">R</font><font color = "silver">.</font><font color = "maroon">mid</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "fuchsia"><i>Avg</i></font><font color = "maroon">(</font><font color = "maroon">stars</font><font color = "maroon">)</font>&nbsp;<font color = "blue">AS</font>&nbsp;<font color = "maroon">A</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>&nbsp;<font color = "maroon">R</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">movie</font>&nbsp;<font color = "maroon">M</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">WHERE</font>&nbsp;&nbsp;<font color = "maroon">R</font><font color = "silver">.</font><font color = "maroon">mid</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "maroon">M</font><font color = "silver">.</font><font color = "maroon">mid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">AND</font>&nbsp;<font color = "maroon">year</font>&nbsp;<font color = "silver">&lt;</font>&nbsp;<font color = "black">1980</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">GROUP</font>&nbsp;&nbsp;<font color = "blue">BY</font>&nbsp;<font color = "maroon">R</font><font color = "silver">.</font><font color = "maroon">mid</font><font color = "maroon">)</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">(</font><font color = "blue">SELECT</font>&nbsp;<font color = "maroon">R</font><font color = "silver">.</font><font color = "maroon">mid</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "fuchsia"><i>Avg</i></font><font color = "maroon">(</font><font color = "maroon">stars</font><font color = "maroon">)</font>&nbsp;<font color = "blue">AS</font>&nbsp;<font color = "maroon">B</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">FROM</font>&nbsp;&nbsp;&nbsp;<font color = "maroon">rating</font>&nbsp;<font color = "maroon">R</font><font color = "silver">,</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "maroon">movie</font>&nbsp;<font color = "maroon">M</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">WHERE</font>&nbsp;&nbsp;<font color = "maroon">R</font><font color = "silver">.</font><font color = "maroon">mid</font>&nbsp;<font color = "silver">=</font>&nbsp;<font color = "maroon">M</font><font color = "silver">.</font><font color = "maroon">mid</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">AND</font>&nbsp;<font color = "maroon">year</font>&nbsp;<font color = "silver">&gt;</font>&nbsp;<font color = "black">1980</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color = "blue">GROUP</font>&nbsp;&nbsp;<font color = "blue">BY</font>&nbsp;<font color = "maroon">R</font><font color = "silver">.</font><font color = "maroon">mid</font><font color = "maroon">)</font><font color = "silver">;</font>&nbsp;
</font>



