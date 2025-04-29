# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
-- Create a table named Attendance with the following constraints:

    AttendanceID as INTEGER should be the primary key.
    
    EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
    
    AttendanceDate as DATE.
    
    Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
  CREATE TABLE Attendance (AttendanceID INTEGER PRIMARY KEY, EmployeeID INTEGER , AttendanceDate DATE, Status TEXT CHECK(Status IN('Present','Absent','Leave')), FOREIGN KEY (EmployeeID) 
  REFERENCES Employees(EmployeeID));
```

**Output:**

![image](https://github.com/user-attachments/assets/f7c3a46c-8141-452f-b2d9-e52460b3daaa)


**Question 2**
---
--Create a table named Events with the following columns:

    EventID as INTEGER
    
    EventName as TEXT
    
    EventDate as DATE


```sql
  --CREATE TABLE Events (
      EventID INTEGER,
      EventName TEXT,
      EventDate DATE
  );
```

**Output:**

![image](https://github.com/user-attachments/assets/8065c8a5-d9f9-47e5-8584-98b8150c3ef6)


**Question 3**
---
-- Insert all customers from Old_customers into Customers


    Table attributes are CustomerID, Name, Address, Email

```sql
-- INSERT INTO Customers (CustomerID, Name, Address, Email)
   SELECT CustomerID, Name, Address, Email FROM Old_customers;
```

**Output:**

![image](https://github.com/user-attachments/assets/3a66a53a-cfd2-4b73-8fa6-2d3e834d168e)


**Question 4**
---
-- Create a new table named item with the following specifications and constraints:

    item_id as TEXT and as primary key.
    
    item_desc as TEXT.
    
    rate as INTEGER.
    
    icom_id as TEXT with a length of 4.
    
    icom_id is a foreign key referencing com_id in the company table.
    
    The foreign key should set NULL on updates and deletes.
    
    item_desc and rate should not accept NULL.
 ```sql
-- CREATE TABLE item(
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT CHECK(LENGTH(icom_id) = 4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
     ON UPDATE SET NULL
     ON DELETE SET NULL
);
```

**Output:**

![image](https://github.com/user-attachments/assets/2a71ea3b-17d3-4e06-9358-9e463519f73c)


**Question 5**
---
-- Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.



```sql
-- ALTER TABLE employee ADD department_id INTEGER;
ALTER TABLE employee ADD manager_id INTEGER DEFAULT NULL;
```

**Output:**

![image](https://github.com/user-attachments/assets/9ea20553-6c23-447e-9ed5-457658353634)


**Question 6**
---
-- Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo        Name             Gender      
----------    ------------     ----------  
204           Samuel Black        M          

Note: The Subject and MARKS columns will use their default values.

```sql
-- INSERT INTO Student_details(RollNo,Name,Gender)
VALUES (204,'Samuel Black', 'M');
```

**Output:**

![image](https://github.com/user-attachments/assets/d20d30f9-57a2-48c4-9c8c-bb1d7c741cac)


**Question 7**
---
-- Create a table named Department with the following constraints:

    DepartmentID as INTEGER should be the primary key.
    
    DepartmentName as TEXT should be unique and not NULL.
    
    Location as TEXT.

```sql
-- CREATE TABLE Department(
    DepartmentID INTEGER PRIMARY KEY,
    DepartmentName TEXT UNIQUE NOT NULL,
    Location TEXT
);
```

**Output:**

![image](https://github.com/user-attachments/assets/7d5bdedb-9c46-46bb-b70e-f4df9711ec6d)


**Question 8**
---
-- Paste Question 8 here

```sql
-- Paste your SQL code below for Question 8
```

**Output:**

![Output8](output.png)

**Question 9**
---
-- Create a table named Invoices with the following constraints:

    InvoiceID as INTEGER should be the primary key.
    
    InvoiceDate as DATE.
    
    Amount as REAL should be greater than 0.
    
    DueDate as DATE should be greater than the InvoiceDate.
    
    OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
-- CREATE TABLE Invoices(
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    Amount REAL CHECK((Amount) > 0),
    DueDate DATE CHECK((DueDate)>(InvoiceDate)),
    OrderID INTEGER ,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/078ddecd-3f63-4e80-95cf-c38afac44ca8)


**Question 10**
---
-- Paste Question 10 here

```sql
-- Paste your SQL code below for Question 10
```

**Output:**

![Output10](output.png)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
