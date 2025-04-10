# 📘 Creating and Populating Tables in MySQL

## ✅ Objective

This project demonstrates how to:
- Create a MySQL database and table.
- Insert multiple rows into the table.
- Retrieve the inserted data using basic SQL queries.

---
- MySQL Shell installed
- Access to a local or remote MySQL server
- Basic familiarity with SQL commands

---

## 🧱 Steps Performed

### 1. **Create a Database**

```sql
CREATE DATABASE presidio;
```

This command creates a new database named `presidio`.

---

### 2. **Select the Database**

```sql
USE presidio;
```

This sets the default schema to `presidio` for all upcoming operations.

---

### 3. **Create the Table**

```sql
CREATE TABLE Employees (
  EmployeeID INT PRIMARY KEY,
  FirstName VARCHAR(50),
  LastName VARCHAR(50),
  Department VARCHAR(50),
  Salary DECIMAL(10,2)
);
```

This defines an `Employees` table with relevant fields and data types. The `EmployeeID` field is used as the primary key.

---

### 4. **Insert Multiple Rows**

```sql
INSERT INTO Employees (EmployeeID, FirstName, LastName, Department, Salary)
VALUES 
  (1, 'Alice', 'Johnson', 'HR', 60000.00),
  (2, 'Bob', 'Smith', 'Engineering', 85000.00),
  (3, 'Charlie', 'Brown', 'Marketing', 70000.00),
  (4, 'Diana', 'Prince', 'Finance', 75000.00),
  (5, 'Ethan', 'Hunt', 'Engineering', 90000.00);
```

This inserts five sample records into the `Employees` table.

---

### 5. **Retrieve Data**

```sql
SELECT * FROM Employees;
```

This fetches all the data from the `Employees` table and displays it in a tabular format.

---

## 🧪 Output

```
+------------+-----------+----------+-------------+----------+
| EmployeeID | FirstName | LastName | Department  | Salary   |
+------------+-----------+----------+-------------+----------+
|          1 | Alice     | Johnson  | HR          | 60000.00 |
|          2 | Bob       | Smith    | Engineering | 85000.00 |
|          3 | Charlie   | Brown    | Marketing   | 70000.00 |
|          4 | Diana     | Prince   | Finance     | 75000.00 |
|          5 | Ethan     | Hunt     | Engineering | 90000.00 |
+------------+-----------+----------+-------------+----------+
```

---
