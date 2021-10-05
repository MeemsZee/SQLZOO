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









