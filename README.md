# SQL Practice — Portfolio

This folder contains my SQL learning and practice exercises from Google cybersecurity professionals certificate course, documented with screenshots.  
It demonstrates the AND, OR, and NOT operators in SQL to filter for information.  
All sensitive/personal data has been replaced with placeholders.

## Scenario
I am a security professional at a large organization. Part of my job is to investigate security issues to help keep the system secure. I recently discovered some potential security issues that involve login attempts and employee machines.

My task is to examine the organization’s data in their employees and log_in_attempts tables. Here, I'm using SQL filters to retrieve records from different datasets and investigate the potential security issues.

## Organization database table format

The organization database contains the following two tables:

- <mark>log_in_attempts</mark>
- <mark>employees</mark>

### log_in_attempts
The log_in_attempts table has the following columns:

- <mark>event_id</mark>: The identification number assigned to each login event
- <mark>username</mark>: The username of the employee
- <mark>login_date</mark>: The date the login attempt was recorded
- <mark>login_time</mark>: The time the login attempt was recorded
- <mark>country</mark>: The country where the login attempt occurred
- <mark>ip_address</mark>: The IP address of that employee’s machine
- <mark>success</mark>: The success of the login attempt; FALSE indicates a failed attempt

 
In the MariaDB shell, these columns are returned as:

![Organization database table](columns-1.png "Organization Database Table 1")


### employees
The employees table has the following columns:
- <mark>employee_id</mark>: The identification number assigned to each employee
- <mark>device_id</mark>: The identification number assigned to each device used by the employee
- <mark>username</mark>: The username of the employee
- <mark>department</mark>: The department the employee is in
- <mark>office</mark>: The office the employee is located in
  
In the MariaDB shell, these columns are returned as:

![Organization database table](columns-2.png "Organization Database Table 2")



## 🗄️ Practice Highlights

### 1. Retrive After Hours login attempts
- **Goal:** My team is investigating failed login attempts that were made after business hours. I want to retrieve this information from the login activity. Office hours end at '18:00'.
    
- **Why it matters:** All the login attemps are stored in the databse. By filtering the failed login attempts made after <mark>'18:00'</mark> I can identify potential threats like Brute-force attacks, compromised accounts, credential stuffing and misconfigurations. It is a part of my daily SOC monitoring.

- **The SQL Query:** ```SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = FALSE;```

  
- **How this works:** The <mark>login_time</mark> column in the <mark>log_in_attempts</mark> table contains information on when login attempts were made.
The <mark>success</mark> column in the <mark>log_in_attempts</mark> table contains values of <mark>TRUE</mark> or <mark>FALSE</mark> to indicate whether the login was successful. MySQL stores Boolean values as 1 for <mark>TRUE</mark>, and 0 for <mark>FALSE</mark>. This means that <mark>TRUE</mark> is represented as 1, and <mark>FALSE</mark> represented as 0 in the <mark>success</mark> column. In the shell screenshot I can see that 19 failed login attempts were made after '18:00' which means someone is trying to infiltrate the database.

**In MariaDB Shell**  

![Create table](sql-query-1.png "Query")
![Create table](sql-query-2.png "Result")


### 2. Retrive login attempts on a specific date
- **Goal:** Your team is investigating a suspicious event that occurred on '2022-05-09'. I want to retrieve all login attempts that occurred on this day and the day before ('2022-05-08').
    
- **Why it matters:** By filtering the login attempts by date I can narrow down the list and cause of the suspicious event.

- **The SQL Query:** ```SELECT * 
FROM log_in_attempts 
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';```
  
- **How this works:** The <mark>login_date</mark> column in the <mark>log_in_attempts</mark> table contains information on the dates when login attempts were made. So, if I put '2022-05-09' and '2022-05-08' dates in the <mark>login_date</mark> using OR operator, I should get all the login attempts made in these 2 days. In this case which is 75 attempts in total. Its long so I've put the screenshot of the first few here. 

**In MariaDB Shell**

![Create table](sql-query-3.png "Login filtering by dates")


### 3. Retrive login attempts outside of a place (Mexico)
- **Goal:** There’s been suspicious activity with login attempts, but the team has determined that this activity didn't originate in Mexico. Now, I need to investigate login attempts that occurred outside of Mexico. I'll be using filters in SQL to create a query that identifies all login attempts that occurred outside of Mexico.
    
- **Why it matters:** BAs the team decided that the login attempts are from outside of Mexico. I should focus on narrowing down the list to the countries that are not Mexico. It saves my team time to investigate the situation.

- **The SQL Query:** ```SELECT * 
FROM log_in_attempts 
WHERE NOT country LIKE 'MEX%';```
  
- **How this works:** The <mark>country</mark> column in the <mark>log_in_attempts</mark> table contains information on the location of the login attempts. As I have to look for countries that are not mexico. I'm gonna use the <mark>NOT</mark> operator after <mark>WHERE</mark>. When referring to Mexico, the country column contains values of both <mark>MEX</mark> and <mark>MEXICO</mark>, and I need to use the <mark>LIKE</mark> keyword with <mark>%</mark> to make sure my query reflects this. Which is why I have used 'MEX%' after <mark>LIKE</mark> keyword to find the countries, I should get all the login attempts made outside of Mexico. In this case which is 144 attempts were made outside of Mexico. Its long list so I've put the screenshot of the first and last few here.

**In MariaDB Shell**

![Create table](sql-query-4.png "Login filtering by specific Location 1")
![Create table](sql-query-5.png "Login filtering by specific Location 2")
