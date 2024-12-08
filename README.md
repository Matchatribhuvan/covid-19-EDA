# covid-19-EDA
Exploratory Data Analysis (EDA) is an essential process in data analysis, especially when working with complex datasets like COVID-19. The goal of EDA is to summarize and visualize key aspects of the data to understand its structure, uncover underlying patterns, detect anomalies, and formulate hypotheses. Given the queries above, the focus is on examining the relationships between various COVID-19 metrics such as total cases, total deaths, population size, and death rates across different locations. Below is a description of how these queries contribute to the EDA for COVID-19 data

sql queries

select * from coviddeaths
order by 3,4;
select * from covidvaccines
order by 3,4;
select location,c_date,total_cases,new_cases,total_deaths,population
from coviddeaths
order by 1,2;
--total cases vs total deaths
select location,c_date,total_cases,total_deaths,(total_deaths/nullif(total_cases,0))*100 as death_percentage
from coviddeaths
order by 1,2;
--lets see in a particular location
select location,c_date,total_cases,total_deaths,(total_deaths/nullif(total_cases,0))*100 as death_percentage
from coviddeaths
where location like '%India%'
order by 1,2;
--lets see total cases vs population
select location,c_date,total_cases,population,(total_deaths/nullif(population,0))*100 as case_percentage
from coviddeaths
where location like '%India%'
order by 1,2;
--lokking at countries with highest infection rate
select location,max(total_cases) as highinfectioncount,population,max((total_deaths/nullif(population,0)))*100 as percent_population_infected
from coviddeaths
GROUP BY location,population
order by 1,2;
