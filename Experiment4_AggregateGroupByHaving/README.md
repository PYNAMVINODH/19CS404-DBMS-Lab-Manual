# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
-- 
Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table

![image](https://github.com/user-attachments/assets/6a6d0203-c203-4a57-b668-dc4927d6e484)
    
    For example:
    
    Result
    PatientID   AvgMedications
    ----------  --------------
    4           5
    6           1
    7           1
    8           3


```sql
--
SELECT PatientID, COUNT(*) AS AvgMedications
FROM MedicalRecords
GROUP BY PatientID;

```

**Output:**

![image](https://github.com/user-attachments/assets/ebb90cc1-67d2-4bda-ad32-68d6e06f23d5)


**Question 2**
---
--
What is the most common diagnosis among patients?

Sample table:MedicalRecords Table

![image](https://github.com/user-attachments/assets/a9e4e689-12df-430c-a2e3-a54842a3a6d8)


    For example:
    
    Result
    Diagnosis              DiagnosisCount
    ---------------------  --------------
    Childhood vaccination  3


```sql
--
SELECT
    Diagnosis,
    COUNT(*) AS DiagnosisCount
FROM 
    MedicalRecords
GROUP BY 
    Diagnosis
ORDER BY
    DiagnosisCount DESC
LIMIT 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/8888a2be-04cd-4e78-bf9e-54269e11dad6)


**Question 3**
---
--![Screenshot 2025-04-29 131558](https://github.com/user-attachments/assets/d054f243-ab5a-49e1-bdd9-071c29ff5199)


```sql
-- select avg(length(email)) as avg_email_length
from customer
order by length(email)
limit 1;
```

**Output:**
![Screenshot 2025-04-29 131605](https://github.com/user-attachments/assets/c279b3db-a9e8-4dcf-b38a-cd467996b4f9)
**Question 4**
---
-- 
Write a SQL query to find  how many employees work in California?

Table: employee

    name        type
    ----------  ----------
    id          INTEGER
    name        TEXT
    age         INTEGER
    city        TEXT
    income      INTEGER
 

    For example:
    
    Result
    employees_in_california
    -----------------------
    2


```sql
-- 
SELECT COUNT(*) AS employees_in_california
FROM employee
WHERE city = 'California';

```

**Output:**

![image](https://github.com/user-attachments/assets/8539494b-fd23-4b03-881a-a005ac092f9e)


**Question 5**
---
-- 
Write a SQL query to find the total number of unique cities in the customer table?

Table: customer

    name        type
    ----------  ----------
    id          INTEGER
    name        TEXT
    city        TEXT
    email       TEXT
    phone       INTEGER
    For example:
    
    Result
    unique_cities
    -------------
    10


```sql
-- 
SELECT COUNT(DISTINCT city) AS unique_cities
FROM customer;


```

**Output:**

![image](https://github.com/user-attachments/assets/9d5a3ec2-a257-4b6c-802c-21a082307661)


**Question 6**
---
-- 
Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city

Table: customer

    name        type
    ----------  ----------
    id          INTEGER
    name        TEXT   
    city        TEXT
    email       TEXT
    phone       INTEGER
    For example:
    
    Result
    avg_email_length_below_30
    -------------------------
    14.0


```sql
--
SELECT AVG(LENGTH(email)) AS avg_email_length_below_30
FROM customer
WHERE city = 'Mumbai';

```

**Output:**

![image](https://github.com/user-attachments/assets/ebe68ef7-1f1e-4554-873e-6c712a797cd1)


**Question 7**
---
--
Write a SQL query to  find the average salary of all employees?

Table: employee

    name        type
    ----------  ----------
    id          INTEGER
    name        TEXT
    age         INTEGER
    city        TEXT
    income      INTEGER
     
    
    For example:
    
    Result
    Average_Salary
    --------------
    1568750.0

```sql
-- 
SELECT AVG(income) AS Average_Salary
FROM employee;

```

**Output:**

![image](https://github.com/user-attachments/assets/a89b3da5-e3be-4110-9f8a-2ac7e174e61f)


**Question 8**
---
--
Write the SQL query that accomplishes the selection of average price for each category from the "products" table and includes only those products where the average price falls between 10 and 15.

Sample table: products

![image](https://github.com/user-attachments/assets/05c5adce-efb4-4643-83e1-694af481d7df)



    For example:
    
    Result
    category_id  AVG(Price)
    -----------  ----------
    1            12.375


```sql
-- 
SELECT category_id, AVG(price) AS "AVG(Price)"
FROM products
GROUP BY category_id
HAVING AVG(price) BETWEEN 10 AND 15;

```

**Output:**

![image](https://github.com/user-attachments/assets/55d3960f-ede8-4f67-9a65-8675a24b9b0d)


**Question 9**
---
--
Write the SQL query that accomplishes the grouping of data by age, calculates the maximum income for each age group, and includes only those age groups where the maximum income is greater than 2,000,000.

Sample table: employee

![image](https://github.com/user-attachments/assets/b79821cf-f64e-45ce-9115-22ff3b53f92f)


    For example:
    
    Result
    age         MAX(income)
    ----------  -----------
    35          5000000


```sql
--
SELECT age, MAX(income) AS "MAX(income)"
FROM employee
GROUP BY age
HAVING MAX(income) > 2000000;

```

**Output:**

![image](https://github.com/user-attachments/assets/74cd2970-e386-4aa6-b7a6-cc01d5cb9a06)


**Question 10**
---
-- 
Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

Sample table: customer1

![image](https://github.com/user-attachments/assets/541eeaa3-85ac-4319-ae0f-b744deb489cc)



    For example:
    
    Result
    address     AVG(salary)
    ----------  -----------
    Bhopal      8500.0
    Indore      10000.0
    Mumbai      6500.0


```sql
-- 
SELECT address, AVG(salary) AS "AVG(salary)"
FROM customer1
GROUP BY address
HAVING AVG(salary) > 5000;

```

**Output:**

![image](https://github.com/user-attachments/assets/30d4504d-cb2b-4316-87f5-4baad5e018a1)



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
