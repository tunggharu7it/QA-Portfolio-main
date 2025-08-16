# 🛡️ SQL Error Handling & Edge Cases

Real-world examples of how SQL behaves in edge scenarios, observed via DBeaver and SQLite (Chinook sample DB). Designed for QA documentation, debugging, and learning robust practices.

---

## 1️⃣ Insert customer with missing mandatory fields

```sql
INSERT INTO Customer (FirstName)
VALUES ('Ghost');
```

**🧨 DBeaver Error Message:**  
*Cannot insert the value NULL into column 'LastName', 'Email', etc. — violates NOT NULL constraint.*

📎 **Explanation:**  
The `Customer` table requires mandatory fields (`LastName`, `Email`, etc.) due to `NOT NULL` constraints. Skipping these causes integrity violations.

✅ **Expected outcome:**  
Insertion blocked with clear error message. Data integrity preserved.

---

## 2️⃣ Update of non-existent track

```sql
UPDATE Track
  SET UnitPrice = 0.99
WHERE TrackId = 99999;
```

**🧾 Result:**
- `Updated Rows = 0`  
- Execution Time: `0.000s`

📌 **Explanation:**  
SQL executed the query without errors — this is valid behavior when `WHERE` clause matches no rows.

✅ **Correct Outcome:**  
- Query runs successfully  
- No rows affected  
- No integrity constraints violated

🧠 **Tip for QA Logs:**  
Such scenarios are helpful for asserting post-deletion state — queries returning zero affected rows confirm deletion was effective.

---

## 3️⃣ DELETE from protected table with no WHERE clause

```sql
DELETE FROM Employee;
```

**🧷 Result:**
- `Updated Rows = 0`  
- No error or warning

🔒 **Possible safeguards active:**
- Foreign Key constraints prevent deletion
- Triggers or role permissions silently block the operation
- SQLite does not throw errors but disallows change when constraints are violated

⚠️ **Best practice:**  
Use explicit `WHERE` clause and verify affected rows via `SELECT` before deletion.

---

## ✅ Summary Table

| Scenario                              | Error Triggered | Rows Affected | Interpretation                         |
|---------------------------------------|-----------------|----------------|----------------------------------------|
| Insert with missing fields            | ✅               | 0              | Blocked due to NOT NULL constraints    |
| Update after deletion                 | ❌               | 0              | No match found — query runs safely     |
| DELETE from table (no WHERE)          | ❌               | 0              | Blocked silently — likely constraints  |

---

📘 *All queries executed and verified in DBeaver against the Chinook SQLite sample database.*