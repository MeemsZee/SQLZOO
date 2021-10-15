# [SQLZOO](https://sqlzoo.net/wiki/SQL_Tutorial) Tutorial Answer key

<!-- Working on this! 

## Table of Contents

<a href="#select-basics">SELECT Basics</a>

<a href="#select-from-world"> SELECT from WORLD
	-->

### SELECT Basics

#### Question 1- Introducing the world of table of countries

Show population of Germany.  Note: Don't use double quotation marks
  
```sql
SELECT population
FROM   world
WHERE  name = 'Germany';
```

#### Question 2- Scandinavia

Show the name and population of 'Sweden', 'Norway' and 'Denmark'

```sql
SELECT name, 
       population
FROM   world
WHERE  name IN('Sweden', 'Norway', 'Denmark');
```

#### Question 3- Just the right size

Show the country and area for countries with an aera between 200,000 and 250,000 

```sql
SELECT name, 
       area
FROM   world
WHERE  area BETWEEN 200000 AND 250000;
;
```

### SELECT from WORLD

#### Question 1- Introduction

Show name, continent and population of all countries

```sql
SELECT name, 
       continent, 
       population
FROM   world;
```

#### Question 2- Large Countries

Show the name for the countries that have a population of at least 200 million.

```sql
SELECT 
  name
FROM 
  world
WHERE 
  population >200000000
;
```

#### Question 3- Per capital GDP

Give the name and per capita GDP for those countries with a population of at least 200 million.  Hint: per capita GDP= GDP/population

```sql
SELECT 
  name, 
  GDP/population AS per_capita_GDP
FROM 
  world
WHERE 
  population >200000000
;
```

#### Question 4- South America In millions

Show the name and population in millions for the countries of the continent 'South America'.  

```sql
SELECT 
  name, 
  population/1000000 AS pop_per_million
FROM 
  world
WHERE 
  continent = 'South America'
;
```

#### Question 5- France, Germany, Italy

Show the name and population for France, Germany, Italy

```sql
SELECT 
  name, 
  population 
FROM 
  world
WHERE 
  name 
    IN ('France', 'Germany', 'Italy')
;
```
#### Question 6- United

Show the countries which have name that includes the word 'United'

```sql
SELECT 
  name
FROM 
  world
WHERE 
  name 
    LIKE '%United%'
;
```

#### Question 7- Two ways to be big

Show the countries that are big by area or big by population.  Show name, population and area.

```sql
SELECT 
  name, 
  population, 
  area
FROM 
  world
WHERE 
  area> 3000000 
  OR population>250000000
;
```

#### Question 8- One or the other (but not both)

Show the countries that are big by area (more than 3 mil) or by population (more than 250 mil) but not both.  Show name, population and area. 

```sql
SELECT 
  name, 
  population, 
  area 
FROM 
  world 
WHERE 
  area > 3000000 
  XOR population > 250000000
;
```

OR

```sql
SELECT 
  name, 
  population, 
  area 
FROM 
  world 
WHERE 
  (area > 3000000 AND population <250000000) 
  OR (population > 250000000 AND area <3000000)
;
```

#### Question 9- Rounding
Show the name and population in millions and the GDP in billions for the countires of the continent 'South America' to the nearnest hundredth. 

```sql
SELECT 
  name, 
  ROUND(population/1000000,2) AS pop_in_millions,
  ROUND(GDP/1000000000,2) AS GDP_in_billions 
FROM 
  world 
WHERE 
  continent = 'South America'
; 
```

#### Question 10- Trillion dollar economies 

Show the name and per capita GDP for countries with a GDP of minimum 1 tillion rounded to nearest thousand. 

```sql
SELECT 
  name, 
  ROUND(GDP/population,-3)
FROM 
  world
WHERE 
  gdp > 1000000000000
;
```

#### Question 11- Name and capital have the same length

Show the name and capital where the name and the capital have the same number of characters. 

```sql
SELECT 
  name, 
  capital 
FROM 
  world 
WHERE 
  LENGTH(name)= LENGTH(capital)
;
```

#### Question 12- Matching name and capital

Show the name and capital where the first letters of each match. Don't include countries where the name and the capital are the same word

