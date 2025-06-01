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

![438625577-36ff204e-3f8b-416d-82fe-eb1d8f89b143](https://github.com/user-attachments/assets/6e0e6827-5c50-48c7-8196-e4f42a9bca42)


```sql
select date(AppointmentDateTime) as AppointmentDate, count(*) as  TotalAppointments
from Appointments
group by AppointmentDate;
```

**Output:**

![438625779-47d1740e-89ab-4a74-b978-2dd156b5452a](https://github.com/user-attachments/assets/23292941-c639-4026-88ca-d74ebbc298c2)

**Question 2**

![438626791-458094fb-3ec1-464b-a0b1-0e599bf83844](https://github.com/user-attachments/assets/61f4c853-2b55-4b74-b305-b00384b5afec)


```sql
select name,email,length(email) as  min_email_length
from customer
order by length(email)
limit 1;
```

**Output:**

![438626832-7ff52baa-ed62-4bbd-8ecd-103d7fc949f4](https://github.com/user-attachments/assets/00d18ce1-5b8b-4455-b92a-64c851444851)

**Question 3**

![438627161-d054f243-ab5a-49e1-bdd9-071c29ff5199](https://github.com/user-attachments/assets/84f44231-d7c4-4d5d-ba3c-9c91cfeda3de)


```sql
select avg(length(email)) as avg_email_length
from customer
order by length(email)
limit 1;
```

**Output:**

![438627215-c279b3db-a9e8-4dcf-b38a-cd467996b4f9](https://github.com/user-attachments/assets/8826906b-e902-4a93-b344-d4ddafc0197e)

**Question 4**

![438628107-08bb463d-4280-40ab-9aa0-44359d76ce0a](https://github.com/user-attachments/assets/e398ad4d-380b-4e54-8fd2-72b0b290ad91)


```sql
select sum(purch_amt) as TOTAL
from orders
```

**Output:**

![438628183-2eaa2a23-41eb-4ebe-874d-f3cb8da408dc](https://github.com/user-attachments/assets/cb59940b-cb4a-488b-a807-a8a3ffccb7bf)

**Question 5**

![438628502-dac02082-7b58-437f-b882-6a4a8577855e](https://github.com/user-attachments/assets/02e8673a-b2d8-4627-8206-97fdfad482c2)


```sql
select jdate,MIN(workhour)
from employee1
group by jdate
having MIN(workhour) <10 ;
```

**Output:**

![image](https://github.com/user-attachments/assets/686ee1ae-3d1d-47ab-9b33-b20421799714)

**Question 6**

![image](https://github.com/user-attachments/assets/e216271e-d215-42ee-9169-0bedc1d9287c)


```sql
select max(purch_amt) as MAXIMUM
from orders
order by purch_amt;
```

**Output:**

![image](https://github.com/user-attachments/assets/0004a646-5bd4-4a23-a440-9321d86bed74)

**Question 7**

![image](https://github.com/user-attachments/assets/4af387e9-1b11-4116-9abc-6c97a3150d89)


```sql
select address,AVG(salary)
from customer1
group by address
having avg(salary) > 5000
```

**Output:**

![image](https://github.com/user-attachments/assets/a8300202-0010-49b0-8035-fb84fa37341b)

**Question 8**

![image](https://github.com/user-attachments/assets/d499119b-3b85-4206-9ea3-30567f363885)


```sql
select category_id,count(product_name)
from products
group by category_id
having min(category_id) <3
```

**Output:**

![image](https://github.com/user-attachments/assets/515d3e40-2ce6-4fe5-b5de-7cc3dc682703)

**Question 9**

![image](https://github.com/user-attachments/assets/ee6a52f4-a510-4943-892c-6d0168528226)


```sql
select sum(inventory) as total
from fruits
where unit ='LB'
```

**Output:**

![image](https://github.com/user-attachments/assets/6ddad507-e581-4d5d-9f85-e025a18f06e5)

**Question 10**

![image](https://github.com/user-attachments/assets/87f3ec7c-5a83-4743-aa4f-1a02b2cd006d)


```sql
select count(distinct salesman_id) as COUNT
from orders
```

**Output:**

![image](https://github.com/user-attachments/assets/d2f009cf-379c-46d2-9b61-d5e8fa2d62f8)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

![image](https://github.com/user-attachments/assets/76f13057-b2ba-4b90-a996-696d78163b66)

