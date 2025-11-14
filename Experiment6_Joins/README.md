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

```sql
SELECT
    T1.cust_name AS "Customer Name",
    T1.city AS "city",
    T2.name AS "Salesman",
    T2.commission AS "commission"
FROM
    customer AS T1
INNER JOIN
    salesman AS T2
ON
    T1.salesman_id = T2.salesman_id;
```

**Output:**

<img width="1306" height="902" alt="image" src="https://github.com/user-attachments/assets/1ffb652c-923c-4683-8d89-44e7c96a6dbc" />


**Question 2**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

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
SELECT
    T1.cust_name,
    T1.city,
    T1.grade,
    T2.name AS Salesman,
    T2.city AS "city"
FROM
    customer AS T1
INNER JOIN
    salesman AS T2
ON
    T1.salesman_id = T2.salesman_id
ORDER BY
    T1.customer_id ASC;
```

**Output:**

<img width="1330" height="809" alt="image" src="https://github.com/user-attachments/assets/ba59eb42-61dc-4e3d-ad4e-b51aef2a7883" />


**Question 3**
---
Write the SQL query that achieves the selection of the first name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date of '2024-01-15'.:

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

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE

```sql
SELECT
    T1.first_name
FROM
    patients AS T1  
INNER JOIN
    surgeries AS T2  
ON
    T1.patient_id = T2.patient_id
WHERE
    T2.surgery_date = '2024-01-15';
```

**Output:**

<img width="1287" height="485" alt="image" src="https://github.com/user-attachments/assets/fe06a003-fc7e-44cc-900b-b3fe87cf4d04" />


**Question 4**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount greater than 1000.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
SELECT
    c.cust_name,
    o.ord_no,
    o.ord_date,
    o.purch_amt
FROM
    customer AS c
LEFT JOIN
    orders AS o
ON
    c.customer_id = o.customer_id
WHERE
    o.purch_amt > 1000;
```

**Output:**

<img width="1311" height="704" alt="image" src="https://github.com/user-attachments/assets/0f00b946-1d87-445e-8321-9cc41507eb96" />


**Question 5**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id



APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date



```sql
SELECT
    T1.first_name AS patient_name,
    T2.*
FROM
    PATIENTS AS T1
INNER JOIN
    APPOINTMENTS AS T2
ON
    T1.patient_id = T2.patient_id;
```

**Output:**

<img width="1347" height="484" alt="image" src="https://github.com/user-attachments/assets/efcf68e4-c3fa-4472-afa7-cace5ae5ce9e" />


**Question 6**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-02-01' and '2024-02-28'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id



APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date



```sql
SELECT
    p.*
FROM
    PATIENTS AS p
INNER JOIN
    APPOINTMENTS AS a
ON
    p.patient_id = a.patient_id
WHERE
    a.appointment_date BETWEEN '2024-02-01' AND '2024-02-28'
GROUP BY
    p.patient_id;
```

**Output:**

<img width="1361" height="345" alt="image" src="https://github.com/user-attachments/assets/f3959327-0be8-4f6d-9cdf-a6675beaaa9b" />


**Question 7**
---
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
SELECT 
    s.name AS Salesman,
    c.cust_name,
    s.city
FROM 
    salesman s
INNER JOIN 
    customer c
ON 
    s.city = c.city;

```

**Output:**

<img width="1340" height="633" alt="image" src="https://github.com/user-attachments/assets/7b085716-a195-4841-8576-51914cc6cad5" />


**Question 8**
---
Write an SQL query to select the 'cust_name' column from the 'customer' table (aliased as 'c'), using a LEFT JOIN with the 'orders' table based on the 'customer_id' column.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
SELECT
    c.cust_name
FROM
    customer AS c
LEFT JOIN
    orders AS o
ON
    c.customer_id = o.customer_id;
```

**Output:**

<img width="1345" height="968" alt="image" src="https://github.com/user-attachments/assets/d557cc12-2a94-41da-88af-98b57d55dce2" />


**Question 9**
---
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

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
SELECT
    T1.cust_name,
    T1.city,
    T2.ord_no,
    T2.ord_date,
    T2.purch_amt AS "Order Amount",
    T3.name AS name,
    T3.commission
FROM
    customer AS T1
LEFT JOIN
    orders AS T2
ON
    T1.customer_id = T2.customer_id
LEFT JOIN
    salesman AS T3
ON
    T1.salesman_id = T3.salesman_id;
```

**Output:**

<img width="1363" height="891" alt="image" src="https://github.com/user-attachments/assets/d32da5ee-ee25-4646-85a2-3753e3b00070" />


**Question 10**
---
 From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

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
SELECT
    T1.cust_name AS "Customer Name",
    T1.city AS "city",
    T2.name AS Salesman,
    T2.commission AS commission
FROM
    customer AS T1
INNER JOIN
    salesman AS T2
ON
    T1.salesman_id = T2.salesman_id
WHERE
    T2.commission > 0.12;
```

**Output:**

<img width="1320" height="771" alt="image" src="https://github.com/user-attachments/assets/314b9c56-b30a-40b2-a435-abeb0fb8e6a9" />

## COMPLETION STATUS

<img width="1607" height="196" alt="image" src="https://github.com/user-attachments/assets/1a14af1d-5094-4d09-9fd9-64ebc1111df1" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
