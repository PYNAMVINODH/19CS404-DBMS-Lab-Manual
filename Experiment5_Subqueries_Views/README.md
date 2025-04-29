# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
-- 
From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

customer table

    name         type
    -----------  ----------
    customer_id  int
    cust_name    text
    city         text
    grade        int
    salesman_id  int
    For example:
    
    Result
    grade       COUNT(*)
    ----------  ----------
    300         2

```sql
-- 
SELECT grade, COUNT(*) 
FROM customer 
WHERE grade > (
    SELECT AVG(grade) 
    FROM customer 
    WHERE city = 'New York'
)
GROUP BY grade;

```

**Output:**

![image](https://github.com/user-attachments/assets/e79860f6-41a1-4271-af5e-25a2a59d219c)


**Question 2**
---
-- 
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

salesman table
    
    name                 type
    ---------------   ---------------
    salesman_id       numeric(5)
    name                  varchar(30)
    city                     varchar(15)
    commission       decimal(5,2)
    
    customer table
    
    name              type
    -----------       ----------
    customer_id   int
    cust_name     text
    city                text
    grade            int
    salesman_id  int
    
    For example:
    
    Result
    salesman_id  name
    -----------  ----------
    5001         James Hoog
    5002         Nail Knite

```sql
-- 
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(*) > 1;

```

**Output:**

![image](https://github.com/user-attachments/assets/6181fd89-626f-4dad-97a9-9d70a346d905)


**Question 3**
---
-- 
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE
    
    name            type
    ----------     ----------
    ord_no          int
    purch_amt    real
    ord_date       text
    customer_id  int
    salesman_id  int
    
    For example:
    
    Result
    ord_no      purch_amt   ord_date    customer_id  salesman_id
    ----------  ----------  ----------  -----------  -----------
    70005       2400.6      2012-07-27  3007         5001
    70008       5760.0      2012-09-10  3002         5001
    70003       2480.4      2012-10-10  3009         5003
    70013       3045.6      2012-04-25  3002         5001


```sql
-- 
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE purch_amt > (
    SELECT AVG(purch_amt)
    FROM orders
    WHERE ord_date = '2012-10-10'
);


```

**Output:**

![image](https://github.com/user-attachments/assets/cd897e68-306d-4af0-a743-cad588d551df)


**Question 4**
---
-- 
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

Sample table: CUSTOMERS
    
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    
    1          Ramesh     32              Ahmedabad     2000
    2          Khilan        25              Delhi                 1500
    3          Kaushik      23              Kota                  2000
    4          Chaitali       25             Mumbai            6500
    5          Hardik        27              Bhopal              8500
    6          Komal         22              Hyderabad       4500
    
    7           Muffy          24              Indore            10000
    
     
     
    
    For example:
    
    Result
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    2           Khilan      25          Delhi       1500

```sql
-- 
SELECT * 
FROM CUSTOMERS
WHERE TRIM(UPPER(ADDRESS)) = 'DELHI'
  AND AGE < 30
ORDER BY ID ASC;

```

**Output:**

![image](https://github.com/user-attachments/assets/3e53d1cc-d23c-49e4-8159-7f6da82ab00f)


**Question 5**
---
-- 

Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

Sample table: CUSTOMERS
    
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    
    1          Ramesh     32              Ahmedabad     2000
    2          Khilan        25              Delhi                 1500
    3          Kaushik      23              Kota                  2000
    4          Chaitali       25             Mumbai            6500
    5          Hardik        27              Bhopal              8500
    6          Komal         22              Hyderabad       4500
    
    7           Muffy          24              Indore            10000
    
     
     
    
    For example:
    
    Result
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    1           Ramesh      32          Ahmedabad   2000
    3           Kaushik     23          Kota        2000
    4           Chaitali    25          Mumbai      6500
    5           Hardik      27          Bhopal      8500
    6           Komal       22          Hyderabad   4500
    7           Muffy       24          Indore      10000
```sql
-- 
SELECT * 
FROM CUSTOMERS 
WHERE SALARY > 1500;

```

**Output:**

![image](https://github.com/user-attachments/assets/659470b2-b99e-431f-9def-ae45afe34a1b)


**Question 6**
---
-- 
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

![image](https://github.com/user-attachments/assets/be111da2-2a21-4e9d-8a7e-f510c8670ddc)


    
    For example:
    
    Result
    student_id       student_name     subject          grade
    ---------------  ---------------  ---------------  ---------------
    2                Bob              Math             85
    6                Frank            Science          85
    7                John             Social           85

```sql
-- 
SELECT * 
FROM GRADES g
WHERE grade = (
    SELECT MIN(grade)
    FROM GRADES
    WHERE subject = g.subject
);

```

**Output:**

![image](https://github.com/user-attachments/assets/1c21bd7c-5606-423b-8d8e-635156029a88)


**Question 7**
---
--  7QUE
 

```sql
-- Paste your SQL code below for Question 7
```

**Output:**

![Output7](output.png)

**Question 8**
---
-- 
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

salesman table
    
    name             type
    ---------------  ---------------
    salesman_id      numeric(5)
    name                 varchar(30)
    city                    varchar(15)
    commission       decimal(5,2)
    
    customer table
    
    name         type
    -----------  ----------
    customer_id  int
    cust_name    text
    city         text
    grade        int
    salesman_id  int
     
    
    For example:
    
    Result
    customer_id  cust_name    city        grade       salesman_id
    -----------  -----------  ----------  ----------  -----------
    3005         Graham Zusi  California  200         5002
```sql
--
SELECT c.customer_id, c.cust_name, c.city, c.grade, c.salesman_id
FROM customer c
WHERE c.customer_id = (
    SELECT s.salesman_id - 2001
    FROM salesman s
    WHERE s.name = 'Mc Lyon'
);

```

**Output:**

![image](https://github.com/user-attachments/assets/ee3293bf-9718-4c79-86c9-c9bf800e402b)


**Question 9**
---
-- 9QUE
```sql
-- Paste your SQL code below for Question 9
```

**Output:**

![Output9](output.png)

**Question 10**
---
-- 
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

Sample table: CUSTOMERS
    
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    
    1          Ramesh     32              Ahmedabad     2000
    2          Khilan        25              Delhi                 1500
    3          Kaushik      23              Kota                  2000
    4          Chaitali       25             Mumbai            6500
    5          Hardik        27              Bhopal              8500
    6          Komal         22              Hyderabad       4500
    
    7           Muffy          24              Indore            10000
    
     
     
    
    For example:
    
    Result
    ID          NAME        AGE         ADDRESS     SALARY
    ----------  ----------  ----------  ----------  ----------
    4           Chaitali    25          Mumbai      6500
    5           Hardik      27          Bhopal      8500
    7           Muffy       24          Indore      10000
```sql
-- 
SELECT * 
FROM CUSTOMERS 
WHERE SALARY > 4500;

```

**Output:**

![image](https://github.com/user-attachments/assets/bc7788f9-0a4f-41f5-af09-3b70bc7f88da)


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
