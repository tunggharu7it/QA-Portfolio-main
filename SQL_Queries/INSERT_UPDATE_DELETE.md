# ✍️ INSERT / UPDATE / DELETE Queries

Examples of modifying database content manually using SQL. All scripts are executed against the Chinook (SQLite) schema with real output captured from DBeaver.

---

## 1. Insert a new customer

```sql
INSERT INTO Customer (FirstName, LastName, Country, Email)
VALUES ('Ivan', 'Shevchenko', 'Ukraine', 'ivan.shevchenko@example.com');
```

**Result:**

```text
Updated Rows: `1`  
Execute Time: `0.010s`  
```

Query executed successfully ✅

---

## 2. Update track price

```sql
UPDATE Track
SET UnitPrice = 1.29
WHERE Name = 'Fire In Space';
```

**Result:**

```text
Updated Rows: `1`  
Execute Time: `0.012s`  
```

Track price modified successfully 💵

---

## 3. Delete invoice lines with quantity zero

```sql
DELETE FROM InvoiceLine
WHERE Quantity = 0;
```

**Result:**

```text
Updated Rows: `0`  
Execute Time: `0.018s`
```

No matching records found 🧼 (safe cleanup attempt)

---

📘 *All queries executed and verified in DBeaver against the Chinook SQLite sample database.*