```sql
SELECT 
  name, 
  capital 
FROM 
  world 
WHERE 
  LEFT(name,1)= LEFT(capital,1) 
  AND name <> capital
;
```

#### Question 13- All the vowels

Find the country that has all the vowels and no spaces in its name.

```sql
SELECT 
  name
FROM 
  world
WHERE 
  name LIKE '%a%' 
  AND name LIKE '%e%' 
  AND name LIKE '%i%'
  AND name LIKE '%o%' 
  AND name LIKE '%u%' 
  AND name NOT LIKE '% %'
;
```

### SELECT from Nobel 

#### Question 1- Winners from 1950

Change existing query to display Nobel prices for 1950

```sql
SELECT 
  yr, 
  subject, 
  winner
FROM 
  nobel
WHERE 
  yr = 1950
;
```

#### Question 2- 1962 Literature

Show who won the 1962 prize for Literature

```sql
SELECT 
  winner
FROM 
  nobel 
WHERE 
  yr = 1962
  AND subject = 'literature'
;
```

#### Question 3- Albert Einstein

Show the year and subject that won 'Albert Einstein' his prize

```sql
SELECT 
  yr, 
  subject
FROM 
  nobel 
WHERE 
  winner= 'albert einstein'
;
```

#### Question 4- Recent Peace Prizes

Give the name of the 'Peace' winners since the year 2000, including 2000

```sql
SELECT 
  winner
FROM 
  nobel
WHERE 
  yr >= 2000 
  AND subject ='peace'
;
```

#### Question 5- Literature in the 1980s

Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive. 

```sql
SELECT 
  *
FROM 
  nobel
WHERE 
  subject= 'literature'
  AND yr>=1980 
  AND yr <=1989
;
```
OR

```sql
SELECT 
  yr, 
  subject, 
  winner
FROM 
  nobel
WHERE 
  subject= 'literature'
  AND yr>=1980 
  AND yr <=1989
;
```

#### Question 6- Only Presidents

Show all details of the presidental winners: Theodore Roosevelt, Woodrow Wilson, Jimmy Carter, Barack Obama

```sql
SELECT 
  * 
FROM 
  nobel 
WHERE 
  winner 
    IN ('theodore roosevelt', 'woodrow wilson', 'jimmy carter', 'barack obama')
; 
```

#### Question 7- John 

Show the winners with the first name John

```sql
SELECT 
  winner
FROM 
  nobel
WHERE 
  winner 
    LIKE 'John%'
;
```

#### Question 8- Chemistry and Physics from different years

Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984

```sql
SELECT 
  yr, 
  subject, 
  winner
FROM 
  nobel 
WHERE 
  subject='physics' 
  AND yr =1980
  OR (subject='chemistry' 
    AND yr = 1984)
;
```

#### Question 9- Exclude Chemists and Medics

Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine

```sql
SELECT 
  yr, 
  subject, 
  winner
FROM 
  nobel 
WHERE 
  yr = 1980 
  AND subject 
    NOT IN ('Chemistry', 'Medicine')
;
```

#### Question 10- Early Medicine, Late Literature

Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later (after 2004, including 2004)

```sql
SELECT 
  yr, 
  subject, 
  winner
FROM 
  nobel
WHERE 
  (subject ='medicine' and yr<1910)
  OR (subject='literature' and yr >=2004)
;
```
#### Question 11- Umlaut

Find all details of the prize won by Peter Grünberg. Hint: for macs hold press on u until options pop up and select the number corresponding to the letter desired

```sql
SELECT 
  *
FROM 
  nobel 
WHERE 
  winner='peter grünberg'
;
```

#### Question 12- Apostrophe

Find all details of the prize won by Eugene O'Neill. Hint: to tell sql you want to keep the single quote, add another one directly after ('')

```sql
SELECT 
  *
FROM 
  nobel
WHERE 
  winner= 'eugene o''neill'
;
```

#### Question 13- Knights of the realm

List the winners, year, and subject where the winner starts with Sir.  Show the most recent first, then by name order. 

