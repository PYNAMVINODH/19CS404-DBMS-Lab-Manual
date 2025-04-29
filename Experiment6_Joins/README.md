# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
-- 
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'London'.

Customer Table:

![image](https://github.com/user-attachments/assets/0c4b236f-e957-4100-9892-fb0d5800b360)


Salesmen Table:

![image](https://github.com/user-attachments/assets/7e8abcae-5622-4bb6-9162-2f1821825bde)


 

    For example:
    
    Result
    name
    ---------------
    Pit Alex
    Nail Knite


```sql
--
 SELECT DISTINCT s.name
FROM salesman AS s
LEFT JOIN customer AS c
  ON s.salesman_id = c.salesman_id
WHERE c.city = 'London';
```

**Output:**

![image](https://github.com/user-attachments/assets/525a8233-965e-469b-bfe1-cb6cdd047550)


**Question 2**
---
--
 From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

Sample table: customer

     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table: salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12
    For example:
    
    Result
    Customer Name    city             Salesman         commission
    ---------------  ---------------  ---------------  ---------------
    Nick Rimando     Chennai          Bob Emily        0.15
    Graham Zusi      California       Nail Knite       0.13
    Brad Guzan       London           Pit Alex         0.11
    Fabian Johns     Paris            Mc Lyon          0.14
    Brad Davis       New York         Bob Emily        0.15
    Geoff Cameron    Berlin           Lauson Hen       0.12
    Julian Green     London           Nail Knite       0.13
    Jozy Altidore    Moscow           Paul Adam        0.13

```sql
-- 
SELECT
  c.cust_name     AS "Customer Name",
  c.city          AS city,
  s.name          AS Salesman,
  s.commission    AS commission
FROM customer AS c
JOIN salesman AS s
  ON c.salesman_id = s.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/a2f035be-4ef5-4eeb-9348-7366f2539918)


**Question 3**
---
--
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman

     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005

```sql
-- 
SELECT
  s.name    AS Salesman,
  c.cust_name,
  s.city
FROM salesman AS s
JOIN customer AS c
  ON s.city = c.city;
```

**Output:**

![image](https://github.com/user-attachments/assets/dee759ae-1daf-455f-b6f6-476044b2ac59)


**Question 4**
---
--
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

Sample table: orders

    ord_no      purch_amt   ord_date    customer_id  salesman_id
    ----------  ----------  ----------  -----------  -----------
    70001       150.5       2012-10-05  3005         5002
    70009       270.65      2012-09-10  3001         5005
    70002       65.26       2012-10-05  3002         5001
    70004       110.5       2012-08-17  3009         5003
    70007       948.5       2012-09-10  3005         5002
    70005       2400.6      2012-07-27  3007         5001
    70008       5760        2012-09-10  3002         5001
    70010       1983.43     2012-10-10  3004         5006
    70003       2480.4      2012-10-10  3009         5003
    70012       250.45      2012-06-27  3008         5002
    70011       75.29       2012-08-17  3003         5007
    70013       3045.6      2012-04-25  3002         5001
    Sample table: customer
    
     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table: salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12

```sql
--
SELECT
  o.ord_no,
  o.ord_date,
  o.purch_amt,
  c.cust_name   AS "Customer Name",
  c.grade,
  s.name        AS Salesman,
  s.commission
FROM orders AS o
JOIN customer AS c
  ON o.customer_id = c.customer_id
JOIN salesman AS s
  ON o.salesman_id = s.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/ebbe2a76-2f70-4928-a5ac-f4b2f7e8a2e8)
![image](https://github.com/user-attachments/assets/efaae05d-d90d-4811-805c-277a702ded2d)



**Question 5**
---
-- 
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: customer

     customer_id |   cust_name    |    city    | grade | salesman_id 
    -------------+----------------+------------+-------+-------------
            3002 | Nick Rimando   | New York   |   100 |        5001
            3007 | Brad Davis     | New York   |   200 |        5001
            3005 | Graham Zusi    | California |   200 |        5002
            3008 | Julian Green   | London     |   300 |        5002
            3004 | Fabian Johnson | Paris      |   300 |        5006
            3009 | Geoff Cameron  | Berlin     |   100 |        5003
            3003 | Jozy Altidor   | Moscow     |   200 |        5007
            3001 | Brad Guzan     | London     |       |        5005
    Sample table : salesman
    
     salesman_id |    name    |   city   | commission 
    -------------+------------+----------+------------
            5001 | James Hoog | New York |       0.15
            5002 | Nail Knite | Paris    |       0.13
            5005 | Pit Alex   | London   |       0.11
            5006 | Mc Lyon    | Paris    |       0.14
            5007 | Paul Adam  | Rome     |       0.13
            5003 | Lauson Hen | San Jose |       0.12
    For example:
    
    Result
    ord_no           purch_amt        ord_date         cust_name        customer_city  grade       salesman_name  salesman_city  commission
    ---------------  ---------------  ---------------  ---------------  -------------  ----------  -------------  -------------  ----------
    70001            150.5            2012-10-05       Graham Zusi      California     200         Nail Knite     Paris          0.13
    70009            270.65           2012-09-10       Brad Guzan       London         100         Pit Alex       London         0.11
    70002            65.26            2012-10-05       Nick Rimando     Chennai        100         Bob Emily      New York       0.15
    70004            110.5            2012-08-17       Geoff Cameron    Berlin         100         Lauson Hen     San Jose       0.12
    70007            948.5            2012-09-10       Graham Zusi      California     200         Nail Knite     Paris          0.13
    70005            2400.6           2012-07-27       Brad Davis       New York       200         Bob Emily      New York       0.15
    70008            5760.0           2012-09-10       Nick Rimando     Chennai        100         Bob Emily      New York       0.15
    70010            1983.43          2012-10-10       Fabian Johns     Paris          300         Mc Lyon        Paris          0.14
    70003            2480.4           2012-10-10       Geoff Cameron    Berlin         100         Lauson Hen     San Jose       0.12
    70012            250.45           2012-06-27       Julian Green     London         300         Nail Knite     Paris          0.13
    70011            75.29            2012-08-17       Jozy Altidore    Moscow         200         Paul Adam      Rome           0.13
    70013            3045.6           2012-04-25       Nick Rimando     Chennai        100         Bob Emily      New York       0.15


```sql
-- 
SELECT
  o.ord_no,
  o.purch_amt,
  o.ord_date,
  c.cust_name        AS cust_name,
  c.city             AS customer_city,
  c.grade,
  s.name             AS salesman_name,
  s.city             AS salesman_city,
  s.commission
FROM orders AS o
JOIN customer AS c
  ON o.customer_id = c.customer_id
JOIN salesman AS s
  ON o.salesman_id = s.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/27ea9666-5d02-4d4e-b167-8df974af2f64)
![image](https://github.com/user-attachments/assets/75769073-9ac7-46a8-8073-dc3477d31b0d)



**Question 6**
---
--
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for customers with a grade less than or equal to 100.

Customer Table:

![image](https://github.com/user-attachments/assets/f038a02e-7af7-48ad-ba2e-a49f57aacd10)


Salesmen Table:


![image](https://github.com/user-attachments/assets/ebb5c932-e89d-4dc2-81ed-be1cb1a2db86)

 

    For example:
    
    Result
    name             cust_name        city             grade            salesman_id
    ---------------  ---------------  ---------------  ---------------  -----------
    Bob Emily        Nick Rimando     Chennai          100              5001
    Pit Alex         Brad Guzan       London           100              5005
    Lauson Hen       Geoff Cameron    Berlin           100              5003

```sql
-- 
SELECT
  s.name,
  c.cust_name,
  c.city,
  c.grade,
  c.salesman_id
FROM salesman AS s
LEFT JOIN customer AS c
  ON s.salesman_id = c.salesman_id
WHERE c.grade <= 100;
```

**Output:**

![image](https://github.com/user-attachments/assets/8fde73ed-987e-4c49-b50e-4bbe5bcee0de)


**Question 7**
---
-- 7 que
 

```sql
-- Paste your SQL code below for Question 7
```

**Output:**

![Output7](output.png)

**Question 8**
---
-- 
Write the SQL query that accomplishes the selection of all columns from the "patients" table and the first name of doctors from the "doctors" table, with an inner join on the "doctor_id" column.

PATIENTS TABLE:
    name             type
    ---------------  ---------------
    patient_id       INT
    first_name       VARCHAR(50)
    last_name        VARCHAR(50)
    date_of_birth    DATE
    admission_date   DATE
    discharge_date   DATE
    doctor_id        INT
    
    DOCTORS TABLE:
    
    name             type
    ---------------  ---------------
    doctor_id        INT
    first_name       VARCHAR(50)
    last_name        VARCHAR(50)
    specialization   VARCHAR(100)
    
    For example:
    
    Result
    patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id   doctor_name
    ---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------  -----------
    1                Alice            Williams         1980-05-12       2024-01-10                      1           John
    2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01      2           Emily
    3                Charlie          Davis            1972-11-30       2024-03-10                      3           Michael


```sql
-- 
SELECT 
  p.patient_id, 
  p.first_name, 
  p.last_name, 
  p.date_of_birth, 
  p.admission_date, 
  p.discharge_date, 
  p.doctor_id, 
  d.first_name AS doctor_name
FROM 
  patients AS p
INNER JOIN 
  doctors AS d
  ON p.doctor_id = d.doctor_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/23a17581-f2bf-41f5-9e50-7b5619ac3e8d)


**Question 9**
---
-- 
Write the SQL query that accomplishes the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a non-null discharge date.

PATIENTS TABLE:
    name             type
    ---------------  ---------------
    patient_id       INT
    first_name       VARCHAR(50)
    last_name        VARCHAR(50)
    date_of_birth    DATE
    admission_date   DATE
    discharge_date   DATE
    doctor_id        INT
    
    DOCTORS TABLE:
    
    name             type
    ---------------  ---------------
    doctor_id        INT
    first_name       VARCHAR(50)
    last_name        VARCHAR(50)
    specialization   VARCHAR(100)
    
    For example:
    
    Result
    patient_name     doctor_name
    ---------------  ---------------
    Bob              Emily


```sql
-- 
SELECT 
  p.first_name AS patient_name,
  d.first_name AS doctor_name
FROM 
  patients AS p
INNER JOIN 
  doctors AS d
  ON p.doctor_id = d.doctor_id
WHERE 
  p.discharge_date IS NOT NULL;
```

**Output:**

![image](https://github.com/user-attachments/assets/b23ed10f-a00d-47a5-8daf-437ea52f0553)


**Question 10**
---
-- Paste Question 10 here

```sql
-- Paste your SQL code below for Question 10
```

**Output:**

![Output10](output.png)


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
