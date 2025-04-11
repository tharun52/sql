# 🔄 Task 8: Common Table Expressions (CTEs) and Recursive Queries

## 🎯 Objective:
- Simplify complex queries using **CTEs**.
- Use **recursive CTEs** for hierarchical or tree-structured data.

---

## ✅ Example 1: Non-Recursive CTE – Top Earners in Each Department

```sql
WITH DeptMax AS (
  SELECT Department, MAX(Salary) AS MaxSalary
  FROM Employees
  GROUP BY Department
)
SELECT e.FirstName, e.Department, e.Salary
FROM Employees e
JOIN DeptMax d ON e.Department = d.Department AND e.Salary = d.MaxSalary;
```

### 🔍 Output:

| FirstName | Department  | Salary   |
|-----------|-------------|----------|
| Ethan     | Engineering | 90000.00 |
| Diana     | Finance     | 75000.00 |
| Charlie   | Marketing   | 70000.00 |
| Alice     | HR          | 60000.00 |

> 💡 Lists highest-paid employee(s) per department.

---

## ✅ Example 2: Non-Recursive CTE – Average and Count per Department

```sql
WITH DeptStats AS (
  SELECT Department, COUNT(*) AS EmpCount, AVG(Salary) AS AvgSalary
  FROM Employees
  GROUP BY Department
)
SELECT * FROM DeptStats;
```

### 🔍 Output:

| Department  | EmpCount | AvgSalary |
|-------------|----------|-----------|
| Engineering | 3        | 86666.67  |
| Finance     | 1        | 75000.00  |
| HR          | 1        | 60000.00  |
| Marketing   | 1        | 70000.00  |

---

## ✅ Example 3: Recursive CTE – Organizational Chart with Path

```sql
WITH RECURSIVE OrgPath AS (
  SELECT EmployeeID, FirstName, ManagerID, CONCAT(FirstName) AS Path
  FROM OrgEmployees
  WHERE ManagerID IS NULL
  UNION ALL
  SELECT e.EmployeeID, e.FirstName, e.ManagerID, CONCAT(op.Path, ' > ', e.FirstName)
  FROM OrgEmployees e
  JOIN OrgPath op ON e.ManagerID = op.EmployeeID
)
SELECT * FROM OrgPath ORDER BY EmployeeID;
```

### 🔍 Output:

| EmployeeID | FirstName | ManagerID | Path                   |
|------------|-----------|-----------|------------------------|
| 1          | Alice     | NULL      | Alice                  |
| 2          | Bob       | 1         | Alice > Bob            |
| 3          | Charlie   | 2         | Alice > Bob > Charlie  |
| 4          | Diana     | 2         | Alice > Bob > Diana    |
| 5          | Ethan     | 3         | Alice > Bob > Charlie > Ethan |

> 💡 Shows full path from top manager to each employee.

---
