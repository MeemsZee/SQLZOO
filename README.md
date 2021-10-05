# SQLZOObasics

Q1. Show population of Germany.  Note: Don't use double quotation marks
  SELECT population 
    FROM world
    WHERE name='Germany'; 
  
Q2. Show the name and population of 'Sweden', 'Norway' and 'Denmark'
  SELECT name, population 
    FROM world 
    WHERE name IN ('Sweden', 'Norway', 'Denmark');
    
Q3. Show the country and area for countries with an aera between 200,000 and 250,000. 
  SELECT name, area
    FROM world
    WHERE area 
    BETWEEN 200000 and 250000
