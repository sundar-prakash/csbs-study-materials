Data normalization is the process of organizing data in a database to reduce redundancy and dependency. It ensures that each piece of data is stored in the most logical and efficient manner. The normalization process typically involves breaking down larger tables into smaller ones and establishing relationships between them. There are several normal forms, with the most common being the first, second, and third normal forms (1NF, 2NF, and 3NF).

Let's explore each of these normal forms with examples:

### First Normal Form (1NF):

1NF requires that each column in a table contains atomic (indivisible) values, and there are no repeating groups or arrays of data.

**Example:**

Consider a table named "StudentCourses" with the following columns:

- Student_ID
- Courses (comma-separated list of courses)

```
Student_ID   | Courses
-------------------------
1            | Math, Science
2            | English
3            | History, Geography, Math
```

To achieve 1NF, we need to break down the "Courses" column into separate rows:

```
Student_ID   | Course
---------------------
1            | Math
1            | Science
2            | English
3            | History
3            | Geography
3            | Math
```

### Second Normal Form (2NF):

2NF requires that a table is in 1NF and that all non-key attributes are fully functionally dependent on the primary key.

**Example:**

Consider a table named "EmployeeDetails" with the following columns:

- Employee_ID
- Department
- Manager_ID
- Manager_Name

In this table, "Manager_Name" depends only on "Manager_ID", not on the entire primary key ("Employee_ID"). To achieve 2NF, we split the table into two:

Table: "Employees"

```
Employee_ID   | Department   | Manager_ID
-----------------------------------------
101           | HR           | 201
102           | IT           | 202
```

Table: "Managers"

```
Manager_ID    | Manager_Name
----------------------------
201           | John
202           | Emily
```

### Third Normal Form (3NF):

3NF requires that a table is in 2NF and that there are no transitive dependencies, meaning that non-key attributes are not dependent on other non-key attributes.

**Example:**

Consider a table named "EmployeeSalaries" with the following columns:

- Employee_ID
- Department
- Manager_ID
- Manager_Salary

Here, "Manager_Salary" depends on "Manager_ID", which is not the primary key. To achieve 3NF, we further split the table:

Table: "Employees"

```
Employee_ID   | Department   | Manager_ID
-----------------------------------------
101           | HR           | 201
102           | IT           | 202
```

Table: "Managers"

```
Manager_ID    | Manager_Salary
-------------------------------
201           | 5000
202           | 6000
```

In this way, each table in 3NF contains only information directly related to the primary key, without any indirect dependencies.

By applying the principles of these normal forms, we can ensure that our database is well-structured, efficient, and free from redundancy.
