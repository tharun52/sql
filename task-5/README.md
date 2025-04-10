# 📘 Task 5: Subqueries and Nested Queries

## 🎯 Objective:
- Use **subqueries** to filter or compute values within a main query.
- Understand the difference between **correlated** and **non-correlated** subqueries.
- Use subqueries in the `SELECT` clause for dynamic values.

---

## 🧠 Concepts Covered:
- Subqueries in `WHERE` clause.
- Correlated vs Non-Correlated Subqueries.
- Subqueries in `SELECT` clause.

---

## 📄 SQL Queries Used:

### 🔹 1. Employees with salary above overall average (Non-Correlated Subquery)
```sql
SELECT * FROM Employees WHERE Salary > (SELECT AVG(Salary) FROM Employees);
```
📌 This query finds employees whose salary is **greater than the overall average salary** of all employees.

---

### 🔹 2. Employees with salary above their department's average (Correlated Subquery)
```sql
SELECT * FROM Employees E WHERE Salary > (SELECT AVG(Salary) FROM Employees WHERE Department = E.Department);
```
📌 This **correlated subquery** compares each employee’s salary to the **average salary of their department**.

---

### 🔹 3. Include department average salary as a column (Subquery in `SELECT`)
```sql
SELECT FirstName, LastName, Department, Salary, (SELECT AVG(Salary) FROM Employees E2 WHERE E2.Department = E1.Department) AS DeptAvgSalary FROM Employees E1;
```
📌 This adds an extra column that shows the **average salary of the employee’s department** next to each row.

---

## ✅ Output:
Each query retrieves relevant and dynamically computed insights using subqueries. These examples help in understanding how **nested queries** enhance SQL's power for reporting and analytics.

---

Let me know if you'd like all five tasks in one combined README!Here's the **README** for **Task 5: Subqueries and Nested Queries** using the `Employees` table in your `presidio` database:

---

# 📘 Task 5: Subqueries and Nested Queries

## 🎯 Objective:
- Use **subqueries** to filter or compute values within a main query.
- Understand the difference between **correlated** and **non-correlated** subqueries.
- Use subqueries in the `SELECT` clause for dynamic values.

---

## 🧠 Concepts Covered:
- Subqueries in `WHERE` clause.
- Correlated vs Non-Correlated Subqueries.
- Subqueries in `SELECT` clause.

---

## 📄 SQL Queries Used:

### 🔹 1. Employees with salary above overall average (Non-Correlated Subquery)
```sql
SELECT * FROM Employees WHERE Salary > (SELECT AVG(Salary) FROM Employees);
```
📌 This query finds employees whose salary is **greater than the overall average salary** of all employees.

---

### 🔹 2. Employees with salary above their department's average (Correlated Subquery)
```sql
SELECT * FROM Employees E WHERE Salary > (SELECT AVG(Salary) FROM Employees WHERE Department = E.Department);
```
📌 This **correlated subquery** compares each employee’s salary to the **average salary of their department**.

---

### 🔹 3. Include department average salary as a column (Subquery in `SELECT`)
```sql
SELECT FirstName, LastName, Department, Salary, (SELECT AVG(Salary) FROM Employees E2 WHERE E2.Department = E1.Department) AS DeptAvgSalary FROM Employees E1;
```
📌 This adds an extra column that shows the **average salary of the employee’s department** next to each row.

---

## ✅ Output:
Each query retrieves relevant and dynamically computed insights using subqueries. These examples help in understanding how **nested queries** enhance SQL's power for reporting and analytics.
