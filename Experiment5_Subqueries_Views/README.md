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

![438645286-e9bb55a0-ef1c-49e5-9d77-9c147822d3f3](https://github.com/user-attachments/assets/a78db943-fcb0-48b3-9141-0aa4040acaf5)


```sql
SELECT * 
FROM Grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM Grades
    WHERE subject = g.subject
);

```

**Output:**

![image](https://github.com/user-attachments/assets/706eb095-e682-4361-b651-c5290beaf03b)

**Question 2**

![image](https://github.com/user-attachments/assets/438a3ef2-e40f-435f-8779-eba5d3ce11cd)


```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM ORDERS o
JOIN SALESMAN s ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';

```

**Output:**

![image](https://github.com/user-attachments/assets/1f889e21-d1f6-4db1-925c-af8522eefd7a)

**Question 3**

![image](https://github.com/user-attachments/assets/459f351c-c7a4-4c18-aeaa-46a99d1729eb)


```sql
SELECT g.student_name, g.grade
FROM GRADES g
WHERE g.grade = (
    SELECT MAX(g2.grade)
    FROM GRADES g2
    WHERE g2.subject = g.subject
);
```

**Output:**

![image](https://github.com/user-attachments/assets/4e127124-85a1-46d0-ab2d-f2afac2b045f)

**Question 4**

![image](https://github.com/user-attachments/assets/d14c69be-a30f-47c4-9832-bbd847269d51)


```sql
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(*) = 1
);

```

**Output:**

![image](https://github.com/user-attachments/assets/447289c5-280c-43a3-b18e-8924c745f1cc)

**Question 5**

![image](https://github.com/user-attachments/assets/27ed12b3-6c10-4092-b00d-8a81420aefb6)


```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY > 1500;

```

**Output:**

![image](https://github.com/user-attachments/assets/26a03ad4-658b-4d40-9971-70e4bcb6d7e5)

**Question 6**

![image](https://github.com/user-attachments/assets/f65dd57a-8b3a-47d7-8c94-b37f1c6d290d)


```sql
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(c.customer_id) > 1;

```

**Output:**

![image](https://github.com/user-attachments/assets/7e181040-b040-4886-b967-8a0001a6bbd9)

**Question 7**

![image](https://github.com/user-attachments/assets/808408e8-1247-46df-ac5f-81a5384c9df1)


```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE purch_amt > (
    SELECT AVG(purch_amt)
    FROM orders
    WHERE ord_date = '2012-10-10'
);
```

**Output:**

![image](https://github.com/user-attachments/assets/0c5ed138-f98a-4f9c-a6b5-6f0f1091917b)

**Question 8**

![image](https://github.com/user-attachments/assets/b9e11780-9beb-41ae-a2d5-a8c91102599f)


```sql
SELECT *
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);

```

**Output:**

![image](https://github.com/user-attachments/assets/8c5b549d-2bc7-4832-8213-66b966e7efbe)

**Question 9**

![image](https://github.com/user-attachments/assets/a64e12dd-4153-4dcf-bab1-52b5c3c31dcf)


```sql
SELECT *
FROM CUSTOMERS
WHERE AGE < 30;

```

**Output:**

![image](https://github.com/user-attachments/assets/44c588a9-04c8-42c6-9aa1-c9e01f25dc9d)

**Question 10**

![image](https://github.com/user-attachments/assets/4be29dfb-b9b3-4e35-a9b6-116e2b8656b4)


```sql
select medication_id, medication_name, dosage from Medications
where dosage=(select max(dosage) from Medications)
```

**Output:**

![image](https://github.com/user-attachments/assets/31cfccd8-a2f2-4fe6-9ab9-b0dbf417db55)


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.

![image](https://github.com/user-attachments/assets/24dd6d22-3ddb-4d2c-9b8f-7e8d1f448f8a)

![image](https://github.com/user-attachments/assets/1b6404de-49db-4768-89ba-f886b00789c4)
