# 📊 GROUP_BY_Queries.md

Analytical queries using `GROUP BY` clauses in the Chinook sample database. Designed to extract insights across genres, customers, and artists.

---

## 1️⃣ Total Sales Per Genre

```sql
SELECT g.Name AS Genre, SUM(il.UnitPrice * il.Quantity) AS TotalSales
FROM Genre g
JOIN Track t ON g.GenreId = t.GenreId
JOIN InvoiceLine il ON t.TrackId = il.TrackId
GROUP BY g.Name
ORDER BY TotalSales DESC;
```

**Result:**

| Genre                | TotalSales |
|----------------------|------------|
| Rock                 | 826.65     |
| Latin                | 382.14     |
| Metal                | 261.36     |
| Alternative & Punk   | 241.56     |
| TV Shows             | 93.53      |
| Jazz                 | 79.20      |
| Blues                | 60.39      |
| Drama                | 57.71      |
| R&B/Soul             | 40.59      |
| Classical            | 40.59      |
| Sci Fi & Fantasy     | 39.80      |
| Reggae               | 29.70      |
| Pop                  | 27.72      |
| Soundtrack           | 19.80      |
| Comedy               | 17.91      |
| Hip Hop/Rap          | 16.83      |
| Bossa Nova           | 14.85      |
| Alternative          | 13.86      |
| World                | 12.87      |
| Science Fiction      | 11.94      |
| Heavy Metal          | 11.88      |
| Electronica/Dance    | 11.88      |
| Easy Listening       | 9.90       |
| Rock And Roll        | 5.94       |

📈 **Insight:** Rock dominates overall sales across genres, followed by Latin and Metal. Long tail includes niche styles like Bossa Nova, Sci Fi, and Easy Listening.

---

## 2️⃣ Number of Customers Per Country

```sql
SELECT Country, COUNT(*) AS CustomerCount
FROM Customer
GROUP BY Country
ORDER BY CustomerCount DESC;
```

**Result:**

| Country          | CustomerCount |
|------------------|----------------|
| USA              | 13             |
| Canada           | 8              |
| France           | 5              |
| Brazil           | 5              |
| Germany          | 4              |
| United Kingdom   | 3              |
| Portugal         | 2              |
| India            | 2              |
| Czech Republic   | 2              |
| Ukraine          | 1              |
| Sweden           | 1              |
| Spain            | 1              |
| Poland           | 1              |
| Norway           | 1              |
| Netherlands      | 1              |
| Italy            | 1              |
| Ireland          | 1              |
| Hungary          | 1              |
| Finland          | 1              |
| Denmark          | 1              |
| Chile            | 1              |
| Belgium          | 1              |
| Austria          | 1              |
| Australia        | 1              |
| Argentina        | 1              |

🌍 **Insight:** USA holds the largest share of customers, but the dataset reflects a globally distributed user base.

---

## 3️⃣ Top 5 Artists by Total Track Count

```sql
SELECT a.Name AS Artist, COUNT(t.TrackId) AS TrackCount
FROM Artist a
JOIN Album al ON a.ArtistId = al.ArtistId
JOIN Track t ON al.AlbumId = t.AlbumId
GROUP BY a.Name
ORDER BY TrackCount DESC
LIMIT 5;
```

**Result:**

| Artist         | TrackCount |
|----------------|------------|
| Iron Maiden    | 213        |
| U2             | 135        |
| Led Zeppelin   | 114        |
| Metallica      | 112        |
| Lost           | 92         |

🎸 **Insight:** Iron Maiden clearly leads in volume, followed by other prolific rock legends. This reflects deep discographies across multiple albums.

---

📘 *All queries validated in DBeaver using Chinook SQLite database.*

