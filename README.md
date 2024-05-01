# Employee-Analysis

#### All questions were solved, and retrieved data using various SQL Queries,I then transfer the result table into Excel for more analysis 
Queries used to perform this analysis with the interpretation is found in the text document attached to this repository post.

## Unveiling Insights: Analyzing Employee Data Using SQL

In today’s competitive business landscape, companies increasingly recognize the significance of data-driven decision-making across all operations. One crucial area where data analysis plays a pivotal role is in understanding and managing the workforce. Analyzing employee data provides invaluable insights that can drive strategic HR decisions, optimize organizational performance, and foster a positive workplace culture.

The dataset was transformed into a CSV file and then loaded into SQL Server for analysis.

## Why SQL?

SQL allows analysts to retrieve and manipulate data stored in relational databases efficiently. With SQL queries, analysts can extract specific subsets of employee data based on criteria such as department, tenure, performance metrics, and more. This capability enables targeted analysis and provides insights into various aspects of the workforce.

## Overview of Analytical Questions

This post will delve into a comprehensive analysis of employee data using SQL. We’ll explore various aspects of the workforce, uncovering insights that can inform strategic decisions and improve organizational performance. Here’s an overview of the questions we’ll be exploring:

1. Demographic Analysis

2. Salary Analysis

3. Tenure Analysis

4. Departmental Analysis

5. Performance Analysis

6. Geographic Analysis

7. Exit Analysis

8. Ethnicity and Age Analysis

#### Through these analyses, we’ll gain valuable insights into the composition, performance, and dynamics of the workforce, enabling informed decision-making and strategic planning within the organization. Let’s dive into each question and uncover actionable insights from the data using SQL.

#### All questions were solved, and retrieved data using various SQL Queries,I then transfer the result table into Excel for more analysis 
Queries used to perform this analysis with the interpretation is found in the text document attached to this repository post. And you can also visit my Medium Page for more explicit detail and Result tables of this analysis via this link https://medium.com/@Esther.0/unveiling-insights-analyzing-employee-data-using-sql-f8e26c584959

## Demographic Analysis

a. Gender Distribution

Query: Calculate the count of employees categorized by gender.

SELECT Gender, COUNT(Gender) AS Gender_Count
FROM [Employee _Data]
GROUP BY Gender

### Result Interpretation:

The male has a total count of 485

The female has a total count of 515

b. Age Group Distribution

Query: Determine the distribution of employees into age groups, using CASE.

SELECT
CASE
WHEN Age < = 35 THEN 'Young'
WHEN Age BETWEEN 35 AND 50 THEN 'Mid_Aged'
ELSE 'Senior'
END AS Age_group,
COUNT (*) AS Employee_Count
FROM [Employee _Data]
GROUP BY
CASE
WHEN Age < = 35 THEN 'Young'
WHEN Age BETWEEN 35 AND 50 THEN 'Mid_Aged'
ELSE 'Senior'
END;

### Result Interpretation:

The age group “Mid_Aged” (ages 35 to 50) has the highest employee count, totaling 414. The “Senior” age group (aged 51 and above) follows with a total employee count of 337, while the “Young” age group (aged 35 and below) comprises 249 employees.

c. Ethnicity Categorization

First, find the Distinct Ethnicity in the Company
Query:

SELECT DISTINCT Ethnicity
FROM
[Employee _Data]

### Result Interpretation:

There are 4 distinct Ethnicity in the Company namely:
Asian
Latino
Caucasian
Black

Categorize employees by ethnicity.
Query:

SELECT
CASE
WHEN Ethnicity = 'Asian' THEN 'Asian'
WHEN Ethnicity = 'Caucasian' THEN 'Caucasian'
WHEN Ethnicity = 'Latino' THEN 'Latino'
ELSE 'Black'
END AS Ethnicity_Category,
COUNT (*) Ethnicity_Count
FROM
[Employee _Data]
GROUP BY
CASE
WHEN Ethnicity = 'Asian' THEN 'Asian'
WHEN Ethnicity = 'Caucasian' THEN 'Caucasian'
WHEN Ethnicity = 'Latino' THEN 'Latino'
ELSE 'Black'
END
ORDER BY
Ethnicity_Count DESC

