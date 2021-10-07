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
	FROM world
	WHERE name='Germany'; 
```

#### Question 2- Scandinavia

Show the name and population of 'Sweden', 'Norway' and 'Denmark'

```sql
SELECT name, population 
    FROM world 
    WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

#### Question 3- Just the right size

Show the country and area for countries with an aera between 200,000 and 250,000 

```sql
SELECT name, area
    FROM world
    WHERE area 
    BETWEEN 200000 and 250000;
```

### SELECT from WORLD

#### Question 1- Introduction

Show name, continent and population of all countries

```sql
SELECT name, continent, population 
FROM world;
```

#### Question 2- Large Countries

Show the name for the countries that have a population of at least 200 million.

```sql
SELECT name
FROM world
WHERE population >200000000;
```

#### Question 3- Per capital GDP

Give the name and per capita GDP for those countries with a population of at least 200 million.  Hint: per capita GDP= GDP/population

```sql
SELECT name, GDP/population AS per_capita_GDP
FROM world
WHERE population >200000000;
```

#### Question 4- South America In millions

Show the name and population in millions for the countries of the continent 'South America'.  

```sql
SELECT name, population/1000000 as pop_per_million
FROM world
WHERE continent = 'South America';
```

#### Question 5- France, Germany, Italy

Show the name and population for France, Germany, Italy

```sql
SELECT name, population 
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```
#### Question 6- United

Show the countries which have name that includes the word 'United'

```sql
SELECT name
FROM world
WHERE name LIKE '%United%';
```

#### Question 7- Two ways to be big

Show the countries that are big by area or big by population.  Show name, population and area.

```sql
SELECT name, population, area
FROM world
WHERE area> 3000000 OR population>250000000;
```

#### Question 8- One or the other (but not both)

Show the countries that are big by area (more than 3 mil) or by population (more than 250 mil) but not both.  Show name, population and area. 

```sql
SELECT name, population, area 
FROM world 
WHERE area > 3000000 XOR population > 250000000;
```

OR

```sql
SELECT name, population, area 
FROM world 
WHERE (area > 3000000 AND population <250000000) OR (population > 250000000 and area <3000000);
```

#### Question 9- Rounding
Show the name and population in millions and the GDP in billions for the countires of the continent 'South America' to the nearnest hundredth. 

```sql
SELECT name, ROUND(population/1000000,2) AS pop_in_millions, ROUND(GDP/1000000000,2) AS GDP_in_billions 
FROM world 
WHERE continent = 'South America'; 
```

#### Question 10- Trillion dollar economies 

Show the name and per capita GDP for countries with a GDP of minimum 1 tillion rounded to nearest thousand. 

```sql
SELECT name, ROUND(GDP/population,-3)
FROM world
WHERE gdp > 1000000000000;
```

#### Question 11- Name and capital have the same length

Show the name and capital where the name and the capital have the same number of characters. 

```sql
SELECT name, capital 
FROM world 
WHERE LENGTH(name)= LENGTH(capital);
```

#### Question 12- Matching name and capital

Show the name and capital where the first letters of each match. Don't include countries where the name and the capital are the same word

```sql
SELECT name, capital 
FROM world 
WHERE LEFT(name,1)= LEFT(capital,1) and name <> capital;
```

#### Question 13- All the vowels

Find the country that has all the vowels and no spaces in its name.

```sql
SELECT name
FROM world
WHERE name LIKE '%a%' 
AND name LIKE '%e%' 
AND name LIKE '%i%'
AND name LIKE '%o%' 
AND name LIKE '%u%' 
AND name NOT LIKE '% %';
```

### SELECT from Nobel 

#### Question 1- Winners from 1950

