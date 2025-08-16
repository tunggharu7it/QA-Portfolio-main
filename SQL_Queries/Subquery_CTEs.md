# 🧩 Subqueries & CTEs

Advanced queries for validating logic, aggregations, and readable multi-step SQL. Based on real data from the Chinook sample database.

---

## 1. Find customers who spent more than the average

```sql
SELECT CustomerId, Total
FROM (
  SELECT c.CustomerId,
         SUM(il.UnitPrice * il.Quantity) AS Total
  FROM Customer c
  JOIN Invoice i ON c.CustomerId = i.CustomerId
  JOIN InvoiceLine il ON i.InvoiceId = il.InvoiceId
  GROUP BY c.CustomerId
) AS CustomerTotals
WHERE Total > (
  SELECT AVG(CustomerTotal)
  FROM (
    SELECT SUM(il.UnitPrice * il.Quantity) AS CustomerTotal
    FROM Customer c
    JOIN Invoice i ON c.CustomerId = i.CustomerId
    JOIN InvoiceLine il ON i.InvoiceId = il.InvoiceId
    GROUP BY c.CustomerId
  )
);
```

**Result (truncated):**

| CustomerId | Total  |
|------------|--------|
| 8          | 5.94   |
| 14         | 8.91   |
| 23         | 13.86  |
| 46         | 21.86  |
| 25         | 18.86  |
| 26         | 23.86  |
| 6          | 25.86  |
| ...        | ...    |

✅ Confirms that query correctly identifies high-value customers based on invoice totals.

---

## 2. Use CTE to get top 5 longest tracks

```sql
WITH LongTracks AS (
  SELECT Name, Milliseconds
  FROM Track
  ORDER BY Milliseconds DESC
  LIMIT 5
)
SELECT *
FROM LongTracks;
```

**Result:**

| Name                          | Milliseconds |
|-------------------------------|--------------|
| Occupation / Precipice        | 5286953      |
| Through a Looking Glass       | 5088838      |
| Greetings from Earth, Pt. 1   | 2960293      |
| The Man With Nine Lives       | 2956998      |
| Battlestar Galactica, Pt. 2   | 2956081      |

⏱ Tracks returned as expected using clean CTE logic and ordering by duration.

---

📘 *All queries executed and verified in DBeaver against the Chinook SQLite sample database.*