```sql
SELECT 
  winner, 
  yr, 
  subject
FROM 
  nobel
WHERE 
  winner 
    LIKE 'SIR%'
ORDER BY 
  yr DESC, 
  winner
;
```

#### Question 14- Chemistry and Physics last

Show the 1984 winners and subject ordered by subject and winner name; bust list Chesmitry and Physics last. 

```sql
SELECT 
  winner, 
  subject
FROM 
  nobel
WHERE 
  yr=1984
ORDER BY 
  subject 
    IN ('physics','chemistry'), subject, winner
;
```
 
 OR
 
```sql
SELECT 
  winner, 
  subject
FROM 
  nobel
WHERE 
  yr=1984
ORDER BY 
  CASE WHEN subject 
   IN ('physics','chemistry')
      THEN 1 ELSE 0 
      END,
  subject,
  winner
;
```


### SELECT within SELECT

#### Question 1- Bigger than Russia

List each country name where the population is larger than that of 'Russia'. 

```sql
SELECT 
  name
FROM 
  world
WHERE 
  population> 
    (SELECT 
       population 
     From 
       world
     WHERE 
       name='Russia')
;
```

#### Question 2- Richer than UK

Show the countries in Europe with a per capita GDP greater than 'United Kingdom'

```sql
SELECT 
  name
FROM 
  world
WHERE 
  continent='europe'
  AND GDP/population> (SELECT 
       			 gdp/population
     		       FROM 
       			 world
     		       WHERE 
       			 name= 'united kingdom')
;
```

#### Question 3- Neighbours of Argentina and Australia
List the name and continent of countries in the continent containing either Argentina or Australia.  Order by name of the country

```sql
SELECT 
  name, 
  continent
FROM 
  world
WHERE 
  continent= (SELECT 
       		continent 
     	      FROM 
       		world
              WHERE 
       		name='Australia')
  OR continent= (SELECT 
      		   continent
     		 FROM 
       		   world
     		 WHERE 
       		   name= 'Argentina')
ORDER BY 
  name ASC
;
```

#### Question 4- Between Cananda and Poland

Which country has a population that is more than Cananda but less than Poland? Show name and population

```sql
SELECT 
  name, 
    population 
FROM 
  world
WHERE 
  population> (SELECT 
      		 population 
     	       FROM 
      		 world
     	       WHERE 
       		 name='Canada')
  AND population<(SELECT 
       		    population 
     		  FROM 
      		    world
     		  WHERE 
      		    name ='poland')
;
```

#### Question 5- Percentages of Germany

Show the name and population of each country in Europe.  Show the population as a percentage of the population of Germany. 

```sql
SELECT 
  name, 
  CONCAT
    (ROUND(population/(SELECT 
                         population 
		       From 
		         world 
		       WHERE 
		         name='Germany')
           *100,0),'%')
FROM 
  world
WHERE 
  continent='europe'
;
```
#### Question 6- Bigger than every country in Europe

Which countries have a GDP greater than every country in Europe? Give the name only.  Hint: For the first query, the condition gdp>0 is imperative in the subquery.  Some countries have null for gdp.

```sql
SELECT 
  name 
FROM 
  world
WHERE 
  gdp> ALL(SELECT 
  		gdp 
    	   FROM 
	   	world
	   WHERE 
	   	continent='europe'
		AND gdp>0)
; 
```
OR

```sql
SELECT 
  name 
FROM
  world
WHERE 
  gdp>(SELECT 
         MAX(gdp) 
       FROM 
         world
       WHERE 
         continent='europe')
;
```

#### Question 7- Largest in each continent

Find the largest country(by area) in each continent, show the continent, the name and the area. 

```sql
SELECT 
  continent, 
  name, 
  area 
FROM 
  world a
WHERE 
  area >= ALL(SELECT 
	  	area 
	      FROM 
	   	world b
	      WHERE 
	   	a.continent=b.continent
	    	AND area>0)
;
```

OR 

```sql
SELECT 
  continent, 
  name, 
  area 
FROM 
  world a
WHERE 
  area =(SELECT 
	   Max(area) 
	 FROM 
	   world b
	 WHERE 
	   a.continent=b.continent
	   AND area>0)
;
```

