# 🔗 JOIN_Queries.md

Join-based queries on the Chinook sample database to explore relationships across tables such as Album, Customer, Employee, and InvoiceLine.

---

## 1️⃣ Albums with Number of Tracks

```sql
SELECT al.Title AS Album, COUNT(t.TrackId) AS TrackCount
FROM Album al
JOIN Track t ON al.AlbumId = t.AlbumId
GROUP BY al.Title
ORDER BY TrackCount DESC;
```

**Result (Top albums by track count):**

| Album                                                | TrackCount |
|------------------------------------------------------|------------|
| Greatest Hits                                        | 57         |
| Minha Historia                                       | 34         |
| Unplugged                                            | 30         |
| Lost, Season 3                                       | 26         |
| The Office, Season 3                                 | 25         |
| Lost, Season 1                                       | 25         |
| My Way: The Best Of Frank Sinatra [Disc 1]           | 24         |
| Lost, Season 2                                       | 24         |
| Battlestar Galactica (Classic), Season 1             | 24         |
| Instant Karma: The Amnesty International Campaign... | 23         |
| ...                                                  | ...        |

📀 **Insight:** TV soundtracks and compilation albums often hold higher track counts than studio albums.

---

## 2️⃣ Customers and Their Support Representatives

```sql
SELECT c.FirstName || ' ' || c.LastName AS Customer,
       e.FirstName || ' ' || e.LastName AS SupportRep
FROM Customer c
JOIN Employee e ON c.SupportRepId = e.EmployeeId
ORDER BY SupportRep, Customer;
```

**Result Format:** *(Displayed in plain text output)*

```
# | Customer             | SupportRep
--+----------------------+------------------
1 | Frank Ralston        | Jane Peacock
2 | Helena Holý          | Jane Peacock
3 | Lucas Mancini        | Jane Peacock
...
```

👥 **Insight:** Support representatives are assigned to customers across different countries and regions. This join reveals customer-service relationships within the business.

---

## 3️⃣ Invoice Detail with Track and Artist Names

```sql
SELECT i.InvoiceId,
       a.Name AS Artist,
       t.Name AS Track,
       il.UnitPrice,
       il.Quantity
FROM Invoice i
JOIN InvoiceLine il ON i.InvoiceId = il.InvoiceId
JOIN Track t ON il.TrackId = t.TrackId
JOIN Album al ON t.AlbumId = al.AlbumId
JOIN Artist a ON al.ArtistId = a.ArtistId
ORDER BY i.InvoiceId
LIMIT 10;
```

**Result:**

| InvoiceId | Artist     | Track                | UnitPrice | Quantity |
|-----------|------------|----------------------|-----------|----------|
| 1         | Accept     | Balls to the Wall     | 0.99      | 1        |
| 1         | Accept     | Restless and Wild     | 0.99      | 1        |
| 2         | AC/DC      | Put The Finger On You | 0.99      | 1        |
| 2         | AC/DC      | Inject The Venom      | 0.99      | 1        |
| 2         | AC/DC      | Evil Walks            | 0.99      | 1        |
| 2         | AC/DC      | Breaking The Rules    | 0.99      | 1        |
| 3         | AC/DC      | Dog Eat Dog           | 0.99      | 1        |
| 3         | AC/DC      | Overdose              | 0.99      | 1        |
| 3         | Aerosmith  | Love In An Elevator   | 0.99      | 1        |
| 3         | Aerosmith  | Janie's Got A Gun     | 0.99      | 1        |

🧾 **Insight:** Each invoice includes track-level detail with associated artists, pricing, and quantity. Useful for granular billing and analysis.

---

📘 *All queries executed and verified in DBeaver against the Chinook SQLite sample database.*
