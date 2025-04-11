# 🧮 Task 7: Window Functions and Ranking

## 🎯 Objective:
Learn how to apply **window functions** to rank, compare, and analyze rows within partitions of data in SQL.

---

## 📚 Key Concepts:
- `ROW_NUMBER()` – Assigns unique numbers to rows within a partition.
- `RANK()` – Assigns same rank to ties, with gaps.
- `DENSE_RANK()` – Like `RANK()` but **without gaps**.
- `LEAD()` / `LAG()` – Access **next** or **previous** row values.
- `PARTITION BY` – Divides result into groups (like per department).
- `ORDER BY` – Defines sorting within each partition for ranking/comparison.

---

## 🗂️ Table Used: `Employees`

| EmployeeID | FirstName | LastName | Department  | Salary   |
|------------|-----------|----------|-------------|----------|
| 1          | Alice     | Johnson  | HR          | 60000.00 |
| 2          | Bob       | Smith    | Engineering | 85000.00 |
| 3          | Charlie   | Brown    | Marketing   | 70000.00 |
| 4          | Diana     | Prince   | Finance     | 75000.00 |
| 5          | Ethan     | Hunt     | Engineering | 90000.00 |
| 6          | Fay       | Wilson   | Engineering | 85000.00 |

---

## 🔹 1. `ROW_NUMBER()` – Rank employees by salary within each department

```sql
SELECT *, ROW_NUMBER() OVER(PARTITION BY Department ORDER BY Salary DESC) AS RowNum 
FROM Employees;
```

### ✅ Output:

| EmployeeID | FirstName | LastName | Department  | Salary   | RowNum |
|------------|-----------|----------|-------------|----------|--------|
| 5          | Ethan     | Hunt     | Engineering | 90000.00 | 1      |
| 2          | Bob       | Smith    | Engineering | 85000.00 | 2      |
| 6          | Fay       | Wilson   | Engineering | 85000.00 | 3      |
| 4          | Diana     | Prince   | Finance     | 75000.00 | 1      |
| 1          | Alice     | Johnson  | HR          | 60000.00 | 1      |
| 3          | Charlie   | Brown    | Marketing   | 70000.00 | 1      |

---

## 🔹 2. `RANK()` – Rank with gaps for ties

```sql
SELECT *, RANK() OVER(PARTITION BY Department ORDER BY Salary DESC) AS RankBySalary 
FROM Employees;
```

### ✅ Output:

| EmployeeID | FirstName | LastName | Department  | Salary   | RankBySalary |
|------------|-----------|----------|-------------|----------|--------------|
| 5          | Ethan     | Hunt     | Engineering | 90000.00 | 1            |
| 2          | Bob       | Smith    | Engineering | 85000.00 | 2            |
| 6          | Fay       | Wilson   | Engineering | 85000.00 | 2            |
| 4          | Diana     | Prince   | Finance     | 75000.00 | 1            |
| 1          | Alice     | Johnson  | HR          | 60000.00 | 1            |
| 3          | Charlie   | Brown    | Marketing   | 70000.00 | 1            |

---

## 🔹 3. `DENSE_RANK()` – Rank without gaps

```sql
SELECT *, DENSE_RANK() OVER(PARTITION BY Department ORDER BY Salary DESC) AS DenseRank 
FROM Employees;
```

### ✅ Output:

| EmployeeID | FirstName | LastName | Department  | Salary   | DenseRank |
|------------|-----------|----------|-------------|----------|-----------|
| 5          | Ethan     | Hunt     | Engineering | 90000.00 | 1         |
| 2          | Bob       | Smith    | Engineering | 85000.00 | 2         |
| 6          | Fay       | Wilson   | Engineering | 85000.00 | 2         |
| 4          | Diana     | Prince   | Finance     | 75000.00 | 1         |
| 1          | Alice     | Johnson  | HR          | 60000.00 | 1         |
| 3          | Charlie   | Brown    | Marketing   | 70000.00 | 1         |

---

## 🔹 4. `LEAD()` and `LAG()` – Compare with next/previous salary in department

```sql
SELECT 
  EmployeeID, FirstName, Department, Salary,
  LAG(Salary) OVER(PARTITION BY Department ORDER BY Salary DESC) AS PrevSalary,
  LEAD(Salary) OVER(PARTITION BY Department ORDER BY Salary DESC) AS NextSalary
FROM Employees;
```

### ✅ Output:

| EmployeeID | FirstName | Department  | Salary   | PrevSalary | NextSalary |
|------------|-----------|-------------|----------|------------|------------|
| 5          | Ethan     | Engineering | 90000.00 | NULL       | 85000.00   |
| 2          | Bob       | Engineering | 85000.00 | 90000.00   | 85000.00   |
| 6          | Fay       | Engineering | 85000.00 | 85000.00   | NULL       |
| 4          | Diana     | Finance     | 75000.00 | NULL       | NULL       |
| 1          | Alice     | HR          | 60000.00 | NULL       | NULL       |
| 3          | Charlie   | Marketing   | 70000.00 | NULL       | NULL       |

---

## ✅ Summary:
Window functions provide advanced capabilities for ranking, comparison, and trend analysis across grouped data without collapsing the rows — ideal for analytics!