#### Question 8- First country of each continent

```sql
SELECT 
  continent, 
  name 
FROM 
  world a
WHERE 
  name=(SELECT 
          MIN(name) 
      	FROM
          world b 
      	WHERE 
          a.continent=b.continent)
;
```

OR 
```sql
SELECT 
  continent, 
  name 
FROM 
  world a
WHERE 
  name<= ALL(SELECT 
	   	name 
	     FROM 
	   	world b 
	     WHERE 
	 	a.continent=b.continent)
;
```

#### Question 9- Difficult Questions that Utilize Techniques Not Covered In Prior Sections

Find the continents where all countires have a population <25000000.  Then find the names of the countries associated with these continents.  Show name, continent and population. 

```sql
SELECT 
  name, 
  continent, 
  population 
FROM 
  world a
WHERE 
  25000000>= ALL(SELECT 
  		   population
		 FROM 
		   world b
		 WHERE 
		   a.continent=b.continent)
;
```

#### Question 10

Some countries have populations more than three times that of any of their neighbours (in the same continent).  Give the countries and continents

```sql
SELECT 
  name, 
  continent 
FROM 
  world a 
WHERE 
  population>= ALL(SELECT 
  		     population*3 
		   FROM 
		     world b
		   WHERE 
		     a.continent= b.continent 
		     AND b.name != a.name)
;
```

### SUM and COUNT

#### Question 1- Total world population

Show the total population of the world. 

```sql
SELECT 
  SUM(population)
FROM 
  world
;
```

#### Question 2- List of continents

List all continents- just once each

```sql
SELECT 
  Distinct(continent)
FROM 
  world
;
```

#### Question 3.  GDP of Africa

Give the total GDP of Africa

```sql
SELECT 
  sum(gdp) 
FROM 
  world
WHERE 
  continent='africa'
;
```

#### Question 4. Count the big countries

How many countries have an area of at least 1000000

```sql
SELECT 
  count(name) 
FROM
  world
WHERE 
  area>=1000000
;
```

#### Question 5- Baltic states population

What is the total population of ('Estonia', 'Latvia', 'Lithuania')

```sql
SELECT 
  SUM(population)
FROM 
  world
WHERE 
  name 
    IN ('estonia', 'latvia', 'lithuania')
;
```

#### Question 6- Counting the countries of each continent

For each continent show the continent and number of countries

```sql
SELECT continent, count(name)
FROM world
GROUP BY continent
;
```

#### Question 7- Counting big countries in each continent

For each continent show the continent and number of countries with populations of at least 10 million. 

```sql
SELECT 
  continent,
  COUNT(name)
FROM 
  world
WHERE 
  population>=10000000
GROUP BY 
  continent
;
```

#### Question 8- Counting big continents

List the continents that have a total population of at least 100 million

```sql
SELECT 
  continent
FROM 
  world 
GROUP BY 
  continent
HAVING 
  SUM(population)>=100000000
;
```

### Nobel Table- SUM and COUNT functions

#### Question 1

Show the number of prizes awarded

```sql
SELECT
  COUNT(winner) 
FROM 
  nobel
;
```

#### Question 2

List each subject- just once

```sql
SELECT 
  DISTINCT(subject)
FROM 
  nobel
;
```

### Question 3

Show the total number of prizes awarded for Physics

```sql
SELECT 
  COUNT(winner) 
FROM 
  nobel
WHERE 
  subject='physics'
;
```

#### Using GROUP BY and HAVING

#### Question 4

For each subject, show the subject and number of prizes

```sql
SELECT 
  subject, 
  COUNT(winner)
FROM 
  nobel
GROUP BY 
  subject
;
```

#### Question 5

For each subject, show the first year that the prize was awarded

```sql
SELECT 
  subject, 
  MIN(yr)
FROM 
  nobel 
GROUP BY 
  subject
;
```

#### Question 6

For each subject, who the number of prizes awarded in the year 2000

```sql
SELECT 
  subject, 
  COUNT(winner)
FROM 
  nobel 
WHERE 
  yr='2000'
GROUP BY 
  subject
;
```

#### Aggregates with DISCTINCT

