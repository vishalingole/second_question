# second_question

In question number two, need to find below things as:

1.All available departments.
2.Department wise Male and female employees of each departments
3.The "Decade" tearm in question stands for 10 year duration, for this I have taken 10 year group as: 
 3.1 1981 -1990
 3.2 1991-2000
 3.3 2001-2010
 3.4 2011-2020
 
 Now to get the required output I have used the Hive and Pig.
 
 First in Hive I have used below query as:
 
 " INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/sales_male_1991_2000' row format delimited fields terminated by ',' select d.dept_name,'1991-2000' as col3,e.gender,s.salary,de.from_date from employees e left join salaries s on (s.emp_no = e.emp_no) left join dept_emp1 de on (e.emp_no = de.emp_no) left join departments d on(d.dept_no = de.dept_no) where (de.from_date between 1991 AND 2000 OR de.to_date between 1991 AND 2000) AND e.gender LIKE 'M' AND d.dept_name LIKE '%Sales%' order by de.from_date; "
 
 Using above query I got the all Male employees of Sales department under the 1991 to 2000 decade.
 
in this way using above qury will get the all department wise , decade wise , gender wise required list of employees.

Now using below Pig script  I have calculated the Average salary by department, its decade, and then gender wise and script as:

"
employee_details = LOAD '/usr/sales_male_1981_1990/000000_0' USING PigStorage(',') as (dept_name:chararray,col3:chararray, gender:chararray, salary:int,from_date:chararray);
employee_group_all = Group employee_details All;
employee_sal_avg = foreach employee_group_all  Generate
  AVG(employee_details.salary);
STORE employee_sal_avg INTO 'file:///home/vishal/Desktop/sales_male_1981_1990_Avg_csv';

".

using this pig script will  get the other department wise, decade wise and gender wise average salary.

File Details:

1."sales_female_1981_1990", here the Sales department, all female employees under the  1981 to1990 decade list with required columns.
2."sales_female_1981_1990_Avg_csv" here the average salary of sales department all female employees under 1981 to 1990 decade.
3."sales_female_1991_2000" here the Sales department, all female employees under the  1991 to 2000 decade list with required columns.
4."sales_male_1981_1990" here the Sales department, all male employees under the  1981 to1990 decade list with required columns.
5."sales_male_1981_1990_Avg_csv" here the average salary of sales department all male employees under 1981 to 1990 decade.
6."sales_male_1991_2000" here the Sales department, all male employees under the  1991 to 2000 decade list with required columns.
7."Execution Process" file includes the terminal execuation process and the used query details.

 
 
 
