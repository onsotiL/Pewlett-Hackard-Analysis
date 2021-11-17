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
The analysis demonstrated that a massive number of employers are due for retirement accross all departments
### Employees retiring by Department 
The number of employees retiring from each of the nine departments ranges between 2000 and 5000 in each department
![image](https://user-images.githubusercontent.com/90416094/142129861-d7b5906f-f693-48fd-b48b-6a6d514d35ba.png)

#### Employees retiring by job titles 
![image](https://user-images.githubusercontent.com/90416094/142129919-2aa323d1-5094-41c4-8472-9f3cab02dd2d.png)


#### The Employees Eligible for the Mentorship Program
To ensure upcoming vacant position will be filled, a Mentorship Eligibilty table showing employees born between January 1, 1965 and December 31, 1965 was created uisng the follwing commands in PgAdmin


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
    
## Looking into the future
1.	Summary: Provide high-level responses to the following questions, then provide two additional queries or tables that may provide more insight into the upcoming "silver tsunami."
o	How many roles will need to be filled as the "silver tsunami" begins to make an impact?

### There are a total of 300,024 empllyees at Pewlett Hackard
   
    SELECT COUNT (emp_no)
    FROM employees;
    
### The resulting table  shows a total of 1549 employees eligible for the the mentorship program.
     
    SELECT COUNT(me.emp_no)
    FROM mentorship_eligibilty as me

### The table new table bellow shows viable mentorship candidates by titles

     SELECT COUNT(title),title
     FROM mentorship_eligibilty as me
     GROUP BY title










o	Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?

Pewlett-Hackard-Analysis
