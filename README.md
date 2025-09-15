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

