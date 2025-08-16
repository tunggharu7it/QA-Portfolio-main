# 🗃️ SQL Queries

## Overview

This folder contains sample SQL queries used for manual data validation, functional testing, and database structure analysis. All queries are written based on the [Chinook Sample Database](https://www.sqlitetutorial.net/sqlite-sample-database/) (SQLite), which simulates a digital media store with tracks, customers, invoices, and employees.

The examples aim to help QA engineers practice:

- Verifying returned results via SELECT statements  
- Validating table relationships through JOINs  
- Testing filtering, grouping, and sorting logic  
- Reviewing edge cases like NULLs and missing foreign keys

---

## Sample Database Used

- **Database Name:** Chinook.db  
- **Platform:** SQLite (used via DBeaver Sample Database tool)  
- **Source:** Built-in under `Help -> Create Sample Database -> SQLite` in [DBeaver](https://dbeaver.io/)  
- **Tables Available:**  
  `albums`, `artists`, `customers`, `employees`, `genres`, `invoices`, `invoice_items`, `media_types`, `playlists`, `playlist_track`, `tracks`

You can view the schema diagram and download the `.db` file from [SQLitetutorial.net](https://www.sqlitetutorial.net/sqlite-sample-database/)

---

## 📁 Available Query Files

- [SELECT_Queries.md](SELECT_Queries.md) – basic data retrieval, filtering, ordering  
- [JOIN_Queries.md](JOIN_Queries.md) – relational logic across multiple tables  
- [GROUP_BY_Queries.md](GROUP_BY_Queries.md) – aggregate results like total sales or customer counts  
- [INSERT_UPDATE_DELETE.md](INSERT_UPDATE_DELETE.md) – modifying data for edge-case testing  
- [Subquery_CTEs.md](Subquery_CTEs.md) – examples using nested logic and common table expressions  
- [Error_Scenarios.md](Error_Scenarios.md) – malformed queries, violations, constraint issues

---

## Usage Guidelines

- All queries are written for manual execution via [DBeaver](https://dbeaver.io/) *(or any SQLite-compatible tool)*  
- Schema assumptions are based on Chinook default structure  
- Comments inside each file explain expected output and testing goals  
- You can adapt queries to other databases by adjusting syntax and table names
