# 📘 Basic Filtering and Sorting in MySQL

## 🧩 **Task 2: Basic Filtering and Sorting**

### 🎯 **Objective**
- Practice writing SQL queries that **filter** records using conditions.
- Use `ORDER BY` to **sort** the result set.
- Combine multiple conditions using `AND` and `OR`.

---

## 💽 **Using the Same Database**

All queries are executed on the previously created **`presidio`** database and **`Employees`** table.

---

## 🧪 **Queries and Output**

### ✅ 1. **Filter by Department**

```sql
SELECT * FROM Employees WHERE Department = 'Engineering';
```

**Output:**
```
+------------+-----------+----------+-------------+----------+
| EmployeeID | FirstName | LastName | Department  | Salary   |
+------------+-----------+----------+-------------+----------+
|          2 | Bob       | Smith    | Engineering | 85000.00 |
|          5 | Ethan     | Hunt     | Engineering | 90000.00 |
+------------+-----------+----------+-------------+----------+
```

---

### ✅ 2. **Filter by Department and Salary (AND)**

```sql
SELECT * FROM Employees WHERE Department = 'Engineering' AND Salary > 85000;
```

**Output:**
```
+------------+-----------+----------+-------------+----------+
| EmployeeID | FirstName | LastName | Department  | Salary   |
+------------+-----------+----------+-------------+----------+
|          5 | Ethan     | Hunt     | Engineering | 90000.00 |
+------------+-----------+----------+-------------+----------+
```

---

### ✅ 3. **Filter by Multiple Departments (OR)**

```sql
SELECT * FROM Employees WHERE Department = 'HR' OR Department = 'Finance';
```

**Output:**
```
+------------+-----------+----------+------------+----------+
| EmployeeID | FirstName | LastName | Department | Salary   |
+------------+-----------+----------+------------+----------+
|          1 | Alice     | Johnson  | HR         | 60000.00 |
|          4 | Diana     | Prince   | Finance    | 75000.00 |
+------------+-----------+----------+------------+----------+
```

---

### ✅ 4. **Sort by Last Name (Alphabetical Order)**

```sql
SELECT * FROM Employees ORDER BY LastName;
```

**Output:**
```
+------------+-----------+----------+-------------+----------+
| EmployeeID | FirstName | LastName | Department  | Salary   |
+------------+-----------+----------+-------------+----------+
|          3 | Charlie   | Brown    | Marketing   | 70000.00 |
|          5 | Ethan     | Hunt     | Engineering | 90000.00 |
|          1 | Alice     | Johnson  | HR          | 60000.00 |
|          4 | Diana     | Prince   | Finance     | 75000.00 |
|          2 | Bob       | Smith    | Engineering | 85000.00 |
+------------+-----------+----------+-------------+----------+
```

---
