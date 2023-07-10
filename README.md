# HRdata
HR data analysis
-- check data
describe hrdata;
select * from hrdata;

-- Data cleaning
alter table hrdata
change column ï»¿emp_no emp_id int;

-- Data analysis

select count(employee_count) from hrdata;

-- employee count by gender
select gender, count(gender) gender_count from hrdata
group by gender;

-- count of attrition by gender
select gender, count(gender) gender_count, count(attrition) as attrition from hrdata where attrition='Yes'
group by gender;

-- count of attrition by department
select department, count(attrition) from hrdata
where attrition='Yes'
group by department;

-- Attrition rate
select round((select count(attrition) from hrdata
where attrition='Yes')/ count(employee_count) * 100,2)	 as attritionrate from hrdata;

-- Active employees
select sum(employee_count)- (select count(attrition) from hrdata
where attrition='Yes') as active_employees from hrdata ;

-- Active male employees
select sum(employee_count)- (select count(attrition) from hrdata
where attrition='Yes'and gender='Male' ) as active_employees from hrdata where gender='Male' ;

-- Avg age of employees

select gender, round(avg(age),0) as avg_age from hrdata group by gender order by avg_age desc;