Change existing query to display Nobel prices for 1950

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950;
```

#### Question 2- 1962 Literature

Show who won the 1962 prize for Literature

```sql
SELECT winner
FROM nobel 
WHERE yr = 1962
AND subject = 'literature';
```

#### Question 3- Albert Einstein

Show the year and subject that won 'Albert Einstein' his prize

```sql
SELECT yr, subject
FROM nobel 
WHERE winner= 'albert einstein';
```

#### Question 4- Recent Peace Prizes

Give the name of the 'Peace' winners since the year 2000, including 2000

```sql
SELECT winner
FROM nobel
WHERE yr >= 2000 and subject ='peace';
```

#### Question 5- Literature in the 1980s

Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive. 

```sql
SELECT *
FROM nobel
WHERE subject= 'literature'
and yr>=1980 and yr <=1989;
```
OR

```sql
SELECT yr, subject, winner
FROM nobel
WHERE subject= 'literature'
and yr>=1980 and yr <=1989;
```

#### Question 6- Only Presidents

Show all details of the presidental winners: Theodore Roosevelt, Woodrow Wilson, Jimmy Carter, Barack Obama

```sql
SELECT * 
FROM nobel 
WHERE winner IN ('theodore roosevelt', 'woodrow wilson', 'jimmy carter', 'barack obama'); 
```

#### Question 7- John 

Show the winners with the first name John

```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%';
```

#### Question 8- Chemistry and Physics from different years

Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984

```sql
SELECT yr, subject, winner
FROM nobel 
WHERE subject='physics' AND yr =1980
OR (subject='chemistry' AND yr = 1984);
```

#### Question 9- Exclude Chemists and Medics

Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine

```sql
SELECT yr, subject, winner
FROM nobel 
WHERE yr = 1980 
AND subject NOT IN ('Chemistry', 'Medicine');
```

#### Question 10- Early Medicine, Late Literature

Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later (after 2004, including 2004)

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject ='medicine' and yr<1910)
OR (subject='literature' and yr >=2004);
```
#### Question 11- Umlaut

Find all details of the prize won by Peter Grünberg. Hint: for macs hold press on u until options pop up and select the number corresponding to the letter desired

```sql
SELECT *
FROM nobel 
WHERE winner='peter grünberg';
```

#### Question 12- Apostrophe

Find all details of the prize won by Eugene O'Neill. Hint: to tell sql you want to keep the single quote, add another one directly after ('')

```sql
SELECT *
FROM nobel
WHERE winner= 'eugene o''neill';
```

#### Question 13- Knights of the realm

List the winners, year, and subject where the winner starts with Sir.  Show the most recent first, then by name order. 

```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'SIR%'
ORDER BY yr DESC, winner;
```

#### Question 14- Chemistry and Physics last

Show the 1984 winners and subject ordered by subject and winner name; bust list Chesmitry and Physics last. 

```sql
SELECT winner, subject
  FROM nobel
 WHERE yr=1984
 ORDER BY subject IN ('physics','chemistry'), subject, winner;
 ```
 
 OR
 
 ```sql
 SELECT winner, subject
  FROM nobel
 WHERE yr=1984
 ORDER BY 
CASE WHEN subject IN ('physics','chemistry')THEN 1 ELSE 0 END,
subject, winner;
```


### SELECT within SELECT

#### Question 1- Bigger than Russia

List each country name where the population is larger than that of 'Russia'. 

```sql
SELECT name
FROM world
WHERE population> 
(SELECT population 
From world
WHERE name='Russia');
```

#### Question 2- Richer than UK

Show the countries in Europe with a per capita GDP greater than 'United Kingdom'

```sql
SELECT name
FROM world
WHERE continent='europe'
AND GDP/population>
(SELECT gdp/population
FROM world
WHERE name= 'united kingdom');
```

#### Question 3- Neighbours of Argentina and Australia
List the name and continent of countries in the continent containing either Argentina or Australia.  Order by name of the country

```sql
SELECT name, continent
FROM world
WHERE continent= 
(SELECT continent 
FROM world
WHERE name='Australia')
OR continent= 
(SELECT continent
FROM world
WHERE name= 'Argentina')
ORDER BY name ASC;
```