#### Question 7

Show the number of winners for each subject

```sql
SELECT 
  subject, 
  COUNT(
    DISTINCT(winner))
FROM 
  nobel
GROUP BY 
  subject
;
```

#### Question 8

For each subject, show how many years have had prizes awarded

```sql
SELECT 
  subject, 
  COUNT(
    DISTINCT(yr))
FROM 
  nobel
GROUP BY 
  subject
;
```

#### Using HAVING

#### Question 9

Show the years in which three prizes where given for Physics

```sql
SELECT 
  yr
FROM 
  nobel
WHERE 
  subject='physics'
GROUP BY 
  yr
HAVING 
  COUNT(winner)=3
;
```

#### Question 10

Show winners who have won more than once

```sql
SELECT 
  winner
FROM 
  nobel
GROUP BY 
  winner
HAVING 
  COUNT(winner)>1
;
```

#### Question 11

Show winners who have one more than one subject

```sql
SELECT 
  winner 
FROM 
  nobel
GROUP BY 
  winner
HAVING 
  COUNT(
    DISTINCT(subject))
    >1
;
```

#### GROUP By yr, subject

#### QUESTION 12

Show the year and subject where 3 prizes were given.  SHow only years 2000 onwards

```sql
SELECT 
  yr, 
  subject
FROM 
  nobel
WHERE 
  yr >=2000
GROUP BY 
  yr, 
  subject
HAVING
  COUNT(winner)=3
;
```

### The JOIN Operation

#### Question 1

Show matchid and player name for all goals scored by Germany.  To identify German players, check for teamid='GER'

```sql
SELECT 
  matchid, 
  player 
FROM 
  goal 
WHERE 
  teamid='GER'
;
```

#### Question 2

From the previous query you can see that Lars Bender's scored a goal in game 1012. Now we want to know what teams were playing in that match.

Notice in the that the column matchid in the goal table corresponds to the id column in the game table. We can look up information about game 1012 by finding that row in the game table.

Show id, stadium, team1, team2 for just game 1012

```sql
SELECT 
  id,
  stadium,
  team1,
  team2
FROM 
  game
WHERE 
  id=1012
;
```

OR

```sql
SELECT 
  id,
  stadium,
  team1,
  team2
FROM 
  game 
    JOIN goal
	ON game.id=goal.matchid
WHERE 
  player='Lars Bender'
;
```

OR

```sql
SELECT 
  id,
  stadium,
  team1,
  team2
FROM 
  game, 
  goal
WHERE 
  game.id=goal.matchid 
  AND player='Lars Bender'
;
```

#### Question 3- 

The code below shows the player (from the goal) and stadium name (from the game table) for every goal scored.

Modify it to show the player, teamid, stadium and mdate for every German goal.

```sql
SELECT 
  player, 
  teamid, 
  stadium, 
  mdate
FROM 
  game, 
  goal
WHERE 
  game.id=goal.matchid 
  AND teamid='GER'
;
```

OR

```sql
SELECT 
  player,
  teamid, 
  stadium, 
  mdate
FROM 
  game 
    JOIN goal
	ON game.id=goal.matchid
WHERE 
  teamid='GER'
;
```

#### Question 4- 

Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'

```sql
SELECT 
  team1, 
  team2, 
  player 
FROM 
  game, 
  goal
WHERE 
  game.id=goal.matchid 
  AND player LIKE 'Mario%'
;
```

OR

```sql
SELECT 
  team1, 
  team2, 
  player 
FROM 
  game 
    JOIN goal
	ON game.id=goal.matchid
WHERE 
  player 
    LIKE 'Mario%'
;
```

#### Question 5- 

The table eteam gives details of every national team including the coach. You can JOIN goal to eteam using the phrase goal JOIN eteam on teamid=id

Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10

```sql
SELECT 
  player,
  teamid, 
  coach, 
  gtime
FROM 
  goal, 
  eteam
WHERE 
  goal.teamid=eteam.id 
  AND gtime<=10
;
```

OR

```sql
SELECT 
  player, 
  teamid, 
  coach, 
  gtime
FROM 
  goal 
    JOIN eteam
	ON goal.teamid=eteam.id 
WHERE 
  gtime<=10
;
```

