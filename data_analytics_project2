SELECT *
FROM FirstProject..CovidDeaths

SELECT location, date, total_cases, total_deaths, population
FROM FirstProject..CovidDeaths

-- Total Cases vs Total Deaths

SELECT location, date, total_cases, total_deaths, 
       (total_deaths/total_cases) * 100 AS death_percentage
FROM FirstProject..CovidDeaths 
WHERE location IS NOT NULL
ORDER by location

-- Total Cases vs Total possible recoveries

SELECT location, date, total_cases, total_deaths,  (total_deaths/total_cases) * 100 AS death_percentage,
	   ((total_cases - total_deaths)/total_cases) * 100 AS possible_recovered_percentage
FROM FirstProject..CovidDeaths
WHERE location IS NOT NULL
ORDER by location


-- Total Cases vs Population
SELECT location, date, total_cases, total_deaths, population, 
       (total_cases/population) * 100 AS population_infected_percentage  
FROM FirstProject..CovidDeaths
WHERE location IS NOT NULL
ORDER BY location

-- Countries with Highest Infection Rate compared to Population

SELECT location, population, 
       MAX(total_cases/population) * 100 AS percent_infection_perpopulation
FROM FirstProject..CovidDeaths
GROUP BY location, population
ORDER BY percent_infection_percountry DESC

-- Infection rate in Africa compared to its population

SELECT location AS country, population, MAX(total_cases) AS highest_infection_record, 
       MAX(total_cases/population) * 100 AS percent_infected_perpopulation
FROM FirstProject..CovidDeaths
WHERE continent = 'Africa'
GROUP BY location, population
ORDER BY percent_infected_perpopulation DESC

-- Infection rate in Europe compared to its population

SELECT location AS country, population, MAX(total_cases) AS highest_infection_record, 
       MAX(total_cases/population) * 100 AS percent_infected_perpopulation
FROM FirstProject..CovidDeaths
WHERE continent = 'Europe' 
GROUP BY location, population
ORDER BY percent_infected_perpopulation, country DESC 


-- Countries with Highest Death Count per Population

SELECT location AS country, population, MAX(CAST(total_deaths AS INT)) AS total_death_count,
       MAX(total_deaths/population) * 100  AS percent_death_record
FROM FirstProject..CovidDeaths
WHERE population IS NOT NULL
GROUP BY location, population
ORDER BY percent_death_record DESC

-- Continents with highest death count 

SELECT continent, MAX(CAST(total_deaths AS INT)) AS total_death_count,
       MAX(total_deaths/population) * 100 AS percent_death_record
FROM FirstProject..CovidDeaths
WHERE continent IS NOT NULL
GROUP BY continent
ORDER BY percent_death_record DESC



SELECT continent, SUM(CAST(new_deaths AS INT)) AS total_deaths, SUM(new_cases) AS total_cases, 
SUM(CAST(new_deaths AS INT))/SUM(new_cases) * 100 AS percentdeath
FROM FirstProject..CovidDeaths
WHERE continent IS NOT NULL
GROUP BY continent
ORDER BY percentdeath DESC


WITH perpop_vaccinated (continent, location, date, population, new_vaccinations, vaccination_updates)
as
(
 SELECT cd.continent, cd.location, cd.date, v.population, v.new_vaccinations,
 SUM(CONVERT(INT, v.new_vaccinations)) OVER (PARTITION BY cd.location ORDER BY cd.location) as vaccination_updates
 FROM FirstProject..CovidDeaths cd
 JOIN FirstProject..CovidDeaths v
 ON cd.location = v.location
 AND cd.date = v.date
 WHERE cd.continent IS NOT NULL
)

SELECT *, (vaccination_updates/population) * 100 AS percent_vaccinated
FROM perpop_vaccinated


CREATE VIEW VaccinatedPopulation AS
SELECT *, (vaccination_updates/population) * 100 AS percent_vaccinated
FROM perpop_vaccinated








