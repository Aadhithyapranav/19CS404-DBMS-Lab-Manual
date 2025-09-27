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
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

```sql
create table Department(
    DepartmentID INTEGER primary key,
    DepartmentName text unique not null,
    Location text
);
```

**Output:**

![Output1](output.png)
<img width="1710" height="511" alt="image" src="https://github.com/user-attachments/assets/7c4dbd91-e31a-4f62-9894-23aa62296fed" />



**Question 2**
---

Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

```sql

ALTER TABLE Student_details
ADD COLUMN Date_of_birth Date;

```

**Output:**

![Output2](output.png)
<img width="1231" height="401" alt="image" src="https://github.com/user-attachments/assets/2fafea34-3035-46eb-8f83-f5a41e539f6e" />


**Question 3**
---

Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE

```sql
CREATE TABLE Employees (
    EmployeeID INTEGER,
    FirstName TEXT,
    LastName TEXT,
    HireDate DATE
);

```

**Output:**

![Output3](output.png)
<img width="1212" height="348" alt="image" src="https://github.com/user-attachments/assets/7b0103b1-2026-4c5a-acc0-98a46e13161a" />


**Question 4**
---

In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

```sql

INSERT INTO Products (ProductID, Name, Category) 
VALUES (106, 'Fitness Tracker', 'Wearables');

INSERT INTO Products (ProductID, Name, Category, Price, Stock) 
VALUES (107, 'Laptop', 'Electronics', 999.99, 50);

INSERT INTO Products (ProductID, Name, Category, Stock) 
VALUES (108, 'Wireless Earbuds', 'Accessories', 100);

```

**Output:**

![Output4](output.png)
<img width="1188" height="237" alt="image" src="https://github.com/user-attachments/assets/97e3060b-b687-4088-a685-fe3592325770" />

**Question 5**
---

Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```sql

CREATE TABLE contacts (
    contact_id INTEGER PRIMARY KEY,
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    email TEXT,
    phone TEXT NOT NULL CHECK (LENGTH(phone) >= 10)
);

```

**Output:**

![Output5](output.png)
<img width="1232" height="306" alt="image" src="https://github.com/user-attachments/assets/b2e6ccf5-a10d-4886-9d39-566668144c8b" />


**Question 6**
---

Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
```sql

CREATE TABLE Shipments (
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderID INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);

```

**Output:**

![Output6](output.png)
<img width="1167" height="252" alt="image" src="https://github.com/user-attachments/assets/e00d53fe-3669-4493-9749-3f89876be006" />


**Question 7**
---

Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.

```sql

CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT CHECK(LENGTH(icom_id) = 4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE
);

```

**Output:**

![Output7](output.png)
<img width="1187" height="393" alt="image" src="https://github.com/user-attachments/assets/e85ab1ba-a49e-413b-9d62-d8e5796661b8" />


**Question 8**
---

Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

```sql

INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (201, 'David Lee', 'M', 'Physics', 92);

```

**Output:**

![Output8](output.png)
<img width="1217" height="300" alt="image" src="https://github.com/user-attachments/assets/d3985e36-cde7-49ec-9115-f519783b86a0" />


**Question 9**
---

Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

```sql

INSERT INTO Products (ProductID, ProductName, Price, Stock)
SELECT ProductID, ProductName, Price, Stock
FROM Discontinued_products;

```

**Output:**

![Output9](output.png)
<img width="1186" height="337" alt="image" src="https://github.com/user-attachments/assets/1f05b464-cd39-4266-8f65-f172026839f5" />


**Question 10**
---

Write a SQL query to Add a new column Country as text in the Student_details table.

```sql

ALTER TABLE Student_details
ADD COLUMN Country TEXT;

```

**Output:**

![Output10](output.png)
<img width="1228" height="402" alt="image" src="https://github.com/user-attachments/assets/a0421e80-ab9f-445a-9318-21d367c70f78" />

**COMPLETION STATUS:**
<img width="1713" height="377" alt="image" src="https://github.com/user-attachments/assets/45e8b215-8fe3-41ec-8a5c-d5499e30d52f" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
