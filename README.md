# Pewlett-Hackard-Analysis
#### Data Source
 SIX CSV files including
- departments.csv 
- employees.csv,
- dept_emp.csv, 
- dept_manager.csv, 
- salaries.csv, 
- titles.csv

#### Software
- SQL, PostgreSQL, pgAdmin

## Overview of the analysis
Pewlett Hackard, a huge company with thousands of employees, is in the process of planning for the future of the company since many of its baby boomers are beginning to retire. In an effort to ensure the continuity of the company, a thorough analysis is necessary to determine the employees who will be retiring and positions that will be left vacant as a result. The analysis focused on the following

- Determining the number of retiring employees 
- Determining the number of retiring employees per title,
- Identifying employees who are eligible to participate in a mentorship program.
- Creating tailored lists for specific departments

## Results
The analysis demonstrated that a massive number of employers are due for retirement across all departments

#### Employees retiring by job titles 
The table below shows the number of employees retiring according to their job title 

![image](https://user-images.githubusercontent.com/90416094/142129919-2aa323d1-5094-41c4-8472-9f3cab02dd2d.png)

    
## Looking into the future

### There are a total of 300,024 employees at Pewlett Hackard
   
    SELECT COUNT (emp_no)
    FROM employees;
    
    
   ![image](https://user-images.githubusercontent.com/90416094/142255980-657e14d3-2a18-4ce7-b8f7-57428282683d.png)

#### The number of employees who are eligible for retirement are 
### 90,398

![image](https://user-images.githubusercontent.com/90416094/142255900-a766df59-95a8-4ad6-bec9-05596a243023.png)

#### The Employees Eligible for the Mentorship Program

To ensure upcoming vacant position will be filled, a Mentorship Eligibility analysis showing employees born between January 1, 1965 and December 31, 1965 was created using the following commands in PgAdmin

          SELECT DISTINCT ON (em.emp_no) em.emp_no,
          em.first_name,
	      em.last_name, 
	      em.birth_date,
	      de.from_date,
	      de.to_date,  
	      ti.title
    INTO mentorship_eligibilty
    FROM employees as em
    LEFT JOIN dept_emp as deON (em.emp_no = de.emp_no)
    LEFT JOIN titles as ti
    ON (em.emp_no = ti.emp_no)
    WHERE (de.to_date = '9999-01-01') AND 
    (em.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
    ORDER BY em.emp_no;	

### The resulting table shows a total of 1549 employees eligible for the the mentorship program.
     
    SELECT COUNT(me.emp_no)
    FROM mentorship_eligibilty as me
    
![image](https://user-images.githubusercontent.com/90416094/142222533-4d83c40c-1d59-4913-be3e-66ba009ba8a2.png)

### The table new table below shows viable mentorship candidates by titles

     SELECT COUNT(title),title
     FROM mentorship_eligibilty as me
     GROUP BY title

![image](https://user-images.githubusercontent.com/90416094/142222726-4f77a9ab-7a76-473d-a638-6546bc79af86.png)

## Summary:

Pewlett Hackard has a total of 300,024 total employees. Of these employees, 90,398 are due for retirement. This is about a third of its entire workforce.  However, only 1549 employees are eligible for the mentorship program. This is not nearly enough to cover the upcoming vacant positions
