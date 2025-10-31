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
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
name   city
-----  ---------------
Neha   Bangalore
Rohit  Bangalore
Manoj  Bangalore
Vivek  Chandigarh

```sql
SELECT
    name,
    city
FROM
    customer
WHERE
    city IN (
        SELECT
            city
        FROM
            customer
        WHERE
            id IN (3, 7)
    );
```

**Output:**

<img width="1042" height="478" alt="Screenshot 2025-10-31 104811" src="https://github.com/user-attachments/assets/149d0f91-7644-42de-ae63-7fae50f3c687" />


**Question 2**
---
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
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(c.customer_id) > 1;

```

**Output:**

<img width="817" height="494" alt="Screenshot 2025-10-31 104820" src="https://github.com/user-attachments/assets/23c8bc05-e04f-48ae-b18f-2e6d031dd294" />


**Question 3**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE

name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)

ORDERS TABLE

name            type
----------      ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70002       65.26       2012-10-05  3002         5001
70005       2400.6      2012-07-27  3007         5001
70008       5760.0      2012-09-10  3002         5001
70013       3045.6      2012-04-25  3002         5001


```sql
SELECT
    T1.ord_no,
    T1.purch_amt,
    T1.ord_date,
    T1.customer_id,
    T1.salesman_id
FROM
    orders AS T1  -- T1 is the ORDERS TABLE
INNER JOIN
    salesman AS T2  -- T2 is the SALESMAN TABLE
ON
    T1.salesman_id = T2.salesman_id
WHERE
    T2.city = 'New York';
```

**Output:**

<img width="1146" height="506" alt="Screenshot 2025-10-31 104829" src="https://github.com/user-attachments/assets/41359c00-e608-4dc4-8161-4258b460e74f" />


**Question 4**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)



For example:

Result
medic  medication_name  dosage
-----  ---------------  ---------------
4      Acetaminophen    600mg

```sql
SELECT
    medication_id,
    medication_name,
    dosage
FROM
    Medications
WHERE
    dosage = (
        SELECT
            MAX(dosage)
        FROM
            Medications
    );
```

**Output:**

<img width="967" height="434" alt="Screenshot 2025-10-31 104839" src="https://github.com/user-attachments/assets/e404450c-8daf-4734-b1e4-97a0a623f41b" />


**Question 5**
---
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)



For example:

Result
medic  medication_name  dosage
-----  ---------------  ---------------
2      Ibuprofen        200mg


```sql
SELECT
    medication_id,
    medication_name,
    dosage
FROM
    Medications
WHERE
    dosage = (
        SELECT
            Min(dosage)
        FROM
            Medications
    );
```

**Output:**

<img width="976" height="431" alt="Screenshot 2025-10-31 104849" src="https://github.com/user-attachments/assets/22867669-9f37-4bb5-bff1-9ee959a1f4eb" />


**Question 6**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

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
SELECT
    *
FROM
    CUSTOMERS
WHERE
    SALARY = 1500;
```

**Output:**

<img width="1142" height="380" alt="Screenshot 2025-10-31 104857" src="https://github.com/user-attachments/assets/8d591c69-a886-476f-9f4d-e14003a12c7b" />


**Question 7**
---
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

```sql
SELECT *
FROM customer
WHERE customer_id = (
    SELECT salesman_id - 2001
    FROM salesman
    WHERE name = 'Mc Lyon'
);

```

**Output:**

<img width="1175" height="352" alt="Screenshot 2025-10-31 104905" src="https://github.com/user-attachments/assets/e998d550-a620-4351-9da9-2fb7de329ea9" />


**Question 8**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
name
---------------
Aarti Desai
Vivek Sharma
Nisha Patel
Rajesh Singh
Radha Iyer


```sql
SELECT
    name
FROM
    customer
WHERE
    phone IN (
        SELECT
            phone
        FROM
            customer
        GROUP BY
            phone
        HAVING
            COUNT(phone) = 1
    );
```

**Output:**

<img width="944" height="484" alt="Screenshot 2025-10-31 104915" src="https://github.com/user-attachments/assets/fa23dd35-7611-4748-bc20-8c466452c512" />


**Question 9**
---
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



For example:

Result
student_id       student_name     subject          grade
---------------  ---------------  ---------------  ---------------
2                Bob              Math             85
6                Frank            Science          85
7                John             Social           85
```sql
SELECT *
FROM Grades g
WHERE grade = (
    SELECT MIN(grade)
    FROM Grades
    WHERE subject = g.subject
);

```

**Output:**

<img width="1232" height="458" alt="Screenshot 2025-10-31 104924" src="https://github.com/user-attachments/assets/08c2ea3e-04f5-4f2d-a46c-8d8e1a8091c9" />


**Question 10**
---
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

```sql
SELECT
    T2.ord_no,
    T2.purch_amt,
    T2.ord_date,
    T2.salesman_id
FROM
    salesman AS T1
INNER JOIN
    orders AS T2
ON
    T1.salesman_id = T2.salesman_id
WHERE
    T1.commission = (
        SELECT
            MAX(commission)
        FROM
            salesman
    );
```

**Output:**

<img width="1005" height="493" alt="Screenshot 2025-10-31 104932" src="https://github.com/user-attachments/assets/94ee9ff0-fa15-470d-90e1-240d5e2be020" />

## COMPLITION STATUS

<img width="1437" height="166" alt="Screenshot 2025-10-31 110334" src="https://github.com/user-attachments/assets/75b77420-414e-4ea8-8219-45a7f0ad6160" />




## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
