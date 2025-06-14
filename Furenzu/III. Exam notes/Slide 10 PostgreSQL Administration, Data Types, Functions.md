# 📘 PostgreSQL Administration, Data Types, Operators & Functions — Study Notes (DB-102)

---

## 🗂️ Agenda

1. Overview of PostgreSQL
    
2. Command-Line Administration
    
3. Graphical Tool (pgAdmin)
    
4. Data Types, Operators & Functions
    

---

## 🧾 1. PostgreSQL Overview

- **Origin**: Developed at UC Berkeley by Prof. Michael Stonebraker as a successor to Ingres (“Post-Ingres”).
    
- **History**: Started in 1986, version 1.0 released in 1996. Version 0.01 released on 1995.
    
- **Sponsored**: U.S. Military.
    

---

## 🖥️ 2. Command-Line Administration

### ⚙️ Authorization & Access

- **Unix**: Use `sudo -u postgres -s` to switch to the `postgres` user.
    
- **Windows**: Use `runas /user:postgres "cmd /k cd /d C:\Users\postgres"`.
    

### 📦 Create/Drop Database
	
	bash
	
`# Unix createdb mydb dropdb mydb  # Windows createdb mydb dropdb mydb`

### 📁 Backup & Restore

- **Backup**:
    
    bash
	
    `pg_dump mydb > mydb.sql pg_dumpall > all_databases.sql pg_dump -Fc mydb > mydb.bin`
    
- **Restore**:
    
    bash
	
    `psql mydb < mydb.sql pg_restore -d mydb mydb.bin`
    

### 👤 Create/Drop Users
	
	bash
	
`createuser newuser dropuser newuser`

### 🧾 SQL Execution from Files
	
	bash
	
`psql -U user -d dbname -f script.sql psql -U user -d dbname -c "QUERY" -o output.txt`

### 📄 CSV Import/Export
	
	sql
	
`\COPY table FROM 'file.csv' DELIMITER ',' CSV HEADER; \COPY (SELECT ...) TO 'output.csv' DELIMITER ',' CSV HEADER;`

---

## 🧑‍💻 3. Interactive Terminal (`psql`)

### 🔧 Meta Commands

|Command|Description|
|---|---|
|`\list` or `\l`|List databases|
|`\du`|List users|
|`\d`|List tables|
|`\dt`, `\dv`, `\di`|List tables, views, indexes|
|`\c dbname`|Connect to a database|
|`\o file.txt`|Redirect output to file|
|`\i script.sql`|Execute SQL file|
|`\x`|Toggle expanded display|
|`\q`|Quit|

---

## 🛡️ 4. SQL Security

### 🔐 Privileges

|Type|Description|
|---|---|
|`SELECT`, `INSERT`, `UPDATE`, `DELETE`|Table-level actions|
|`GRANT`, `REVOKE`|Assign/revoke rights|
|`ALTER SYSTEM`|Configuration access|

---

## 📊 5. Query Planning & Optimization

### 🧠 `EXPLAIN`, `EXPLAIN ANALYZE`

- Shows execution plan.
    
- Helps understand performance.
    
- Use `ANALYZE` for actual execution time.
    

---

## 💽 6. Disk Usage

Query approximate disk usage:
	
	sql
	
`SELECT relname, relpages FROM pg_class ORDER BY relpages DESC;`

---

## 🖼️ 7. pgAdmin: GUI Tool

- Create servers, browse databases.
    
- Launch query tool, view EXPLAIN plans.
    
- Schedule jobs via **pgAgent**.
    
- Edit data visually.
    

---

## 📈 8. PostgreSQL Data Types

### 🔢 Numeric

- `SMALLINT`, `INTEGER`, `BIGINT`
    
- `DECIMAL`, `NUMERIC` – exact
    
- `REAL`, `DOUBLE PRECISION`, `FLOAT` – inexact
    
- `MONEY` – locale-dependent, rounded to 2 decimal places
    

### 🔤 Character

- `VARCHAR(n)`, `CHAR(n)`, `TEXT`
    

### 🔣 String Functions

- `CONCAT_WS`, `UPPER`, `LOWER`, `INITCAP`, `TRIM`, `MD5`, `REPLACE`, etc.
    