## Result Interpretation:

In the company, Asian ethnicity represents the largest group with a total count of 432 employees. Latino ethnicity follows with a total count of 279 employees, while Caucasian ethnicity comprises 222 employees. The count of Black ethnicity is 67 employees.

## Salary Analysis

Categorize employees by their salary range: ‘Low’, ‘Medium’, and ‘High’
SELECT
CASE
WHEN Annual_Salary < 60000 THEN 'Low'
WHEN Annual_Salary BETWEEN 60000 AND 100000 THEN 'Medium'
ELSE 'High'
END AS Salary_Category,
COUNT (*) Salary_Category
FROM
[Employee _Data]
GROUP BY
CASE
WHEN Annual_Salary < 60000 THEN 'Low'
WHEN Annual_Salary BETWEEN 60000 AND 100000 THEN 'Medium'
ELSE 'High'
END

### Result Interpretation:

Employees earning above $100,000 (categorized as “High”) have the highest count, totaling 425. Employees that earn below $60,000 (categorized as “Low”) comprise 156 employees, while the “Medium” salary earner, earning between $60,000 and $100,000 includes 419 employees.

Determine the average salary for each job title, categorizing them into ‘Low’, ‘Medium’, and ‘High’ based on salary.
SELECT Job_Title, AVG(Annual_Salary) AS Average_Salary
FROM
[Employee _Data]
GROUP BY Job_Title
ORDER BY
Average_Salary DESC

Finding:

Vice President has the highest average salary with a value of $220125.787

## Tenure Analysis

Categorize employees by their tenure with the company: ‘Less than 5 years’, ‘5 to 10 years’, and ‘More than 10 years’.
SELECT Employee_ID, Full_Name, Hire_Date,
CASE
WHEN DATEDIFF(YEAR, Hire_Date, 
GETDATE()) < 5 THEN 'Less than 5 years'
WHEN DATEDIFF(YEAR, Hire_Date, GETDATE()) >=5 AND DATEDIFF(YEAR, Hire_Date, 
GETDATE()) <=10 THEN '5 to 10 years'
ELSE 'More than 10 years'
END AS Tenure_category
FROM [Employee _Data]

GETDATE() was used to get the current date, then DATEDIFF() subtracts the current date from the hire date on a year interval,

### Result
“According to the analysis, most employees in the company, totaling 481 individuals, have worked for over 10 years. This group constitutes 48.1% of the company’s workforce.”

Determine the average tenure for each job title, categorized into ‘Short’, ‘Medium’, and ‘Long’ tenures.
SELECT Job_Title,
CASE
WHEN tenure < 5 THEN 'Short'
WHEN tenure >= 5 AND tenure <= 10 THEN 'Medium'
ELSE 'Long'
END AS tenure_category,
AVG(tenure) AS average_tenure
FROM
(
SELECT
Job_Title,
DATEDIFF(YEAR, Hire_Date, GETDATE()) AS tenure
FROM
[Employee _Data]
) AS employee_tenure
GROUP BY
Job_Title,
CASE
WHEN tenure < 5 THEN 'Short'
WHEN tenure >= 5 AND tenure <= 10 THEN 'Medium'
ELSE 'Long'
END;

## Result Interpretation:

The employee that has stayed more than 10 years (Long) has a total count of 603 while between 5 to 10 years (Medium) has a total count of 223 Short (5 years and below) has a total of 82.

## Departmental Analysis
Categorize employees by their department and determine the average age for each department.
SELECT
Department,
AVG (Age) AS average_age
FROM [Employee _Data]
GROUP BY
Department;

### Result Interpretation:
The marketing department has an average age of 41 years. The sales department has an average age of 43 years. The engineering department has an average age of 45 years. The IT department has an average age of 44 years. The Human Resources department has an average age of 45 years. The Finance department has an average age of 45 years. The Accounting department has an average age of 44 years.

## Performance Analysis:

Categorize employees by their bonus amount: ‘No Bonus’, ‘Low Bonus’, and ‘High Bonus’.

Query:

