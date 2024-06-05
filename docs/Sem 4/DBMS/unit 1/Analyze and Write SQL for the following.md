Here's the SQL for each of the given scenarios:

(i) **Total salary of each company:**

```sql
SELECT Company_name, SUM(Salary) AS Total_Salary
FROM Employee
GROUP BY Company_name;
```

(ii) **Employee name with the highest salary:**

```sql
SELECT Employee_name
FROM Employee
ORDER BY Salary DESC
LIMIT 1;
```

(iii) **Company name with the lowest average salary:**

```sql
SELECT Company_name
FROM (
    SELECT Company_name, AVG(Salary) AS Avg_Salary
    FROM Employee
    GROUP BY Company_name
    ORDER BY Avg_Salary ASC
    LIMIT 1
) AS Lowest_Avg_Salary;
```

(iv) **Employee names with salary higher than the average salary of TCS:**

```sql
SELECT Employee_name
FROM Employee
WHERE Salary > (
    SELECT AVG(Salary)
    FROM Employee
    WHERE Company_name = 'TCS'
);
```

These SQL queries will help you analyze the data in the "Employee" relation according to the given criteria.