- Regex: `REGEXP_MATCHES`, `REGEXP_REPLACE`
    

### 📅 Date/Time

- `DATE`, `TIME`, `TIMESTAMP`, `INTERVAL`
    
- `AGE`, `EXTRACT`, `DATE_PART`, `DATE_TRUNC`
    
- `CURRENT_DATE`, `CURRENT_TIME`, etc.
    

---

## 📦 9. Arrays

### ✅ Features:

- 1D & Multi-Dimensional
    
- Use `[]` notation, `ARRAY_TO_STRING`, `STRING_TO_ARRAY`
    
- Functions: `UNNEST`, `ARRAY_LENGTH`
    
- Operators: `@>`, `<@`, `||`, `=`, `<>`
    

---

## 📐 10. Range Types

### 📊 Types:

- `INT4RANGE`, `NUMRANGE`, `TSRANGE`, `TSTZRANGE`, `DATERANGE`
    

### 🔍 Operators:

- Containment: `@>`, `<@`
    
- Comparison: `<<`, `>>`, `&<`, `&>`, `-|-`, `+`, `-`, `*`
    
- Metadata: `LOWER`, `UPPER`, `ISEMPTY`, `LOWER_INC`, etc.
    

---

## 🔢 11. Enumerated Types (ENUM)
	
	sql
	
`CREATE TYPE suit AS ENUM ('Clubs', 'Spades', 'Hearts', 'Diamonds');`

- Enforce valid values.
    
- Preserves ordering.
    
- Use `\dT+` to inspect.
    

---

## 🧭 12. Advanced Data Types

### 📐 Geometric

- `point`, `line`, `polygon`, `circle`
    

### 🌐 Network

- `cidr`, `inet`, `macaddr`
    

### 🧮 Bit Strings

- `BIT(n)`, `BIT VARYING(n)`
    

### 🔍 Full-Text Search

- `TSVECTOR`, `TSQUERY`, `@@`, `TO_TSVECTOR`, `TO_TSQUERY`
    

---

## 🧾 13. UUID

- Use `uuid-ossp` or `pgcrypto` module.
    
- Ideal for:
    
    - Partitioned tables
        
    - Merged schemas
        
- `SERIAL` vs `UUID`:
    
    |Category|SERIAL|UUID|
    |---|---|---|
    |Performance|Faster|Slower|
    |Uniqueness|Manual control|Guaranteed|
    |Merge safe|No|Yes|
    

---

## 🧱 14. XML

### ✅ XML Support:

- Validate: `XMLEXISTS`, `XPATH`
    
- Convert: `TABLE_TO_XML`, `QUERY_TO_XML`
    
- Storage Type: `XML`
    

---

## 🧰 15. JSON & JSONB

### 🧾 JSON Syntax:
	
	json
	
`{   "student_number": 123,   "firstname": "Jon",   "lastname": "Snow" }`

### 🛠️ Operators:

- `->`, `->>` – access fields
    
- `#>`, `#>>` – access nested
    
- `@>`, `<@` – containment
    
- `JSONB_SET()`, `#-` – modify/delete
    

### 🧪 Functions:

- `JSON_POPULATE_RECORD`, `row_to_json`, `array_to_json`
    

### ⚙️ Indexing:

- GIN for containment queries
    

---

## 📝 Exercises (Summarized)

1. Create users, databases, tables.
    
2. Grant/verify privileges.
    
3. Use `EXPLAIN`, create indexes.
    
4. Work with different data types: strings, numbers, dates, arrays, JSON, etc.
    

---

## 🧠 Review Summary

|Topic|Key Points|
|---|---|
|Command-line Admin|`createdb`, `pg_dump`, `psql`, `\COPY`, etc.|
|pgAdmin|GUI alternative for managing PostgreSQL|
|Data Types|NUMERIC, TEXT, DATE, MONEY, BOOLEAN, ARRAY, etc.|
|JSON/XML|Complex/nested data support|
|Optimization|Use `EXPLAIN`, index fields, analyze disk use|
|Full Text Search|Use `@@`, `TO_TSQUERY()`|
|Range Types|Simplifies intervals/conditions|