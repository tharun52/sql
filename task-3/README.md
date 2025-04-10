## 🧩 **Task 3: Simple Aggregation and Grouping**

### 🎯 **Objective**
- Use aggregate functions like `COUNT()`, `SUM()`, `AVG()` to get insights.
- Group data using `GROUP BY`.
- Filter grouped results using `HAVING`.

---

## ✅ **Step 1: Add More Data (Optional but useful for meaningful aggregation)**

```sql
INSERT INTO Employees (EmployeeID, FirstName, LastName, Department, Salary) VALUES 
(6, 'Fiona', 'Carter', 'Marketing', 72000.00),
(7, 'George', 'Blake', 'HR', 61000.00),
(8, 'Hannah', 'Wells', 'Finance', 78000.00),
(9, 'Ian', 'Lee', 'Engineering', 87000.00),
(10, 'Jane', 'King', 'Engineering', 88000.00);
```

---

## ✅ **Step 2: Total Number of Employees**

```sql
SELECT COUNT(*) AS TotalEmployees FROM Employees;
```

**Result:**
```
+----------------+
| TotalEmployees |
+----------------+
|             10 |
+----------------+
```

---

## ✅ **Step 3: Average Salary Across All Employees**

```sql
SELECT AVG(Salary) AS AverageSalary FROM Employees;
```

**Result:**
```
+---------------+
| AverageSalary |
+---------------+
|     76600.000 |
+---------------+
```

---

## ✅ **Step 4: Number of Employees per Department**

```sql
SELECT Department, COUNT(*) AS NumEmployees 
FROM Employees 
GROUP BY Department;
```

**Result:**
```
+-------------+---------------+
| Department  | NumEmployees  |
+-------------+---------------+
| HR          |             2 |
| Engineering |             4 |
| Marketing   |             2 |
| Finance     |             2 |
+-------------+---------------+
```

---

## ✅ **Step 5: Total Salary by Department**

```sql
SELECT Department, SUM(Salary) AS TotalSalary 
FROM Employees 
GROUP BY Department;
```

**Result:**
```
+-------------+-------------+
| Department  | TotalSalary |
+-------------+-------------+
| HR          |   121000.00 |
| Engineering |   350000.00 |
| Marketing   |   142000.00 |
| Finance     |   153000.00 |
+-------------+-------------+
```

---

## ✅ **Step 6: Departments with Total Salary > 150000 (Using HAVING)**

```sql
SELECT Department, SUM(Salary) AS TotalSalary 
FROM Employees 
GROUP BY Department 
HAVING SUM(Salary) > 150000;
```

**Result:**
```
+-------------+-------------+
| Department  | TotalSalary |
+-------------+-------------+
| Engineering |   350000.00 |
| Finance     |   153000.00 |
+-------------+-------------+
```

---

## 📌 Notes
- `COUNT()`, `SUM()`, `AVG()` are aggregate functions used for summarizing.
- `GROUP BY` is used to group rows by one or more columns.
- `HAVING` is like `WHERE`, but used to filter **aggregated results**.

---
