# 📦 eCommerce Database Design & Optimization

This project demonstrates a fully normalized and optimized SQL database schema for a typical eCommerce platform. It includes schema creation, indexing, triggers, transactions, views, and test cases with outputs.

---

## 🧾 Objective

Design a normalized database schema with:

- Schema: Products, Customers, Orders, OrderDetails  
- Optimization: Indexes, performance checks  
- Automation: Triggers  
- Data Integrity: Transactions  
- Reporting: Views / Materialized Views  
- Documentation & Test Queries  

---

## 📐 Schema Design

### 🗃️ Customers
```sql
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    address TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 📦 Products
```sql
CREATE TABLE Products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    price DECIMAL(10, 2) NOT NULL CHECK (price > 0),
    stock_quantity INT NOT NULL CHECK (stock_quantity >= 0)
);
```

### 📑 Orders
```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(50) DEFAULT 'Pending',
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);
```

### 📄 OrderDetails
```sql
CREATE TABLE OrderDetails (
    order_detail_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT NOT NULL CHECK (quantity > 0),
    price DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES Orders(order_id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);
```

---

## 🚀 Indexing & Performance

```sql
CREATE INDEX idx_customer_email ON Customers(email);
CREATE INDEX idx_order_customer ON Orders(customer_id);
CREATE INDEX idx_orderdetails_product ON OrderDetails(product_id);
```

✅ *Boosts search on email, order-customer joins, and product lookups.*

---

## 🔄 Triggers

### 🔁 Update Inventory on Order Insert
```sql
CREATE TRIGGER trg_update_inventory
AFTER INSERT ON OrderDetails
FOR EACH ROW
BEGIN
    UPDATE Products
    SET stock_quantity = stock_quantity - NEW.quantity
    WHERE product_id = NEW.product_id;
END;
```

### ❌ Prevent Orders with Insufficient Stock
```sql
CREATE TRIGGER trg_check_stock
BEFORE INSERT ON OrderDetails
FOR EACH ROW
BEGIN
    DECLARE available_stock INT;
    SELECT stock_quantity INTO available_stock
    FROM Products
    WHERE product_id = NEW.product_id;

    IF available_stock < NEW.quantity THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Insufficient stock for this product.';
    END IF;
END;
```

---

## 🔒 Transactions

### ✔️ Place an Order (Atomic Operation)
```sql
START TRANSACTION;

-- Step 1: Insert Order
INSERT INTO Orders (customer_id) VALUES (1);
SET @order_id = LAST_INSERT_ID();

-- Step 2: Insert Items
INSERT INTO OrderDetails (order_id, product_id, quantity, price)
VALUES 
    (@order_id, 1, 1, 999.99),
    (@order_id, 2, 2, 25.99);

COMMIT;
```

🧪 If any step fails, use `ROLLBACK;`

---

## 📊 Views

### 🔎 Customer Order Summary
```sql
CREATE VIEW CustomerOrderSummary AS
SELECT 
    c.customer_id, c.name, o.order_id, o.order_date, 
    SUM(od.quantity * od.price) AS total_amount
FROM Customers c
JOIN Orders o ON c.customer_id = o.customer_id
JOIN OrderDetails od ON o.order_id = od.order_id
GROUP BY o.order_id;
```

### 📈 Product Sales Summary (Materialized View – if supported)
```sql
CREATE MATERIALIZED VIEW ProductSalesSummary AS
SELECT 
    p.product_id, p.name, SUM(od.quantity) AS total_sold
FROM Products p
JOIN OrderDetails od ON p.product_id = od.product_id
GROUP BY p.product_id;
```

---

## 🧪 Testing & Output

### 🧍 Add Customers & Products
```sql
INSERT INTO Customers (name, email, address) 
VALUES ('John Doe', 'john@example.com', '123 Main Street');

INSERT INTO Products (name, description, price, stock_quantity)
VALUES 
  ('Laptop', 'High performance', 999.99, 10),
  ('Mouse', 'Wireless mouse', 25.99, 50);
```

### 🛍️ Place an Order
```sql
START TRANSACTION;
INSERT INTO Orders (customer_id) VALUES (1);
SET @order_id = LAST_INSERT_ID();

INSERT INTO OrderDetails (order_id, product_id, quantity, price)
VALUES 
    (@order_id, 1, 1, 999.99), -- Laptop
    (@order_id, 2, 2, 25.99);  -- Mouse
COMMIT;
```

### ✅ Output: Stock Updated
```sql
SELECT name, stock_quantity FROM Products;
```

**Output:**
```
+--------+----------------+
| name   | stock_quantity |
+--------+----------------+
| Laptop | 9              |
| Mouse  | 48             |
+--------+----------------+
```

### 👁️ View Customer Summary
```sql
SELECT * FROM CustomerOrderSummary;
```

**Output:**
```
+-------------+----------+----------+---------------------+--------------+
| customer_id | name     | order_id | order_date          | total_amount |
+-------------+----------+----------+---------------------+--------------+
| 1           | John Doe | 1        | 2025-04-14 10:00:00 | 1051.97      |
+-------------+----------+----------+---------------------+--------------+
```


