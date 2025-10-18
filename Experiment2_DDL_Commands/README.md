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
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

| **Test**                                                                                                                                                                                                                                              | **Result**                                                              |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `sql<br>INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES (1, 'Alice', 'Johnson', 'alice.johnson@example.com');<br>INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);<br>SELECT * FROM Orders;<br>` | **OrderID    OrderDate    CustomerID**<br>1          2024-08-01       1 |


```
CREATE TABLE Orders(
OrderID  INTEGER PRIMARY KEY,
OrderDate  DATE NOT NULL,
CustomerID INTEGER,
FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

```

**Output:**

<img width="1177" height="272" alt="image" src="https://github.com/user-attachments/assets/646fb90b-a512-42d2-b0c9-6fe581fe8965" />


**Question 2**
---
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

| **Test**                  | **Result**                                                                                                                                                                                                           |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `SELECT * FROM Products;` | **ProductID    Name           Category    Price     Stock**<br>106       Fitness Tracker   Wearables<br>107       Laptop           Electronic    999.99     50<br>108       Wireless Earbud    Accessorie        100 |


```
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES('106','Fitness Tracker','Wearables',NULL,NULL);

INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES('107','Laptop','Electronic',999.99,50);

INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES('108','Wireless Earbud','Accessories',NULL,100);
```

**Output:**
<img width="1191" height="352" alt="image" src="https://github.com/user-attachments/assets/189d0bbc-6fa1-42c3-ab2e-3b123281adcf" />



**Question 3**
---
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.

| **Test**                                                                                               | **Result**                                              |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------- |
| `sql<br>INSERT INTO Invoices (InvoiceID, InvoiceDate)<br>VALUES (1, '2024-08-08'), (1, '2024-09-08');` | **Error:** UNIQUE constraint failed: Invoices.InvoiceID |


```
create table Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
DueDate  DATE CHECK(DueDate > InvoiceDate),
Amount REAL CHECK(Amount > 0)
);
```

**Output:**
<img width="1197" height="358" alt="image" src="https://github.com/user-attachments/assets/07c13217-fba6-4803-a642-c9e0df57722f" />


**Question 4**
---
Write a SQL query to Add a new column mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0

