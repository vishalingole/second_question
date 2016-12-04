# second_question

In question number two, need to find below things as:

1.All available departments.
2.Department wise Male and female employees of each departments
3.The "Decade" tearm in question stands for 10 year duration, for this I have taken 10 year group as: 
 3.1 1981 -1990
 3.2 1991-2000
 3.3 2001-2010
 3.4 2011-2020
 
 * Please find steps detail below:
 
# Following HIVE query is used to get the males from sales department in the decade of 1991-2000
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/sales_male_1991_2000' row format delimited fields terminated by ',' select d.dept_name,'1991-2000' as col3,e.gender,s.salary,de.from_date from employees e left join salaries s on (s.emp_no = e.emp_no) left join dept_emp1 de on (e.emp_no = de.emp_no) left join departments d on(d.dept_no = de.dept_no) where (de.from_date between 1991 AND 2000 OR de.to_date between 1991 AND 2000) AND e.gender LIKE 'M' AND d.dept_name LIKE '%Sales%' order by de.from_date;

# Following PIG script is used to get the desired output. It takes csv file as input which is genrated by HIVE
employee_details = LOAD '/home/vishal/Downloads/sales_male_1991_2000/000000_0' USING PigStorage(',') as (dept_name:chararray,col3:chararray, gender:chararray, salary:int,from_date:chararray);
employee_group_all = Group employee_details All;
employee_sal_avg = foreach employee_group_all  Generate
  flatten(employee_details),AVG(employee_details.salary);
STORE employee_sal_avg INTO 'file:///home/vishal/Desktop/sales_male_1991_2000_Avg_csv';

# Following HIVE query is used to get the males from sales department in the decade of 1981-1990
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/sales_male_1981_1990' row format delimited fields terminated by ',' select d.dept_name,'1991-2000' as col3,e.gender,s.salary,de.from_date from employees e left join salaries s on (s.emp_no = e.emp_no) left join dept_emp1 de on (e.emp_no = de.emp_no) left join departments d on(d.dept_no = de.dept_no) where (de.from_date between 1981 AND 1990 OR de.to_date between 1981 AND 1990) AND e.gender LIKE 'M' AND d.dept_name LIKE '%Sales%' order by de.from_date;

# Following PIG script is used to get the desired output. It takes csv file as input which is genrated by HIVE
employee_details = LOAD '/home/vishal/Downloads/sales_male_1981_1990/000000_0' USING PigStorage(',') as (dept_name:chararray,col3:chararray, gender:chararray, salary:int,from_date:chararray);
employee_group_all = Group employee_details All;
employee_sal_avg = foreach employee_group_all  Generate
  flatten(employee_details),AVG(employee_details.salary);
STORE employee_sal_avg INTO 'file:///home/vishal/Desktop/sales_male_1981_1990_Avg_csv';

# Following HIVE query is used to get the females from sales department in the decade of 1981-1990
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/sales_female_1981_1990' row format delimited fields terminated by ',' select d.dept_name,'1991-2000' as col3,e.gender,s.salary,de.from_date from employees e left join salaries s on (s.emp_no = e.emp_no) left join dept_emp1 de on (e.emp_no = de.emp_no) left join departments d on(d.dept_no = de.dept_no) where (de.from_date between 1981 AND 1990 OR de.to_date between 1981 AND 1990) AND e.gender LIKE 'F' AND d.dept_name LIKE '%Sales%' order by de.from_date;

# Following PIG script is used to get the desired output. It takes csv file as input which is genrated by HIVE
employee_details = LOAD '/home/vishal/Downloads/sales_female_1981_1990/000000_0' USING PigStorage(',') as (dept_name:chararray,col3:chararray, gender:chararray, salary:int,from_date:chararray);
employee_group_all = Group employee_details All;
employee_sal_avg = foreach employee_group_all  Generate
  flatten(employee_details),AVG(employee_details.salary);
STORE employee_sal_avg INTO 'file:///home/vishal/Desktop/sales_female_1981_1990_Avg_csv';
 

 
 