#### Question 6-

List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.

```sql
SELECT 
  mdate, 
  teamname 
FROM 
  game 
    JOIN eteam 
    	ON team1=eteam.id
WHERE 
  team1 =(SELECT 
  		eteam.id 
	  FROM 
	  	eteam
	  WHERE 
	  	coach = 'Fernando Santos')
;
```

#### Question 7-

List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'

```sql
SELECT 
  player
FROM 
  game 
    JOIN goal
	ON game.id=goal.matchid
WHERE 
  game.stadium='national stadium, warsaw'
;
```

#### Question 8-

The example query shows all goals scored in the Germany-Greece quarterfinal.
Instead show the name of all players who scored a goal against Germany.

```sql
SELECT 
  DISTINCT(player)
FROM 
  game 
    JOIN goal
	ON game.id=goal.matchid
WHERE 
  (team1='ger' or team2='ger') 
  AND teamid !='ger'
;
```

#### Question 9-

Show teamname and the total number of goals scored.

```sql
SELECT 
  teamname,
  COUNT(gtime)
    AS goals_scored
FROM 
  goal 
    JOIN eteam 
	ON goal.teamid=eteam.id
GROUP BY 
  teamname
;
```

#### Question 10-

Show the stadium and the number of goals scored in each stadium.

```sql
SELECT 
  stadium, 
  COUNT(gtime) 
    AS goals_scored
FROM 
  game 
    JOIN goal
	ON game.id=goal.matchid
GROUP BY 
  stadium
;
```

#### Question 11-

For every match involving 'POL', show the matchid, date and the number of goals scored.

```sql
SELECT
  matchid, 
  mdate, 
  COUNT(gtime) 
    AS goals_scored
FROM 
  game 
    JOIN goal
	ON game.id=goal.matchid
WHERE 
  (team1='pol' OR team2='pol')
GROUP BY 
  matchid, 
  mdate
;
```

#### Question 12-

For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'

```sql
SELECT
  matchid, 
  mdate, 
  COUNT(gtime) 
    AS goals_scored
FROM 
  game 
    JOIN goal
	ON game.id=goal.matchid
WHERE 
  (team1='ger' or team2='ger') 
  AND teamid='ger'
GROUP BY 
  matchid, 
  mdate
;
```

#### Question 13-

List every match with the goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises.

Notice in the query given every goal is listed. If it was a team1 goal then a 1 appears in score1, otherwise there is a 0. You could SUM this column to get a count of the goals scored by team1. Sort your result by mdate, matchid, team1 and team2.

```sql
SELECT 
  mdate, 
  team1,
  SUM(CASE 
        WHEN teamid=team1 THEN 1 ELSE 0 END) score1,
  team2,
  SUM(CASE 
  	WHEN teamid=team2 THEN 1 ELSE 0 END) score2
FROM 
  game
    LEFT JOIN goal 
      ON game.id = goal.matchid
GROUP BY 
  mdate, 
  team1, 
  team2
ORDER BY 
  mdate,
  matchid, 
  team1,
  team2
;
```

### More JOIN Operations

#### Question 1- 1962 movies

List the films where the yr is 1962 (Show id, title)

```sql
SELECT 
  id, 
  title
FROM 
  movie
WHERE
  yr=1962
;
```

#### Quesiton 2- When was Citizen Kane released? 

Give year of 'Citizen Kane'

```sql
SELECT 
  yr
FROM 
  movie 
WHERE 
  title='Citizen Kane'
;
```

#### Question 3- Star Trek movies

List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title). Order results by year.

```sql
SELECT 
  id, 
  title, 
  yr
FROM 
  movie
WHERE 
  title 
    LIKE '%star trek%'
ORDER BY 
  yr
;
```

#### Question 4- id for actor Glenn close

What id number does the actor 'Glenn Close' have?

```sql
SELECT 
  id
FROM
  actor
WHERE 
  name='glenn close'
;
```

#### Question 5-

What is the id of the film 'Casablanca'

```sql
SELECT 
  id
FROM 
  movie
WHERE 
  title='casablanca'
;
```