SELECT Bonus,
CASE
WHEN Bonus = '0%' THEN 'No Bonus'
WHEN Bonus != '0%'AND Bonus <='20%' THEN 'Low Bonus'
ELSE 'High Bonus'
END AS Bonus_category
FROM [Employee _Data]

### Interpretation and Finding:

Employees receiving no bonus, categorized as “No Bonus,” account for 57.60% of the total. Those receiving a bonus ranging from 1% to 20%, classified as “High Bonus,” make up 27.00% of the total, with the remaining 15.40% categorized as “Low Bonus.”

## Geographic Analysis:

a. Categorize employees by their country and determine the average salary for each country.

SELECT Country,
AVG (Annual_Salary) AS Average_Salary
FROM [Employee _Data]
GROUP BY Country

### Interpretation and Finding:

According to the analysis, Brazil has the highest sum of average salaries, totaling $110,281.44, representing 33.70% of the sum total.

b. Identify the city with the highest number of employees, categorizing them into ‘Small’, ‘Medium’, and ‘Large’ cities based on employee count.

SELECT 
    City,
    CASE
        WHEN COUNT(*) < (SELECT MAX(emp_count) * 0.3
 FROM (SELECT city, COUNT(*) as emp_count FROM [Employee _Data] GROUP BY city)
AS emp_counts) THEN 'Small'
        WHEN COUNT(*) < (SELECT MAX(emp_count) * 0.7
 FROM (SELECT city, COUNT(*) as emp_count FROM [Employee _Data] GROUP BY city) 
AS emp_counts) THEN 'Medium'
        ELSE 'Large'
    END AS city_category
FROM 
    [Employee _Data]
GROUP BY 
    City;
    
## Exit Analysis:

a. Categorize employees based on their exit status: ‘Active’ for employees who are still with the company and ‘Exited’ for those who have left.

SELECT Employee_ID, Full_Name,
  CASE
    WHEN Exit_Date IS NULL THEN 'Active'
    ELSE 'Exited'
     END AS Employment_Status
 FROM 
 [Employee _Data]

### Interpretation and Findings:

According to the analysis, 89.70% of employees are still active and currently working at the company. This indicates a very high level of employee retention and integrity within the organization.

b. Determine the average tenure for employees who have exited the company, categorizing them into ‘Short’, ‘Medium’, and ‘Long’ tenures based on their duration with the company before exit.

SELECT
    CASE
        WHEN AVG(DATEDIFF(day, Exit_Date, GETDATE())) < 365 THEN 'Short'
        WHEN AVG(DATEDIFF(day, Exit_Date, GETDATE())) < 1095 THEN 'Medium'
        ELSE 'Long'
    END AS tenure_category,
    COUNT(*) AS count_of_employees
FROM
    [Employee _Data]
WHERE
    Exit_Date IS NOT NULL;
    
### Finding:

Analysis shows that employees that have exited the company have worked long term, more than 3 years which represents they worked for more than 1095 days

## Ethnicity and Age Analysis:

a. Categorize employees by their ethnicity and age group, such as ‘Asian — Young’, ‘Black — Mid-aged’, ‘Caucasian — Senior’, etc.

SELECT
    CASE 
        WHEN Ethnicity = 'Asian' AND Age < 30 THEN 'Asian-Young'
        WHEN Ethnicity = 'Asian' AND Age >= 30 AND Age <= 50 THEN 'Asain-Mid-aged'
        ELSE 'Asain-Senior'
    END AS category,
    COUNT(*) AS count_of_employees
FROM
    [Employee _Data]
GROUP BY
CASE 
       WHEN Ethnicity = 'Asian' AND Age < 30 THEN 'Asian-Young'
        WHEN Ethnicity = 'Asian' AND Age >= 30 AND Age <= 50 THEN 'Asain-Mid-aged'
        ELSE 'Asain-Senior'
    END;
Finding:

Asain-Senior employees have a total of 71.80% while Asain-Mid-aged 23.40% and Asian-Young 4.80%

note: Replace Asian Ethnicity with Black to get for Black, Caucasian to get for Caucasian, and Latino to get Latino
