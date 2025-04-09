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

## 🥈 Second Normal Form (2NF)

**Rule**: Must be in 1NF and all non-key attributes must depend on the whole primary key.

### ❌ Bad Example (Not 2NF)

| OrderId | ProductId | ProductName | Price |
|---------|-----------|-------------|-------|
| 101     | 2001      | Apples      | 3.00  |

Here, `ProductName` and `Price` depend **only on ProductId**, not the full key `(OrderId, ProductId)`.

### ✅ Good Example (2NF)

Split into two tables:

**OrderProduct**

| OrderId | ProductId |
|---------|-----------|
| 101     | 2001      |

**Product**

| ProductId | ProductName | Price |
|-----------|-------------|-------|
| 2001      | Apples      | 3.00  |

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
