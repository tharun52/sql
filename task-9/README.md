# 🔧 Task 9: Stored Procedures and User-Defined Functions

## 🎯 Objective

- Use **Stored Procedures** to encapsulate logic that can accept input parameters and return outputs.
- Create **User-Defined Functions (UDFs)** for reusable calculations in queries.
- Simplify complex workflows, promote reusability, and maintain consistency in business logic.

---

## 🗃️ Sample Table: `Orders`

| OrderID | CustomerName | OrderDate  | TotalAmount |
|---------|--------------|------------|-------------|
| 1       | Alice        | 2024-03-10 | 2500.00     |
| 2       | Bob          | 2024-04-05 | 3000.00     |
| 3       | Charlie      | 2024-04-08 | 2000.00     |
| 4       | Diana        | 2024-03-28 | 4000.00     |
| 5       | Ethan        | 2024-04-09 | 1000.00     |
| 6       | Frank        | 2024-04-15 | 5000.00     |

---

## ✅ Example 1: Stored Procedure – Total Sales Between Dates

```sql
DELIMITER $$

CREATE PROCEDURE GetTotalSales(IN start_date DATE, IN end_date DATE)
BEGIN
  SELECT SUM(TotalAmount) AS TotalSales
  FROM Orders
  WHERE OrderDate BETWEEN start_date AND end_date;
END $$

DELIMITER ;
```

### ▶️ Call the procedure:

```sql
CALL GetTotalSales('2024-04-01', '2024-04-30');
```

**📤 Output:**

| TotalSales |
|------------|
| 11000.00   |

---

## ✅ Example 2: Scalar Function – Bonus Calculation Based on Amount

```sql
DELIMITER $$

CREATE FUNCTION CalculateBonus(amount DECIMAL(10,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
  DECLARE bonus DECIMAL(10,2);
  IF amount >= 3000 THEN
    SET bonus = amount * 0.1;
  ELSE
    SET bonus = amount * 0.05;
  END IF;
  RETURN bonus;
END $$

DELIMITER ;
```

### ▶️ Usage:

```sql
SELECT OrderID, CustomerName, TotalAmount, CalculateBonus(TotalAmount) AS Bonus
FROM Orders;
```

**📤 Output:**

| OrderID | CustomerName | TotalAmount | Bonus  |
|---------|--------------|-------------|--------|
| 1       | Alice        | 2500.00     | 125.00 |
| 2       | Bob          | 3000.00     | 300.00 |
| 3       | Charlie      | 2000.00     | 100.00 |
| 4       | Diana        | 4000.00     | 400.00 |
| 5       | Ethan        | 1000.00     | 50.00  |
| 6       | Frank        | 5000.00     | 500.00 |

---

## ✅ Example 3: Stored Procedure – Get High Value Customers

```sql
DELIMITER $$

CREATE PROCEDURE HighValueCustomers(IN min_amount DECIMAL(10,2))
BEGIN
  SELECT CustomerName, TotalAmount
  FROM Orders
  WHERE TotalAmount > min_amount;
END $$

DELIMITER ;
```

### ▶️ Call the procedure:

```sql
CALL HighValueCustomers(3000);
```

**📤 Output:**

| CustomerName | TotalAmount |
|--------------|-------------|
| Diana        | 4000.00     |
| Frank        | 5000.00     |

---

## ✅ Example 4: UDF – Calculate Tax (e.g., 18%)

```sql
DELIMITER $$

CREATE FUNCTION CalculateTax(amount DECIMAL(10,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
  RETURN amount * 0.18;
END $$

DELIMITER ;
```

### ▶️ Usage:

```sql
SELECT OrderID, CustomerName, TotalAmount, CalculateTax(TotalAmount) AS GST
FROM Orders;
```

**📤 Output:**

| OrderID | CustomerName | TotalAmount | GST     |
|---------|--------------|-------------|---------|
| 1       | Alice        | 2500.00     | 450.00  |
| 2       | Bob          | 3000.00     | 540.00  |
| 3       | Charlie      | 2000.00     | 360.00  |
| 4       | Diana        | 4000.00     | 720.00  |
| 5       | Ethan        | 1000.00     | 180.00  |
| 6       | Frank        | 5000.00     | 900.00  |

---
