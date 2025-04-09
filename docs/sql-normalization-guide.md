# 🧠 SQL Normalization: A Simple Guide

**Normalization** is a set of rules that help design relational databases efficiently by reducing redundancy and improving data integrity. These rules are organized into "normal forms".

---

## 🥇 First Normal Form (1NF)

**Rule**: Every column should contain atomic (indivisible) values, and each row should be unique.

### ❌ Bad Example (Not 1NF)

| CustomerId | Name  | PhoneNumbers       |
|------------|-------|--------------------|
| 1          | Alice | 123-456, 789-012   |

Here, `PhoneNumbers` stores multiple values in a single field.

### ✅ Good Example (1NF)

| CustomerId | Name  | PhoneNumber |
|------------|-------|-------------|
| 1          | Alice | 123-456     |
| 1          | Alice | 789-012     |

---

Absolutely! Here's a clearer and slightly more real-world rewrite of **Second Normal Form (2NF)** with a better example and deeper explanation:

---

## 🥈 Second Normal Form (2NF)

### ✅ Rule:
A table is in **2NF** if:
1. It is already in **1NF** (no repeating groups, atomic values),
2. **Every non-key column is fully dependent on the entire primary key** — not just part of it.

This rule mostly applies when you have **composite primary keys** (i.e., two or more columns making up the key).

---

### 🧾 Real-World Scenario: Orders and Products

Imagine we have a table that records which products are in which orders, along with product information:

### ❌ Bad Example (Not 2NF — Partial Dependency)

| **OrderId** | **ProductId** | **ProductName** | **UnitPrice** | **Quantity** |
|-------------|---------------|------------------|----------------|--------------|
| 1001        | 2001          | Coffee           | 5.99           | 2            |
| 1001        | 2002          | Tea              | 3.49           | 1            |

Here, the **composite key** is `(OrderId, ProductId)` — together they identify the row.

But:
- `ProductName` and `UnitPrice` only depend on `ProductId`, not the full key.
- This causes **redundancy** (if "Coffee" appears in multiple orders, its name and price are repeated).

---

### ✅ Good Example (Normalized to 2NF)

Split the table into two:

#### 🔹 `OrderProduct` (many-to-many relationship)

| **OrderId** | **ProductId** | **Quantity** |
|-------------|---------------|--------------|
| 1001        | 2001          | 2            |
| 1001        | 2002          | 1            |

#### 🔹 `Product` (product data belongs here)

| **ProductId** | **ProductName** | **UnitPrice** |
|---------------|------------------|----------------|
| 2001          | Coffee           | 5.99           |
| 2002          | Tea              | 3.49           |

Now:

- Each non-key column in `OrderProduct` depends **only on the full key** (`OrderId + ProductId`).
- Product-related info lives in a separate table.

---

### 🤓 Why It Matters

- Prevents duplication of product data across many orders
- Easier to update (change price once)
- Reduces potential inconsistencies

---

## 🥉 Third Normal Form (3NF)

**Rule**: Must be in 2NF, and all columns must depend **only on the key**, not on other non-key columns.

### ❌ Bad Example (Not 3NF)

| CustomerId | Name  | ZipCode | City     |
|------------|-------|---------|----------|
| 1          | Alice | 12345   | Oslo     |

Here, `City` depends on `ZipCode`, not on `CustomerId`.

### ✅ Good Example (3NF)

Split into:

**Customer**

| CustomerId | Name  | ZipCode |
|------------|-------|---------|
| 1          | Alice | 12345   |

**ZipCodeInfo**

| ZipCode | City     |
|---------|----------|
| 12345   | Oslo     |

---

## 🧠 Summary

| Normal Form | Fixes Problem With                    |
|-------------|----------------------------------------|
| 1NF         | Repeating groups / multivalued fields  |
| 2NF         | Partial dependencies (on part of a key)|
| 3NF         | Transitive dependencies                |

---

Normalization helps build databases that are:

- Easier to maintain
- Less redundant
- More consistent

However, denormalization (intentionally breaking these rules) is sometimes useful for performance.
