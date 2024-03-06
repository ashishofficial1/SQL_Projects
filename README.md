# SQL_Project
In this project 
I used absentees data of employees of a company and on the basis of these data
I created a project in which I filter that data in in MYSQl and then build a dashboard on Power BI.





Code used for filtering useful data in MYSQL

show databases;
use new;
show tables;
-- Create a join table --
select * from absent a
left join compensation b
on a.ID = b.ID 
left join reasons r
on a.`Reason for absence` = r.Number;

-- Find the healthiest --
select * from absent where `Social drinker` = 0 and `Social smoker` = 0 
and `Body mass index` < 25 and
`Absenteeism time in hours` < (select avg(`Absenteeism time in hours`) from absent);

-- Compensation rate increase for non-smokers / budget $983,221 so .68 increase per hour / $1414.4 per year --
select count(*) as NonSmokers from absent where `Social smoker` = 0 ;

-- optimize this query --

select 
a.ID,
r.Reason,
`Month of absence`,
`Body mass index`,
case when `Body mass index` < 18.5 then 'Underweight'
     when `Body mass index` between 18.5 and 25 then 'Healthy Weight'
     when `Body mass index` between 25 and 30 then 'Overweight'
     when `Body mass index` > 30 then 'Obese'
     else 'Unknown' end as BMI_Cotegory,
case when `Month of absence` in (12, 1, 2) then 'Winter'
	 when `Month of absence` in (3, 4, 5) then 'Spring'
	 when `Month of absence` in (6, 7, 8) then 'Summer'
	 when `Month of absence` in (9, 10, 11) then 'Fall'
     else 'Unknown' end as Season_names,
     `Month of absence`,
`Day of the week`,
`Transportation expense`,
Education,
Son,
`Social drinker`,
`Social smoker`,
Pet,
`Disciplinary failure`,
Age,
`Work load Average/day`,
`Absenteeism time in hours`
from absent a
left join compensation b
on a.ID = b.ID 
left join reasons r
on a.`Reason for absence` = r.Number;


After filtering these data in MYSQL I uploaded these data in Power BI and make a beautiful dashboard.
