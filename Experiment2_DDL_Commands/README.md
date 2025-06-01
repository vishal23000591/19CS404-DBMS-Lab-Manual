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
Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).
For example:

| cid | name       | type       | notnull | dflt_value | pk |
|-----|------------|------------|---------|------------|----|
| 0   | id         | integer    | 0       |            | 0  |
| 1   | salary     | number     | 0       |            | 0  |
| 2   | first_name | varchar(50)| 0       |            | 0  |
| 3   | last_name  | varchar(50)| 0       |            | 0  |

```sql
ALTER TABLE employee 
ADD COLUMN first_name varchar(50);

ALTER TABLE employee 
ADD COLUMN last_name varchar(50);
```

**Output:**
![image](https://github.com/user-attachments/assets/2f4d836d-4533-4b79-acc3-37f646320a1f)


**Question 2**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT

| cid | name        | type    | notnull | dflt_value | pk |
|-----|-------------|---------|---------|-------------|----|
| 0   | ReviewID    | INTEGER | 0       |             | 0  |
| 1   | ProductID   | INTEGER | 0       |             | 0  |
| 2   | Rating      | REAL    | 0       |             | 0  |
| 3   | ReviewText  | TEXT    | 0       |             | 0  |


```sql
CREATE TABLE Reviews(
    ReviewID INTEGER ,
    ProductID INTEGER,
    Rating REAL,
    ReviewText TEXT
)
```

**Output:**

![image](https://github.com/user-attachments/assets/1967ba09-5c46-41a9-acf9-ed601c45e951)


**Question 3**
---
Create a new table named products with the following specifications:

product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0

For example:

Test	Result
INSERT INTO products (product_id, product_name, list_price) VALUES (2, 'Product B', 50.00);
SELECT * FROM products;

| product_id | product_name | list_price | discount |
|------------|--------------|------------|----------|
| 2          | Product B    | 50         | 0        |

```sql
CREATE TABLE products(
    product_id INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    list_price DECIMAL(10,2) NOT NULL,
    discount DECIMAL(10,2) NOT NULL DEFAULT 0,
    CHECK(list_price>=discount AND discount>=0 AND list_price>=0)
)
```

**Output:**

![image](https://github.com/user-attachments/assets/7a53f948-fe7c-409e-a9c9-da4c010695d0)


**Question 4**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

For example:

Test
SELECT ProductID, Name, Category, Price, Stock 
FROM Products 
WHERE ProductID = 104;

	Result
| ProductID | Name   | Category     | Price | Stock |
|-----------|--------|--------------|-------|-------|
| 104       | Tablet | Electronics  | 100   | 50    |



```sql
INSERT INTO Products (ProductID, Name, Category)  
VALUES (104, 'Tablet', 'Electronics');
```

**Output:**

![image](https://github.com/user-attachments/assets/13299dd9-74cf-4171-8182-d70c51440841)


**Question 5**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700         COM5


```sql
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT(4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
    ON UPDATE CASCADE
    ON DELETE CASCADE
);
```

**Output:**
![image](https://github.com/user-attachments/assets/4bd66829-f890-4cd3-b7d7-70a77c3b05d2)

**Question 6**
---
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
For example:

Test	Result
INSERT INTO Department (DepartmentID, DepartmentName, Location) VALUES (1, 'Human Resources', 'New York');
select * from Department;
DepartmentID  DepartmentName   Location
------------  ---------------  ----------
1             Human Resources  New York


```sql
CREATE TABLE Department (
    DepartmentID INTEGER PRIMARY KEY,
    DepartmentName TEXT UNIQUE NOT NULL,
    Location TEXT
);
```

**Output:**

![image](https://github.com/user-attachments/assets/1de692b9-f883-48c1-bb64-3cac69b45412)


**Question 7**
---
Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

For example:

Test	Result
pragma table_info('Student_details');
cid    name             type             notnu  dflt_value  pk
-----  ---------------  ---------------  -----  ----------  ----------
0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      MobileNumber     NUMBER           0                  0
6      Address          VARCHAR(100)     0                  0


```sql
ALTER TABLE Student_details
ADD COLUMN MobileNumber NUMBER;

ALTER TABLE Student_details
ADD COLUMN Address VARCHAR(100);
```

**Output:**

![image](https://github.com/user-attachments/assets/93b2d74f-4fb3-4cb2-915b-5f40c8fa8015)


**Question 8**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint failed


```sql
CREATE TABLE  ProjectAssignments(
    AssignmentID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    ProjectID INTEGER,
    AssignmentDate DATE NOT NULL,
    FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID)
    FOREIGN KEY(ProjectID) REFERENCES Projects(ProjectID)
    
)
```

**Output:**

![image](https://github.com/user-attachments/assets/f099acd8-06d6-4181-812b-f603f5b35d07)

**Question 9**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

For example:

Test	Result
select * from Books;
ISBN            Title           Author              Publisher      YearPublished
--------------  --------------  ------------------  -------------  -------------
978-1234567890  The Lost World  Arthur Conan Doyle  Vintage Books  1912
978-0987654321  Gone with the   Margaret Mitchell   Macmillan      1936
978-1122334455  Moby Dick       Herman Melville     Harper & Brot  1851


```sql
INSERT INTO Books (ISBN, Title, Author, Publisher, YearPublished)  
SELECT ISBN, Title, Author, Publisher, YearPublished  
FROM Out_of_print_books;
```

**Output:**

![image](https://github.com/user-attachments/assets/51e1b151-8e24-4356-8419-1a26f43b7274)


**Question 10**
---
In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375
 

For example:

Test	Result
SELECT * FROM Customers;
CustomerID  Name          Address     City        ZipCode
----------  ------------  ----------  ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Mano  Gotham      10007
308         Peter Parker  Queens                  11375


```sql

INSERT INTO Customers (CustomerID, Name, Address)  
VALUES (306, 'Diana Prince', 'Themyscira');

INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)  
VALUES (307, 'Bruce Wayne', 'Wayne Manor', 'Gotham', '10007');

INSERT INTO Customers (CustomerID, Name, Address, ZipCode)  
VALUES (308, 'Peter Parker', 'Queens', '11375');
```

**Output:**

![image](https://github.com/user-attachments/assets/8d670d86-a9be-42e7-96a8-530a18a2e304)



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

![image](https://github.com/user-attachments/assets/d4a44ea6-c0a5-4803-97b0-287246937f28)
