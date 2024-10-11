# SQL-Based-Security-Investigation

# Project description
As a security Analyst at a medium sized financial institution. Part of my job is to investigate security issues to help keep the system secure. During routine systems review I discovered some potential security issues that involve login attempts and employee machines.So I was tasked to examine the organization’s data in their employees and log_in_attempts tables. SQL filters were used  to retrieve records from different datasets and investigate the potential security issues.


### Table formats
the tables used for this  activity is contained in the  organization database which includes the following two tables: 
Log_in_attempts           2. employees
log_in_attempts
The log_in_attempts table has the following columns:

event_id: The identification number assigned to each login event
username: The username of the employee
login_date: The date the login attempt was recorded
login_time: The time the login attempt was recorded
country: The country where the login attempt occurred
ip_address: The IP address of that employee’s machine
success: The success of the login attempt; FALSE indicates a failed attempt

In the MariaDB shell, these columns are returned as:
![Capture](https://github.com/user-attachments/assets/0a33419c-d444-469c-9fff-394cb0686e42)


### employees
The employees table has the following columns:
employee_id: The identification number assigned to each employee
device_id: The identification number assigned to each device used by the employee
username: The username of the employee
department: The department the employee is in
office: The office the employee is located in

In the MariaDB shell, these columns are returned as:
![Capture](https://github.com/user-attachments/assets/411ea653-3459-45ff-904c-95d4d7ed8ea0)


### Retrieve after hours failed login attempts
This was the first task carried out during the investigation and the goal here is to identify any failed login attempt that occurred after work hours which is ‘18:00’.
IT should be noted that the success column in the log_in_attempts table contains values of TRUE or FALSE to indicate whether the login was successful. MySQL stores Boolean values as 1 for TRUE, and 0 for FALSE. This means that TRUE is represented as 1, and FALSE represented as 0 in the success column.


![Capture](https://github.com/user-attachments/assets/ea91f759-e4e4-4011-94dc-295bb20ad622)



'SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = 0;

### Retrieve login attempts on specific dates
I also investigated a suspicious event that occurred on '2022-05-09'. The goal is to retrieve all login attempts that occurred on this day and the day before ('2022-05-08').

SELECT * 
FROM log_in_attempts 
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
![Capture](https://github.com/user-attachments/assets/bbf836f7-312f-4256-af14-8c2c56579923)




### Retrieve login attempts outside of Mexico
The  team also decided to  investigate logins that did not originate in Mexico, and I was tasked to find this information.  It was also noted that the country field includes entries with 'MEX' and 'MEXICO'. So I used the NOT and LIKE operators and the matching pattern 'MEX%'.

SELECT * 
FROM log_in_attempts
WHERE NOT  country LIKE 'MEX%';
![Capture](https://github.com/user-attachments/assets/4f77f537-3763-47df-bea3-0e521a1c7a7a)



### Retrieve employees in Marketing
I was also tasked with the task of  updating employee machines, and need to obtain the information about employees in the 'Marketing' department who are located in all offices in the East building (such as 'East-170' or 'East-320').

SELECT * 
FROM employees 
WHERE department = 'Marketing' AND office LIKE 'East-%';

![Capture](https://github.com/user-attachments/assets/833a3251-4ef5-45bb-8cae-bc6453a50c6c)


### Retrieve employees in Finance or Sales
Now, your team needs to perform a different update to the computers of all employees in the Finance or the Sales department, and need to locate information on these employees.  The query used was

SELECT * 
FROM employees 
WHERE department IN ('Finance', 'Sales');

![Capture](https://github.com/user-attachments/assets/3192682a-e6cd-4ad3-890e-023d885faa78)





### Retrieve all employees not in IT
Finally we needed to make one more update. This update was already made to employee computers in the Information Technology department. The team needs information about employees who are not in that department. the NOT operator to identify these employees.

SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
![Capture](https://github.com/user-attachments/assets/3e4fa046-d0d3-479f-af38-279ad6301712)




### Summary
 This project demonstrated the effective use of SQL queries and filters to enhance system security by identifying suspicious activities and managing employee devices across departments. I applied various SQL operators such as AND, OR, NOT, and LIKE to extract precise information and uncover patterns related to failed login attempts, unusual login activities, and employee device management. 


