# 📘 Study Notes: Enhancing Web App with Spring JDBC & JdbcTemplate

---

## 🎯 Goal of This Module

We enhanced our **Eazy School Web Application** to fetch and display **holiday data from an H2 database**, instead of using hardcoded values.  
This is done using **Spring JDBC’s JdbcTemplate** — a powerful helper class for working with relational databases.

---

## 💾 Previous Behavior (Before Enhancement)

- ❌ Holidays were hardcoded directly in the `HolidaysController`.
    
- 📤 Manually created objects were sent to the frontend UI.
    

---

## ✅ New Behavior (After Enhancement)

- ✅ Holidays are now **stored in the H2 database**.
    
- ✅ They are fetched dynamically using **JdbcTemplate** and **RowMapper**.
    
- ✅ The web application now follows a **more scalable and database-driven approach**.
    

---

## 🧱 Step-by-Step Breakdown

### 1️⃣ Create Table & Insert Data Automatically

- **schema.sql**: Used to create the `holidays` table with fields:
    
    - `day`, `reason`, `type`, `created_at`, `created_by`, `updated_at`, `updated_by`
        
- **data.sql**: Populated sample holiday records like:
    
    - `Martin Luther King Junior Day`, `Independence Day`, etc.
        

⏳ When the Spring Boot app starts, it automatically:

- ⬆️ Executes `schema.sql` to create the table
    
- 📝 Runs `data.sql` to insert initial records
    

---

### 2️⃣ Update the Model (Pojo Class)

📄 `Holiday.java` (inside `model` package):

- ✔️ Extended from `BaseEntity` to inherit `created_at`, `created_by`, etc.
    
- ✔️ Removed `final` from fields to allow Spring JDBC to update them via reflection.
    
- ❗ Final fields break Spring’s `RowMapper`, which instantiates objects and sets fields afterward.
    

---

### 3️⃣ Create the Repository Layer

📦 `HolidaysRepository.java` (with `@Repository` annotation):

- 🧠 Uses `JdbcTemplate` with **constructor-based dependency injection**
    
- 💡 Defines method `findAllHolidays()`:
    
    java

	    `String sql = "SELECT * FROM holidays"; return jdbcTemplate.query(sql, BeanPropertyRowMapper.newInstance(Holiday.class));`
    

### 💡 Tip: BeanPropertyRowMapper

- ✅ Automatically maps column names to POJO fields.
    
- ❌ You don’t need a custom RowMapper if the names **match**.
    
- ✅ Ignores underscores and uses camel case mapping (e.g., `created_at` → `createdAt`).
    

---

### 4️⃣ Modify Controller to Use Repository

📄 `HolidaysController.java`:

- ⛔ Removed all hardcoded holiday logic.
    
- ✅ Injected `HolidaysRepository` using `@Autowired`.
    
- ✅ Called `findAllHolidays()` to fetch from DB.
    

📝 Skipped `Service` layer intentionally — since no business logic was involved.

---

## 🧪 Verifying Results

1. 🔎 Open the H2 Console
    
2. 🧾 Confirm holidays table has records from `data.sql`
    
3. 🌐 Navigate to the Holidays page on the website
    
4. 🟢 Holidays should appear dynamically from the database
    

✔️ Confirmed changes using a quick edit:

- Removed the word “Junior” from one entry in `data.sql`
    
- After a rebuild, the UI reflected the updated holiday name 🎉
    

---

## 🛠️ Bonus Tips and Deep Dives

### 🧩 JdbcTemplate vs NamedParameterJdbcTemplate

|Feature|JdbcTemplate 🟠|NamedParameterJdbcTemplate 🟢|
|---|---|---|
|Placeholder syntax|Uses `?`|Uses `:name`|
|Readability|❌ Hard to track multiple `?`|✅ Easier to map parameters|
|Recommended for|Simple queries|More complex or dynamic queries|

**Example:**

java

	`String sql = "SELECT COUNT(*) FROM person WHERE first_name = :first_name"; MapSqlParameterSource param = new MapSqlParameterSource("first_name", "Joe"); namedParameterJdbcTemplate.queryForObject(sql, param, Integer.class);`

---

### 🛡️ JdbcTemplate Tips

- 🛠️ You **don’t need to define DataSource/JdbcTemplate beans manually** in Spring Boot.
    
- 🎛️ Customization via `application.properties`:
    
    properties
    
	    `spring.jdbc.template.max-rows=500`
    
- ✅ Thread-safe: one instance can be reused safely.
    
- 👨‍💻 Focus shifts to:
    
    - Writing SQL
        
    - Setting parameters
        
    - Mapping result data to POJOs
        

---

## 🔚 Summary

✔️ Spring JDBC + JdbcTemplate significantly reduces boilerplate  
✔️ The database-driven design is now implemented for the Holidays page  
✔️ Developers focus on **business logic**, not connection handling or resource cleanup  
✔️ You learned how to:

- Use schema.sql/data.sql
    
- Define repository methods
    
- Use `BeanPropertyRowMapper`
    
- Differentiate between JdbcTemplate and NamedParameterJdbcTemplate
    

---

## 🔜 What’s Next?

🌟 While Spring JDBC is great for small apps, most **modern enterprise projects use**:

- 🔧 **Spring Data JPA**
    
- 🏛️ **Hibernate**
    

These frameworks offer:

- 🧠 Automatic query generation
    
- ❌ No need to write raw SQL
    
- ✨ Even more abstraction and power
    

We'll dive into **Spring Data JPA** next 🚀