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
How many patients have expired insurance coverage for each insurance company?

Sample table:Insurance Table

```sql
SELECT
    InsuranceCompany,
    COUNT(*) AS TotalExpiredPatients
    FROM Insurance
    WHERE ValidityPeriod < CURRENT_DATE
    GROUP BY InsuranceCompany
```

**Output:**


<img width="944" height="810" alt="Screenshot 2025-10-25 082730" src="https://github.com/user-attachments/assets/712f4a5e-e1cb-4447-a87d-86d1d81d6984" />


**Question 2**
---
How many medical records were created in each month?

Sample table:MedicalRecords Table

```sql
SELECT 
    strftime('%Y-%m',Date) AS Month,
    COUNT(RecordID) AS TotalRecords 
FROM MedicalRecords 
GROUP BY Month
ORDER BY Month; 
```

**Output:**


<img width="768" height="458" alt="Screenshot 2025-10-25 082912" src="https://github.com/user-attachments/assets/fb3d3f6a-17fd-4374-8185-626ed7e54d2a" />


**Question 3**
---
How many appointments are scheduled for each patient?

```sql
SELECT 
    PatientID,
    COUNT(AppointmentID) AS TotalAppointments
    FROM 
        Appointments
    GROUP BY
        PatientID
```

**Output:**


<img width="772" height="662" alt="image" src="https://github.com/user-attachments/assets/902a06a2-c244-47c5-bb75-54853cb25237" />


**Question 4**
---
Write a SQL query to find the Fruit with the lowest available quantity.

```sql
SELECT
    name AS fruit_name,
    inventory AS lowest_quantity
FROM fruits
ORDER BY inventory ASC
LIMIT 1;
```

**Output:**


<img width="772" height="321" alt="image" src="https://github.com/user-attachments/assets/e2904639-24ca-4e69-9e85-66fac67ffd6d" />


**Question 5**
---
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

```sql
SELECT avg(income) as avg_income from employee where name LIKE 'A%'
```

**Output:**


<img width="525" height="313" alt="image" src="https://github.com/user-attachments/assets/e78f38e0-0a2c-47ee-b328-e288b770a6f8" />


**Question 6**
---
Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

```sql
SELECT sum(purch_amt) as TOTAL from orders
```

**Output:**


<img width="382" height="312" alt="image" src="https://github.com/user-attachments/assets/32242e7c-e7b0-4d9c-ba6e-34b6a507ee09" />


**Question 7**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is not Noida.

```sql
SELECT
    COUNT(*) AS COUNT 
FROM customer 
WHERE city <> 'Noida';
```

**Output:**


<img width="557" height="328" alt="image" src="https://github.com/user-attachments/assets/31b9e0ca-60f2-4f42-9bc6-f00e131c9d62" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.

```sql
SELECT
    city,
    SUM(income) AS 'Income'
FROM employee
GROUP BY city
HAVING SUM(income)>200000;
```

**Output:**


<img width="647" height="546" alt="image" src="https://github.com/user-attachments/assets/649a924d-c97b-4855-904e-11c37cfb36ed" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 1,000,000.

```sql
SELECT
    age,
    MIN(income) AS 'Income'
FROM employee
GROUP BY age
HAVING MIN(income)<1000000;
```

**Output:**

<img width="677" height="453" alt="image" src="https://github.com/user-attachments/assets/91a2d3f9-c2f0-436f-b4c2-3fd9e9d0aa8d" />


**Question 10**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 400,000.

```sql
SELECT
    age,
    MIN(income) AS "MIN(income)"
FROM employee
GROUP BY age
HAVING MIN(income)<400000;
```

**Output:**

<img width="683" height="422" alt="image" src="https://github.com/user-attachments/assets/6aef4a8a-bf70-4f72-b36f-1c2e5659d284" />

**Completion status**

<img width="1768" height="228" alt="image" src="https://github.com/user-attachments/assets/cc32fa94-1065-45d9-ae8f-46685230f388" />




## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