| **Test**                                | **Result**                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `pragma table_info('Student_details');` | **cid      name        type        notnull    dflt_value    pk**<br>0       RollNo        int         0                      1<br>1       Name          VARCHAR(10)     1                    0<br>2       Gender        TEXT        1                    0<br>3       Subject       VARCHAR(30     0                    0<br>4       MARKS        INT (3)        0                    0<br>5       mobilenumb    number        0                    0 |


```
ALTER TABLE Student_details ADD COLUMN mobilenumber  number;
```

**Output:**
<img width="1191" height="423" alt="image" src="https://github.com/user-attachments/assets/03b7dd69-d32a-429d-9044-5512662ae538" />


**Question 5**
---
Insert the following employees into the Employee table:

EmployeeID  Name        Position    Department  Salary
----------  ----------  ----------  ----------  ----------
2           John Smith  Developer   IT          75000
3           Anna Bell   Designer    Marketing   68000

| **Test**                  | **Result**                                                                                                                                                                          |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `SELECT * FROM Employee;` | **EmployeeID   Name        Position      Department    Salary**<br>2        John Smith   Developer     IT          75000<br>3        Anna Bell     Designer       Marketing   68000 |


```
INSERT INTO Employee(EmployeeID,Name,Position,Department,Salary)
VALUES(2,'John Smith','Developer','IT',75000);

INSERT INTO Employee(EmployeeID,Name,Position,Department,Salary)
VALUES(3,'Anna Bell','Designer','Marketing',68000);
```

**Output:**
<img width="1190" height="417" alt="image" src="https://github.com/user-attachments/assets/3d7b0b68-aa62-47ee-b246-c596fac146a0" />


**Question 6**
---
Create a table named Products with the following columns:

ProductID as INTEGER
ProductName as TEXT
Price as REAL
Stock as INTEGER

| **Test**                         | **Result**                                                                                                                                                                                                                                                                                                       |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `pragma table_info('Products');` | **cid    name        type        notnull    dflt_value    pk**<br>0     ProductID        INTEGER        0                0<br>1     ProductNam       TEXT            0                0<br>2     Price            REAL            0                0<br>3     Stock            INTEGER        0                0 |


```
CREATE TABLE Products(
ProductID INTEGER,
ProductName TEXT,
Price REAL,
Stock INTEGER);
```

**Output:**
<img width="1189" height="360" alt="image" src="https://github.com/user-attachments/assets/420d665d-b861-4aaf-beb2-bf721a184567" />


**Question 7**
---
Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'

 | **Test**                                                                                                                                                                      | **Result**                                                                                                                    |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `sql<br>INSERT INTO Student_details (RollNo, Name, Gender, Subject, email)<br>VALUES (1, 'John Doe', 'M', 'Math', 'john@example.com');<br><br>SELECT * FROM Student_details;` | **RollN   Name   Gen   Subject      email**<br>1       John     M     Math        [john@example.com](mailto:john@example.com) |


```
ALTER TABLE Student_details ADD COLUMN email TEXT NOT NULL DEFAULT 'Invalid';
```

**Output:**
<img width="1179" height="302" alt="image" src="https://github.com/user-attachments/assets/6ef18f02-3248-49b7-a8ad-88ac41d58165" />


**Question 8**
---
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

| **Test**                                          | **Result**                                                                                                                            |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `SELECT * FROM Customers WHERE CustomerID = 301;` | **CustomerID   Name            Address        City         ZipCode**<br>301        Michael Jordan   123 Maple St   Chicago      60616 |

```
INSERT INTO Customers(CustomerID,Name,Address,City,Zipcode)
VALUES(301,'Michael Jordan','123 Maple St','Chicago',60616);
```

**Output:**
<img width="1181" height="304" alt="image" src="https://github.com/user-attachments/assets/7a3c3ee7-d6f8-4f27-8bef-1d5a2d078b80" />


**Question 9**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

| **Test**                                                                                                                                                                                                                                          | **Result**                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `sql<br>INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);<br>INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);<br>SELECT * FROM Invoices;` | **InvoiceID   InvoiceDate   Amount   DueDate   OrderID**<br>1        2024-08-01   100.0   2024-09-01   1 |


```
CREATE TABLE Invoices(
InvoiceID INTEGER PRIMART KEY,
InvoiceDate DATE,
Amount Real check(Amount > 0),
DueDate DATE check(DueDate > InvoiceDate),
OrderID INTEGER,
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID));
```

**Output:**
<img width="1187" height="353" alt="image" src="https://github.com/user-attachments/assets/53018eea-cd42-412c-9da7-fb5ce2e312ee" />


**Question 10**
---
Create a new table named orders with the following specifications:
ord_id as TEXT with a length of 4.
item_id as TEXT.
ord_date as DATE.
ord_qty as INTEGER.
cost as INTEGER.
The primary key is a composite key consisting of item_id and ord_date.
ord_id and item_id should not accept NULL

| **Test**                                                                                                                                        | **Result**                                                                                    |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `sql<br>INSERT INTO orders (ord_id, item_id, ord_date, ord_qty, cost) VALUES ('O001', 'I001', '2023-08-01', 10, 100);<br>SELECT * FROM orders;` | **ord_id   item_id   ord_date   ord_qty   cost**<br>O001     I001     2023-08-01   10     100 |


```
CREATE TABLE orders(
ord_id TEXT  NOT NULL CHECK (LENGTH(ord_id) = 4),
item_id TEXT NOT NULL,
ord_date  DATE,
ord_qty INTEGER,
cost INTEGER,
PRIMARY KEY (item_id,ord_date)
);
```

**Output:**
<img width="1187" height="389" alt="image" src="https://github.com/user-attachments/assets/84b0b366-f4f8-4e36-a018-21e6d7b89017" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
