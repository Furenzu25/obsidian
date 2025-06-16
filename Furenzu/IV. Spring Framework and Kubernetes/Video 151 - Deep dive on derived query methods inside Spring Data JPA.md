# 📚 Study Notes: **Derived Query Methods in Spring Data JPA**

---

## 🧠 What Are Derived Query Methods?

Derived query methods allow us to **query the database by just writing method names** in the repository interface — no need for SQL or JPQL. Spring Data JPA automatically translates these method names into SQL queries!

> ✨ Think of them as _"methods that query the database just by how they're named."_

---

## 🏗 Structure of a Derived Query Method

Each derived query method consists of **two parts**:

|Component|Purpose|
|---|---|
|**Introducer**|Specifies the action (e.g., `find`, `read`, `get`, `count`)|
|**Criteria**|Specifies the condition(s) using field names and keywords like `By`, `And`, `Or`|

👉 Spring uses the **`By`** keyword to identify where the introducer ends and the criteria begin.

---

### 🔹 Example:

java

	`findByLastNameAndEmail(String lastName, String email)`

- `find` = Introducer
    
- `ByLastNameAndEmail` = Criteria
    

Spring will convert this into:

sql

	`SELECT * FROM table WHERE last_name = ? AND email = ?`

---

## 🔍 Common Introducers

|Introducer|Purpose|
|---|---|
|`find`, `read`|Fetch data|
|`get`, `query`|Fetch data|
|`count`|Count rows instead of fetching records|
|`findDistinct`|Adds `DISTINCT` to the query|

✅ All of these behave similarly — they initiate a **SELECT** query.

---

## ⚙ Common Criteria Keywords

Here’s a table with commonly used criteria keywords and how they map to SQL:

|Method Keyword|SQL Equivalent|Example Method|
|---|---|---|
|`Is`, `Equals`|`=`|`findByFirstNameIs(String name)`|
|`Between`|`BETWEEN ... AND ...`|`findByStartDateBetween(start, end)`|
|`LessThan`, `GreaterThan`|`<`, `>`|`findByAgeLessThan(30)`|
|`Before`, `After`|For date columns: `<`, `>`|`findByStartDateAfter(date)`|
|`IsNull`, `IsNotNull`|`IS NULL`, `IS NOT NULL`|`findByEmailIsNull()`|
|`Like`, `NotLike`|`LIKE`, `NOT LIKE`|`findByNameLike("%John%")`|
|`StartingWith`|`LIKE 'abc%'`|`findByNameStartingWith("Jo")`|
|`EndingWith`|`LIKE '%xyz'`|`findByNameEndingWith("hn")`|
|`Containing`|`LIKE '%abc%'`|`findByNameContaining("oh")`|
|`OrderBy`|Adds `ORDER BY` clause|`findByAgeOrderByLastNameDesc()`|
|`In`, `NotIn`|`IN (...)`, `NOT IN (...)`|`findByIdIn(List<Integer> ids)`|
|`True`, `False`|Boolean comparisons|`findByActiveTrue()`|
|`IgnoreCase`|Ignores case sensitivity|`findByFirstNameIgnoreCase(String name)`|

---

## 🧠 Tips for Writing Derived Query Methods

✅ Always separate **introducer** and **criteria** using `By`  
✅ Use **`And`**, **`Or`** to combine multiple fields  
✅ Keep criteria limited to 2-3 fields to avoid long and unreadable method names  
✅ Use keywords like `IsNull`, `Between`, `Like`, `OrderBy`, etc., as needed

---

## 🧪 Real-World Examples

|Method Name|SQL Translation|
|---|---|
|`findDistinctByLastNameAndFirstName()`|`SELECT DISTINCT * FROM table WHERE last_name=? AND first_name=?`|
|`findByFirstNameEquals()`|`SELECT * FROM table WHERE first_name=?`|
|`findByStartDateBetween(start, end)`|`SELECT * FROM table WHERE start_date BETWEEN ? AND ?`|
|`findByStartDateAfter(Date date)`|`SELECT * FROM table WHERE start_date > ?`|
|`findByEmailIsNull()`|`SELECT * FROM table WHERE email IS NULL`|
|`findByNameLike("%John%")`|`SELECT * FROM table WHERE name LIKE ?`|
|`findByAgeOrderByLastNameDesc()`|`SELECT * FROM table WHERE age=? ORDER BY last_name DESC`|
|`findByIdIn(List<Integer> ids)`|`SELECT * FROM table WHERE id IN (?, ?, ?)`|
|`findByActiveTrue()`|`SELECT * FROM table WHERE active = TRUE`|
|`findByFirstNameIgnoreCase(String name)`|`SELECT * FROM table WHERE LOWER(first_name) = LOWER(?)`|

---

## 💡 Why Not Just One Big Method?

Spring follows the **Interface Segregation Principle** 🧩

- Don’t overload a single interface with all logic
    
- Keep responsibilities separated and manageable
    
- Avoid method names that are too long and hard to maintain
    

---

## 🚧 When NOT to Use Derived Queries

Sometimes derived methods aren't enough (e.g., complex joins, dynamic filters, subqueries). In such cases, you can use:

- ✅ **JPQL Queries**
    
- ✅ **Native SQL**
    
- ✅ **@Query Annotation**
    
- ✅ **Specifications / Criteria API**
    

We’ll explore those alternatives in future lectures.

---

## 🎯 Summary

- 🧠 Spring Data JPA lets you write methods that automatically convert to SQL
    
- ✍ Method names must follow a **specific structure**
    
- 🪄 Spring parses your method and generates the corresponding SQL
    
- 🤯 Tons of keywords are supported: `Between`, `Like`, `OrderBy`, `IgnoreCase`, etc.
    
- 🚀 Helps avoid boilerplate SQL for most common use cases
    
- 📌 Stick to 2–3 criteria fields max for clarity and maintainability
    

---

## ✅ Your Next Steps

Now that you're familiar with **derived query methods**, you'll be ready to:

- Build expressive methods in your repositories
    
- Avoid SQL entirely for many CRUD and filter operations
    
- Write cleaner, more maintainable backend code
    

📘 **Coming Up Next:** Custom queries using `@Query`, JPQL, and dynamic filtering.

---

🔚 **End of Notes**  
Happy querying! 🧑‍💻✨ Let Spring write the SQL while you focus on business logic.