#### Question 6- Cast list of Casablanca

Obtain the cast list for 'Casablanca'.

```sql
SELECT 
  name
FROM 
  actor 
    JOIN casting
	ON actorid=id
    JOIN movie 
	ON movieid=movie.id
WHERE 
  title='casablanca'
;
```

OR

```sql
SELECT 
  name
FROM 
  actor 
    JOIN casting
	ON actorid=id
WHERE 
  movieid=11768
;
```

#### Question 7- Alien Cast List 

Obtain the cast list for the film 'Alien'

```sql
SELECT 
  name
FROM 
  actor 
    JOIN casting
	ON actorid=id
    JOIN movie 
	ON movieid=movie.id
WHERE 
  title='alien'
;
```

#### Question 8- Harrison Ford movies

List the films which 'Harrison Ford' has appeared. 

```sql
SELECT 
  title
FROM 
  movie 
    JOIN casting
	ON movie.id=movieid
    JOIN actor
	ON actor.id=actorid
WHERE 
  actor.name='Harrison Ford'
;
```

#### Question 9- Harrison Ford as a supporting actor

List the films where 'Harrison Ford' has appeared - but not in the starring role. (Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role)

```sql
SELECT 
  title
FROM 
  movie 
    JOIN casting
	ON movie.id=movieid
    JOIN actor
	ON actor.id=actorid
WHERE 
  actor.name='Harrison Ford'
  AND casting.ord !=1
;
```

#### Question 10- Lead actors in 1962 movies

List the films together with the leading start for all 1962 films

```sql
SELECT 
  title
    AS movie, 
  name 
    AS leading_actor
FROM 
  movie 
    JOIN casting
	ON movieid=movie.id
    JOIN actor
	ON actorid=actor.id
WHERE 
  yr=1962 
  AND casting.ord =1
;
```

#### Question 11- Busy years for Rock Hudson

Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.

```sql
SELECT 
  yr, 
  COUNT(title)
FROM 
  movie 
    JOIN casting
	ON movie.id=movieid
    JOIN actor
	ON actorid=actor.id
WHERE 
  name='rock hudson'
GROUP BY 
  yr
HAVING 
  COUNT(title)>2
; 
```

#### Question 12- Lead actor in Julie Andrews movies

List the film title and the leading actor for all of the films 'Julie Andrews' played in.

```sql
SELECT 
  title, 
  name
FROM 
  movie 
    JOIN casting
	ON movie.id=movieid
    JOIN actor
	ON actorid=actor.id
WHERE 
  movieid 
    IN(	SELECT
    	  movieid 
	FROM 
	  movie 
	    JOIN casting 
	    	ON movie.id=movieid
	    JOIN actor 
	    	ON actor.id=actorid
	WHERE 
	  name= 'Julie Andrews') 
  AND ord=1
;
```

#### Queation 13- Actors with 15 leading roles

Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.

```sql
SELECT 
  DISTINCT name 
FROM 
  actor
    JOIN casting
	ON actorid=actor.id
WHERE 
  actorid IN(SELECT 
		actorid FROM casting
	     WHERE 
	     	ord = 1
	     GROUP BY 
	     	actorid
	     HAVING 
	     	COUNT(actorid) >= 15)
ORDER BY 
  name
;
```

#### Question 14-

List the films released in the year 1978 ordered by the number of actors in the cast, then by title.

```sql
SELECT 
  title, 
  COUNT(actorid)
FROM 
  movie 
    JOIN casting
	ON movie.id=movieid
WHERE 
  yr=1978
GROUP BY 
  title
ORDER BY 
  COUNT(actorid) DESC, 
  title
;
```

#### Question 15-

List all the people who have worked with 'Art Garfunkel'.

```sql
SELECT 
  name 
FROM 
  actor 
    JOIN casting
	ON actorid=actor.id
WHERE 
  name !='art garfunkel'
  AND movieid IN (SELECT 
  		    movieid
		  FROM 
		    movie 
		      JOIN casting
			ON movieid=movie.id 
		      JOIN actor 
			ON actorid=actor.id
WHERE 
  name ='art garfunkel')
; 
```