#### Question 4- Between Cananda and Poland

Which country has a population that is more than Cananda but less than Poland? Show name and population

```sql
SELECT name, population 
FROM world
WHERE population> 
(SELECT population 
FROM world
WHERE name='Canada')
AND population<
(SELECT population 
FROM world
WHERE name ='poland');
```

#### Question 5- Percentages of Germany

Show the name and population of each country in Europe.  Show the population as a percentage of the population of Germany. 

```sql
SELECT name, CONCAT(ROUND(population/(SELECT population From world WHERE name='Germany')*100,0),'%')
FROM world
WHERE continent='europe';
```
#### Question 6- Bigger than every country in Europe

Which countries have a GDP greater than every country in Europe? Give the name only.  Hint: For the first query, the condition gdp>0 is imperative in the subquery.  Some countries have null for gdp.

```sql
SELECT name 
FROM world
WHERE gdp>
ALL(SELECT gdp 
FROM world
WHERE continent='europe'
and gdp>0); 
```
OR

```sql
SELECT name 
FROM world
WHERE gdp>
(SELECT MAX(gdp) 
FROM world
WHERE continent='europe');
```

#### Question 7- Largest in each continent

Find the largest country(by area) in each continent, show the continent, the name and the area. 

```sql

SELECT continent, name, area FROM world a
WHERE area >= ALL
(SELECT area FROM world b
WHERE a.continent=b.continent
AND area>0);
```

OR 

```sql
SELECT continent, name, area FROM world a
WHERE area =
(SELECT Max(area) FROM world b
WHERE a.continent=b.continent
AND area>0)
```

#### Question 8- First country of each continent

```sql
SELECT continent, name 
FROM world a
WHERE name=
(SELECT MIN(name) FROM world b WHERE a.continent=b.continent)
```

OR 
```sql
SELECT continent, name 
FROM world a
WHERE name<= ALL
(SELECT name FROM world b WHERE a.continent=b.continent)
```

#### Question 9- Difficult Questions that Utilize Techniques Not Covered In Prior Sections

Find the continents where all countires have a population <25000000.  Then find the names of the countries associated with these continents.  Show name, continent and population. 

```sql
SELECT name, continent, population 
FROM world a
WHERE 25000000>= 
ALL(SELECT population
FROM world b
WHERE a.continent=b.continent);
```

#### Question 10

Some countries have populations more than three times that of any of their neighbours (in the same continent).  Give the countries and continents

```sql
SELECT name, continent FROM world a 
WHERE population>= ALL(SELECT population*3 FROM world b
WHERE a.continent= b.continent AND b.name != a.name);
```

### SUM and COUNT

#### Question 1- Total world population

Show the total population of the world. 

```sql
SELECT SUM(population)
FROM world;
```

#### Question 2- List of continents

List all continents- just once each

```sql
SELECT Distinct(continent)
FROM world;
```

#### Question 3.  GDP of Africa

Give the total GDP of Africa

```sql
SELECT sum(gdp) 
FROM world
WHERE continent='africa';
```

#### Question 4. Count the big countries

How many countries have an area of at least 1000000

```sql
SELECT count(name) 
FROM world
WHERE area>=1000000;
```

#### Question 5- Baltic states population

What is the total population of ('Estonia', 'Latvia', 'Lithuania')

```sql
SELECT SUM(population)
FROM world
WHERE name IN ('estonia', 'latvia', 'lithuania');
```

#### Question 6- Counting the countries of each continent

For each continent show the continent and number of countries

```sql
SELECT continent, count(name)
FROM world
GROUP BY continent;
```

#### Question 7- Counting big countries in each continent

For each continent show the continent and number of countries with populations of at least 10 million. 

```sql
SELECT continent, COUNT(name)
FROM world
WHERE population>=10000000
GROUP BY continent;
```






