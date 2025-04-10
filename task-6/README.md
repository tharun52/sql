# 📘 Task 6: Date and Time Functions

## 🎯 Objective:
- Perform **date and time operations** such as calculating intervals, adjusting dates, and filtering using date ranges.
- Format and manipulate dates using **built-in MySQL functions**.

---

## 🧠 Concepts Covered:
- Using `DATEDIFF()` to calculate date differences.
- Using `DATE_ADD()` and `DATE_SUB()` to manipulate dates.
- Filtering with date conditions like **“last 30 days”**.
- Formatting output with `DATE_FORMAT()`.

---

## 🗃️ Sample Setup:

We use an `Orders` table:
```sql
CREATE TABLE Orders (OrderID INT PRIMARY KEY, CustomerID INT, OrderDate DATE, Amount DECIMAL(10,2));
```

We insert sample rows:
```sql
INSERT INTO Orders VALUES 
(1, 101, CURDATE() - INTERVAL 10 DAY, 250.00),
(2, 102, CURDATE() - INTERVAL 35 DAY, 150.00),
(3, 103, CURDATE() - INTERVAL 5 DAY, 300.00),
(4, 104, CURDATE() - INTERVAL 60 DAY, 400.00),
(5, 105, CURDATE(), 500.00);
```

---

## 🧪 Queries Used:

### 🔹 1. Calculate days since order
```sql
SELECT OrderID, OrderDate, DATEDIFF(CURDATE(), OrderDate) AS DaysAgo FROM Orders;
```
📌 This shows how many days ago each order was placed.

---

### 🔹 2. Get orders from the last 30 days
```sql
SELECT * FROM Orders WHERE OrderDate >= CURDATE() - INTERVAL 30 DAY;
```
📌 Filters orders that were placed in the **last 30 days**.

---

### 🔹 3. Add 10 days to the order date (example of `DATE_ADD`)
```sql
SELECT OrderID, OrderDate, DATE_ADD(OrderDate, INTERVAL 10 DAY) AS ExpectedDelivery FROM Orders;
```
📌 Useful for calculating future events like **delivery estimates**.

---

### 🔹 4. Format date output
```sql
SELECT OrderID, DATE_FORMAT(OrderDate, '%M %d, %Y') AS FormattedDate FROM Orders;
```
📌 Displays the date in a more **readable format** like "April 10, 2025".

---

## ✅ Output:
You’ll see how dates are compared, calculated, and formatted using simple MySQL functions, which is essential for any database application involving time-based data.
