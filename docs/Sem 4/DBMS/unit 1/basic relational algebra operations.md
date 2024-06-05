1. **Selection (σ)**:

   - Selects rows from a relation that satisfy a specified condition.

   Example: Consider a table named "Employees" with columns "Name", "Age", and "Department". To select all employees who are in the "IT" department:

   ```
   σ_Department='IT'(Employees)
   ```

2. **Projection (π)**:

   - Selects specific columns from a relation.

   Example: If we want to select only the "Name" and "Age" columns from the "Employees" table:

   ```
   π_Name, Age(Employees)
   ```

3. **Union (∪)**:

   - Combines two relations to produce a result that includes all tuples from both relations, eliminating duplicates.

   Example: Suppose we have two tables, "Sales2019" and "Sales2020", both containing sales data. To get a combined list of sales from both years:

   ```
   Sales2019 ∪ Sales2020
   ```

4. **Intersection (∩)**:

   - Returns a relation containing only tuples that appear in both input relations.

   Example: If we want to find customers who made purchases in both 2019 and 2020, given "Customers2019" and "Customers2020":

   ```
   Customers2019 ∩ Customers2020
   ```

5. **Set Difference (−)**:

   - Returns tuples that are present in the first relation but not in the second relation.

   Example: To find customers who made purchases in 2019 but not in 2020, given "Customers2019" and "Customers2020":

   ```
   Customers2019 - Customers2020
   ```

6. **Cartesian Product (×)**:

   - Combines every tuple from the first relation with every tuple from the second relation, resulting in a new relation with all possible combinations of tuples.

   Example: If we have tables "Students" and "Courses", and we want to find all possible combinations of students and courses they can take:

   ```
   Students × Courses
   ```

7. **Join (⨝)**:

   - Combines tuples from two relations based on a common attribute.

   Example: If we have tables "Employees" and "Departments", and we want to find employees along with their respective departments:

   ```
   Employees ⨝ Department
   ```

These are some basic examples of how relational algebra operations can be practically applied to manipulate and query relational databases.
