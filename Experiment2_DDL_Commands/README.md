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
-- ![image](https://github.com/user-attachments/assets/a6b8b2ca-0327-4f4d-b87c-4a6da1dca18a)


```sql
-- create table Department(DepartmentID INTEGER primary key,DepartmentName TEXT UNIQUE not null,Location TEXT);
```

**Output:**
![image](https://github.com/user-attachments/assets/eb80e91c-7160-4af5-8e14-86799d4b0611)


**Question 2**
---
-- ![image](https://github.com/user-attachments/assets/083ba578-c023-47c0-96ba-af7dd2eb6d94)


```sql
-- create table Shipments(ShipmentID INTEGER primary key,ShipmentDate DATE,SupplierID INTEGER,OrderID INTEGER,foreign key(SupplierID)references Suppliers(SupplierID),foreign key(OrderID)references Orders(OrderID));
```

**Output:**

![image](https://github.com/user-attachments/assets/765c33a0-47f7-4aa3-a737-723fc218d879)


**Question 3**
---
-- ![image](https://github.com/user-attachments/assets/d0a0f908-e16a-4842-972e-26755287002f)


```sql
-- insert into Customers select*from Old_customers;
```

**Output:**

![image](https://github.com/user-attachments/assets/0d0305b1-fd05-4292-b443-769c99b915a6)


**Question 4**
---
-- ![image](https://github.com/user-attachments/assets/e93f7652-de1a-4afc-b5da-7e69ac75abb5)


```sql
-- insert into Customers(CustomerID,Name,Address) values(306,'Diana Prince','Themyscira');
insert into Customers(CustomerID,Name,Address,City,Zipcode) values (307,'Bruce Wayne','Wayne Mano','Gotham',10007);
insert into Customers(CustomerID,Name,Address,Zipcode)values(308,'Peter Parker','Queens',11375);
```

**Output:**

![image](https://github.com/user-attachments/assets/4a808f3e-af48-4a24-ab75-6c6e9e6845dc)


**Question 5**
---
-- ![image](https://github.com/user-attachments/assets/a9a4ddb5-d05e-4b98-8b18-cfa73d7a12f1)


```sql
-- insert into Employee(EmployeeID,Name,Position,Department,Salary) values(001,'Sarah Parker','Manager','HR',60000);
```

**Output:**

![image](https://github.com/user-attachments/assets/9b79570c-d883-4b84-ae19-798195f9ae0f)


**Question 6**
---
--![image](https://github.com/user-attachments/assets/dd5c1a42-dd7f-45c1-8a18-484305f9c41c)


```sql
-- alter table employee add department_id INTEGER;
alter table employee add manager_id INTEGER default NULL;
```

**Output:**

![image](https://github.com/user-attachments/assets/66799351-47af-46c7-ac5d-95d5f3c1db92)

**Question 7**
---
-- ![image](https://github.com/user-attachments/assets/585aabdf-13da-4f75-8c15-6824177805b5)

```sql
-- create table Tasks(TaskID INTEGER,TaskName TEXT,DueDate DATE);
```

**Output:**

![image](https://github.com/user-attachments/assets/eb8c6643-a435-4fb1-8225-84a1467d4ada)

**Question 8**
---
-- ![image](https://github.com/user-attachments/assets/c0217d70-886b-468a-a34b-4ccd529d1f24)

```sql
-- create table jobs(job_id INTEGER,job_title TEXT default '',min_salary INTEGER default '8000',max_salary INTEGER default NULL);
```

**Output:**

![image](https://github.com/user-attachments/assets/656a4be0-02b7-4340-aded-f4c68057a54e)

**Question 9**
---
-- ![image](https://github.com/user-attachments/assets/3109e51f-d9ec-4619-9a67-582b28daa600)


```sql
-- alter table employee add designation varchar(50);
```

**Output:**

![image](https://github.com/user-attachments/assets/fff871af-57ad-45b3-bbd5-a5cbd34bac94)


**Question 10**
---
-- ![image](https://github.com/user-attachments/assets/cc6af063-b3be-4be3-807c-c03d9edbb85f)


```sql
-- create table Invoices(InvoiceID INTEGER primary key,InvoiceDate date,Amount real,DueDate date,OrderID INTEGER,check(Amount>0),check(DueDate>InvoiceDate),foreign key(OrderID)references Orders(OrderID));
```

**Output:**

![image](https://github.com/user-attachments/assets/a7e2d0dd-6990-4788-b081-b9359cc03623)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
