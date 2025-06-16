# 📘 Study Notes: Introduction to Spring JDBC

_(A Simpler Way to Talk to Databases in Spring Boot)_

---

## 🧠 What We Already Know:

In the last lecture, we discussed how **Core Java JDBC** is:

- 📜 Verbose (too much boilerplate code)
    
- ❌ Error-prone (manual connection handling, exception management)
    
- 💀 Heavy (developer must do everything: connect, execute, handle exceptions, close resources)
    

This made working with databases a **tedious and risky job** for developers.

---

## 🌱 Enter: Spring JDBC Framework

To solve the problems of JDBC, the **Spring Team** introduced **Spring JDBC**.

### ✅ What Spring JDBC Does:

|🎯 Feature|💬 Explanation|
|---|---|
|🧹 Reduces boilerplate code|No more writing repeated connection/closing code|
|🔒 Handles exceptions automatically|You don't need try-catch-finally for every query|
|🔗 Manages connections internally|Spring opens & closes them for you|
|📊 Allows focus on business logic|You focus only on **what** to query, not **how**|

Spring JDBC shifts the **responsibility** from the **developer ➝ framework**, freeing you to write cleaner, clearer logic. ✨

---

## 📦 Getting Started

To use Spring JDBC in your Spring Boot app:

### 📌 Step 1: Add Dependency

Add the following to `pom.xml`:

xml

	`<dependency>   <groupId>org.springframework.boot</groupId>   <artifactId>spring-boot-starter-jdbc</artifactId> </dependency>`

This gives you access to **Spring JDBC Templates** and all supporting features.

---

## 🧰 The Magic Behind Spring JDBC: Templates

Spring JDBC introduces **Templates**—predefined tools that automate repetitive tasks like connection handling, query execution, and cleanup.

### 🏗️ Two Common Templates:

|Template|Use Case|
|---|---|
|`JdbcTemplate`|The core class, uses `?` placeholders like JDBC|
|`NamedParameterJdbcTemplate`|Lets you use named placeholders like `:id`, `:name` for clarity|

🔁 `NamedParameterJdbcTemplate` is just a **wrapper** around `JdbcTemplate`, built for **better readability** and **less confusion**.

---

## 🤹‍♂️ Example: SQL Parameters

|Template Type|SQL Format Example|
|---|---|
|`JdbcTemplate`|`"SELECT * FROM user WHERE id = ?"`|
|`NamedParameterJdbcTemplate`|`"SELECT * FROM user WHERE id = :userId"`|

> 🧠 The second one is easier to read and maintain—especially with many parameters.

---

## 📊 Spring JDBC vs Developer Tasks: Who Does What?

|🛠 Action|✅ Spring JDBC|🧑‍💻 Developer|
|---|---|---|
|Define DB credentials|❌|✅ _(1 time only in `application.properties`)_|
|Open DB connection|✅|❌|
|Prepare SQL statement|❌|✅|
|Declare and bind parameters|❌|✅|
|Execute query|✅|❌|
|Handle `ResultSet` iteration (loop)|✅|✅ _(only logic to map to objects)_|
|Handle exceptions|✅|❌|
|Commit/Rollback/Close connections|✅|❌|

🎯 **Result**: Developers only focus on **business logic**, not infrastructure setup. Spring JDBC handles the rest!

---

## 🧠 Why You Should Still Learn Spring JDBC

Even though there are **more modern frameworks** like:

- 🔸 Spring Data JPA
    
- 🔸 Hibernate
    

...many **small-scale projects or legacy systems** still use **Spring JDBC**.

> 💼 In interviews or the real world, your flexibility as a developer depends on understanding **all layers**, not just the newest one.

---

## 🧾 Summary: Why Use Spring JDBC?

✅ Less Code  
✅ Fewer Bugs  
✅ Easier Maintenance  
✅ Clearer SQL (with `NamedParameterJdbcTemplate`)  
✅ Still widely used in small & mid-scale Java projects

---

## 🔜 What’s Next?

In the next lecture, we’ll explore:

- How to actually use **JdbcTemplate** in a real Spring Boot web application.
    
- How to query and save data into the **H2 database** using these templates.
    

Let’s start coding with templates soon! 👨‍💻👩‍💻

---

Thanks for sticking through this session!  
See you in the next lecture. 😊👋