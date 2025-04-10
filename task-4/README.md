## 🧩 **Task 4: Multi-Table JOINs**

### 🎯 **Objective**
- Create two related tables.
- Use `JOIN` operations to retrieve combined data.

---

## ✅ **Step 1: Create `Customers` and `Orders` Tables**

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100)
);
```

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    ProductName VARCHAR(100),
    OrderDate DATE,
    Amount DECIMAL(10,2),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

---

## ✅ **Step 2: Insert Sample Data**

### `Customers`:

```sql
INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES
(1, 'Alice', 'Walker', 'alice@example.com'),
(2, 'Bob', 'Marley', 'bob@example.com'),
(3, 'Charlie', 'Day', 'charlie@example.com'),
(4, 'Diana', 'Ross', 'diana@example.com');
```

### `Orders`:

```sql
INSERT INTO Orders (OrderID, CustomerID, ProductName, OrderDate, Amount) VALUES
(101, 1, 'Laptop', '2024-01-15', 1200.00),
(102, 1, 'Mouse', '2024-02-01', 25.00),
(103, 2, 'Keyboard', '2024-02-10', 45.00),
(104, 3, 'Monitor', '2024-03-05', 300.00);
```

---

## ✅ **Step 3: INNER JOIN – Customers with Their Orders**

```sql
SELECT 
    Customers.FirstName,
    Customers.LastName,
    Orders.ProductName,
    Orders.OrderDate,
    Orders.Amount
FROM 
    Customers
INNER JOIN 
    Orders ON Customers.CustomerID = Orders.CustomerID;
```

**Result:**
```
+-----------+----------+-------------+------------+--------+
| FirstName | LastName | ProductName | OrderDate  | Amount |
+-----------+----------+-------------+------------+--------+
| Alice     | Walker   | Laptop      | 2024-01-15 | 1200.00|
| Alice     | Walker   | Mouse       | 2024-02-01 |   25.00|
| Bob       | Marley   | Keyboard    | 2024-02-10 |   45.00|
| Charlie   | Day      | Monitor     | 2024-03-05 |  300.00|
+-----------+----------+-------------+------------+--------+
```

---

## ✅ **Step 4: LEFT JOIN – Include All Customers Even Without Orders**

```sql
SELECT 
    Customers.FirstName,
    Customers.LastName,
    Orders.ProductName,
    Orders.OrderDate,
    Orders.Amount
FROM 
    Customers
LEFT JOIN 
    Orders ON Customers.CustomerID = Orders.CustomerID;
```

**Result:**
```
+-----------+----------+-------------+------------+--------+
| FirstName | LastName | ProductName | OrderDate  | Amount |
+-----------+----------+-------------+------------+--------+
| Alice     | Walker   | Laptop      | 2024-01-15 | 1200.00|
| Alice     | Walker   | Mouse       | 2024-02-01 |   25.00|
| Bob       | Marley   | Keyboard    | 2024-02-10 |   45.00|
| Charlie   | Day      | Monitor     | 2024-03-05 |  300.00|
| Diana     | Ross     | NULL        | NULL       |   NULL |
+-----------+----------+-------------+------------+--------+
```

📝 Notice how `Diana Ross` appears in the result **even though she has no orders** — that’s what `LEFT JOIN` does!

---

## 📌 Notes
- `INNER JOIN` shows only matches in both tables.
- `LEFT JOIN` shows all from the left table (`Customers`), even if there's no match in `Orders`.
- `NULL` appears where there's no matching row.
