# SQLZOO Answer key

## SELECT Basics

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

## SELECT from WORLD

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

Show the countries that are big by area or big by population.  Show name, population and area

```sql
SELECT name, population, area
FROM world
WHERE area> 3000000 OR population>250000000;
```







