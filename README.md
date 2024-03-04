# Data analysis using Covid Data
This my first project on data analysis, Please go through the following sql queries.


--- First project

--- let's preview our covid deaths data

select *
from first-project-396509.covid_data.covid_deaths
order by 1,2

--- let's check covid vaccines data

select *
from first-project-396509.covid_data.covid_vaccines
order by 1,2

---/

select continent, location, total_deaths
from first-project-396509.covid_data.covid_deaths
where continent is not null
order by 1,2


-- Total deaths by country

select location,max(total_deaths) as Total_deaths
from first-project-396509.covid_data.covid_deaths
group by location

-- Total deaths by continent

select continent,max(total_deaths) as Total_deaths
from first-project-396509.covid_data.covid_deaths
where continent is not null
group by continent


-- Total Cases vs Total Deaths & How much percent of infected people died by date
select location, date, total_deaths, Total_cases,(total_deaths/total_cases)*100 as Deathpercentage
from first-project-396509.covid_data.covid_deaths
where total_deaths is not null and total_cases is not null
order by 1,2

-- Total Newvaccines recorded daily
Select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations
From first-project-396509.covid_data.covid_deaths  dea
Join first-project-396509.covid_data.covid_vaccines  vac
	On dea.location = vac.location
	and dea.date = vac.date
where dea.continent is not null 
order by 2,3

-- Total vaccines and deaths of peoples due to covid in countries
Select dea.location, dea.population, max(vac.people_fully_vaccinated)as Peoplevaccinated, max(dea.total_deaths)as Totaldeaths,max(dea.total_cases)as Totalcases
From first-project-396509.covid_data.covid_deaths  dea
Join first-project-396509.covid_data.covid_vaccines  vac
	On dea.location = vac.location
	and dea.date = vac.date
where dea.continent is not null 
group by dea.location,dea.population
order by population desc
