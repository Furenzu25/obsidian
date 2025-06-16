# 📘 Study Notes: Introduction to JDBC & Why Spring JDBC Is Better

---

## 🚀 Objective

We now have an **internal H2 database** set up in our Eazy School web application.  
Our next goal: **Store contact message data** 📨 submitted through the **Contact Page**.

To do this, we need a **Java-based database interaction framework** that helps:

- Connect to the database
    
- Run `INSERT`, `SELECT`, `UPDATE`, `DELETE` queries
    

---

## 🧰 Available Java Database Frameworks

There are many frameworks for database interaction:

|🛠 Framework|💬 Description|
|---|---|
|**Core JDBC**|Built-in Java API|
|**Spring JDBC**|Simplifies JDBC|
|**Hibernate**|ORM (Object Relational Mapping)|
|**Spring Data JPA**|High-level abstraction using Hibernate|
|**MyBatis**|SQL-focused, flexible mapping|

> ⚠️ Many developers get **confused** over which to use.  
> This course walks you **step by step**—from **Core JDBC → Spring JDBC → Hibernate/Spring Data JPA** with full clarity.

---

## 🔄 Core JDBC (Java Database Connectivity)

### 📌 Definition:

JDBC is a **Java API** that allows Java applications to **communicate with relational databases** using SQL.

### 🔧 Common Steps in JDBC:

1. **Load the Driver Class**  
    E.g., for MySQL: `Class.forName("com.mysql.jdbc.Driver");`
    
2. **Establish Connection**  
    Use `DriverManager.getConnection(url, user, password)`
    
3. **Prepare Statement**  
    E.g., `PreparedStatement pstmt = conn.prepareStatement("SELECT * FROM table WHERE id = ?");`
    
4. **Execute Query**  
    Use `pstmt.executeQuery()` or `executeUpdate()`
    
5. **Process ResultSet**  
    Retrieve data using `rs.getString()`, `rs.getInt()`, etc.
    
6. **Close Resources**  
    Always close `ResultSet`, `PreparedStatement`, and `Connection` in a `finally` block.
    

---

## ❌ Drawbacks of JDBC

|⚠️ Issue|🧾 Explanation|
|---|---|
|**Verbose code**|Too many steps for simple queries|
|**Manual exception handling**|Must handle checked exceptions like `SQLException`|
|**Resource management**|Developer must close all connections, or it causes memory leaks|
|**Hardcoded SQL**|SQL queries are embedded as strings|
|**Database dependent**|If switching DBs (e.g., MySQL → Oracle), query keywords may break|
|**No abstraction**|Entire logic is written manually every time|

---

## 📝 JDBC Code Sample (Traditional Way)

java

	`Class.forName("com.mysql.jdbc.Driver"); Connection conn = DriverManager.getConnection("jdbc:mysql://...", "user", "pass"); PreparedStatement stmt = conn.prepareStatement("SELECT * FROM contact_msg WHERE contact_id = ?"); stmt.setInt(1, contactId); ResultSet rs = stmt.executeQuery(); while (rs.next()) {    // Process result } rs.close(); stmt.close(); conn.close();`

> 😵‍💫 Every query requires **tons of boilerplate code**, exception handling, and resource cleanup.

---

## 💡 JDBC: Foundation for All Modern Frameworks

Even today:

- **Hibernate**
    
- **Spring Data JPA**
    
- **MyBatis**
    

...all internally **use JDBC** under the hood!

> 🔍 **JDBC is the backbone**, but we now use frameworks to **simplify development** and **reduce boilerplate code**.

---

## ✨ Enter: **Spring JDBC**

Spring Team introduced **Spring JDBC** to:

- Automate and simplify the boilerplate tasks of JDBC
    
- Provide better **abstraction** and **error handling**
    
- Manage resources (connections, statements) automatically
    
- Focus more on **writing SQL**, not infrastructure code
    

> ✅ In Spring JDBC:
> 
> - No need to manually manage connections
>     
> - Queries are easier to write and read
>     
> - Exceptions are handled using Spring’s `DataAccessException` hierarchy
>     

---

## 🧠 Key Insight

We **won’t be using Core JDBC anymore** in this course.  
👉 Instead, we’ll use **Spring JDBC** moving forward to interact with the H2 database.

---

## 🔜 What’s Next?

In the **next lecture**, we'll:

- Implement **Spring JDBC**
    
- Use it to **store contact form data** into the H2 database
    
- Explore how Spring simplifies all those tedious steps we saw with JDBC
    

---

## ✅ Final Takeaways

|💡 Concept|📌 Insight|
|---|---|
|JDBC is foundational|Still used under the hood in most modern frameworks|
|Don’t ignore JDBC|Understand it before moving on to higher abstractions|
|JDBC has limitations|Verbose, prone to errors, tight DB coupling|
|Spring JDBC is better|Cleaner, safer, and easier to use|

---

🔁 This transition from JDBC → Spring JDBC → Hibernate/Spring Data JPA will give you a **solid understanding** of database access in Java web apps!

🎯 Let’s move forward and apply Spring JDBC in the Eazy School web application.

See you in the next lecture! 👋