### Using NUll

NULL, INNER JOIN, LEFT JOIN, RIGHT JOIN

#### Question 1- 

Lst the teachers who have NULL for their department

```sql
SELECT 
  name 
FROM 
  teacher 
WHERE 
  dept IS NULL
;
```

#### Question 2-

Note the INNER JOIN misses the teachers with no department and the departments with no teacher.

```sql
SELECT 
  teacher.name, 
  dept.name
FROM 
  teacher 
    INNER JOIN dept
      ON teacher.dept=dept.id
;
````

#### Question 3- 

Use a different JOIN so that all teachers are listed.

```sql
SELECT 
  teacher.name, 
  dept.name
FROM 
  teacher 
     LEFT JOIN dept 
	ON teacher.dept=dept.id
; 
```

#### Question 4-

Use a different JOIN so that all departments are listed.

```sql
SELECT 
  teacher.name, 
  dept.name
FROM 
  teacher 
    RIGHT JOIN dept
	ON teacher.dept=dept.id
;
```

#### Question 5- Using the COALESCE function

Use COALESCE to print the mobile number. Use the number '07986 444 2266' if there is no number given. Show teacher name and mobile number or '07986 444 2266'

```sql
SELECT 
  name, 
  COALESCE(mobile,'07986 444 2266') 
    AS mobile
FROM 
  teacher
; 
```

OR

```sql
SELECT 
  name, 
  IFNULL(mobile,'07986 444 2266') 
    AS mobile
FROM 
  teacher
; 
```

#### Question 6- 

Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department.

```sql
SELECT 
  teacher.name 
    AS teacher, 
  COALESCE(dept.name, 'None') 
    AS department
FROM 
  teacher 
    LEFT JOIN dept 
	ON teacher.dept=dept.id
;
```

OR

```sql
SELECT 
  teacher.name 
    AS teacher,
  IFNULL(dept.name, 'None') 
    AS department
FROM 
  teacher 
    LEFT JOIN dept 
	ON teacher.dept=dept.id
;
```

#### Question 7-

Use COUNT to show the number of teachers and the number of mobile phones.

```sql
SELECT 
  COUNT(name),
  COUNT(mobile)
FROM 
  teacher
;
```

#### Question 8-

Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed.

```sql
SELECT 
  dept.name,
  COUNT(teacher.name)
FROM 
  teacher 
    RIGHT JOIN dept
	ON teacher.dept=dept.id
GROUP BY
  dept.name
;
```

#### Question 9-

Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise.

```sql
SELECT 
  name, 
  CASE 
    WHEN dept<=2 THEN 'Sci'
    ELSE 'Art'
    END
FROM 
  teacher
;
```

#### Question 10-

Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise.

```sql
SELECT 
  name, 
  CASE 
    WHEN dept<=2 THEN 'Sci'
    WHEN dept =3 THEN 'Art'
    ELSE 'None'
    END
FROM 
  teacher
;
```

### SELF JOIN

#### Question 1- 

How many stops are in the database.

```sql
SELECT 
  COUNT(id)
FROM 
  stops
;
```

### Question 2- 

Find the id value for the stop 'Craiglockhart'

```sql
SELECT 
  id
FROM
  stops
WHERE 
  name ='craiglockhart'
;
```

#### Question 3-

Give the id and the name for the stops on the '4' 'LRT' service.
*Note- The data model is flawed.  By naming one of the columns num and not actually be integers is misleading.  

```sql
SELECT 
  id, 
  name
FROM 
  stops, 
  route
WHERE 
  id=stop
  AND company='LRT'
  AND num=4
ORDER BY 
  pos
;
```

#### Question 4- Routes and stops

The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes.

```sql
SELECT 
  company, 
  num, 
  COUNT(*)
FROM 
  route 
WHERE 
  stop=149 
  OR stop=53
GROUP BY 
  company, 
  num
HAVING 
  COUNT(*)=2
;
```

<!--#### Question 5- 

Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road.

SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=53 and b.stop IN(SELECT stop FROM route JOIN stops ON route.stop=stops.id WHERE name='London Road');

#### Question 6- 

The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross'
-->


