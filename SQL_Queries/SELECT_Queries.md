# 🔎 SELECT Queries

This file contains basic SELECT statements used for data retrieval and validation. Queries reflect real output from a SQLite database.

---

## 1. Retrieve all customers

```sql
SELECT * FROM Customer;
```

**Result (truncated preview):**

| CustomerId | FirstName | LastName    | Company                                   | City        | Country        | Email                        |
|------------|-----------|-------------|-------------------------------------------|-------------|----------------|------------------------------|
| 1          | Luís      | Gonçalves   | Embraer - Empresa Brasileira de Aeronáutica S.A. | São José dos Campos | Brazil         | luisg@embraer.com.br        |
| 2          | Leonie    | Köhler      |                                           | Stuttgart   | Germany        | leonekohler@surfeu.de        |
| 3          | François  | Tremblay    |                                           | Montréal    | Canada         | ftremblay@gmail.com          |
| ...        | ...       | ...         |                                           | ...         | ...            | ...                          |

📌 _Note: Full result set includes 59 customers._

---

## 2. Get customer emails from Canada only

```sql
SELECT FirstName, LastName, Email
FROM Customer
WHERE Country = 'Canada';
```

**Result:**

| FirstName | LastName  | Email                     |
|-----------|-----------|---------------------------|
| François  | Tremblay  | ftremblay@gmail.com       |
| Mark      | Philips   | mphilips12@shaw.ca        |
| Jennifer  | Peterson  | jenniferp@rogers.ca       |
| Robert    | Brown     | robbrown@shaw.ca          |
| Edward    | Francis   | edfrancis@yachoo.ca       |
| Martha    | Silk      | marthasilk@gmail.com      |
| Aaron     | Mitchell  | aaronmitchell@yahoo.ca    |
| Ellie     | Sullivan  | ellie.sullivan@shaw.ca    |

🎯 Great for verifying `WHERE` clause filtering and email formatting.

---

## 3. Order tracks by duration

```sql
SELECT Name, Milliseconds
FROM Track
ORDER BY Milliseconds DESC;
```

**Result (top 10):**

| Name                            | Milliseconds |
|---------------------------------|--------------|
| Occupation / Precipice          | 5286953      |
| Through a Looking Glass         | 5088838      |
| Greetings from Earth, Pt. 1     | 2960293      |
| The Man With Nine Lives         | 2956998      |
| Battlestar Galactica, Pt. 2     | 2956081      |
| Battlestar Galactica, Pt. 1     | 2952702      |
| Murder On the Rising Star       | 2935894      |
| Battlestar Galactica, Pt. 3     | 2927802      |
| Take the Celestra               | 2927677      |
| Fire In Space                   | 2926593      |

🔁 Confirms correct descending sort and proper numeric handling.

---

📘 *All queries executed and verified in DBeaver against the Chinook SQLite sample database.*