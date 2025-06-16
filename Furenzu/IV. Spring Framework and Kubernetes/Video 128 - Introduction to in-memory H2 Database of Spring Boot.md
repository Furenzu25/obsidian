# 🏫 Study Notes: Introduction to H2 Database in Spring Boot (Eazy School Project)

---

## 📌 Current Progress Recap

So far in our **Eazy School Web Application**, we’ve already:

- ✅ Used **Spring Core**, **Spring AOP**, and **Spring MVC**
    
- ✅ Built the app following the **MVC architecture**
    
- ✅ Secured it using **Spring Security**
    

But to make the application **fully dynamic**, we now need to introduce **a database**. Why?

> A dynamic web app needs persistent storage — for storing, retrieving, and managing data for end users.

---

## 🗄️ Why Introduce a Database?

- Web applications typically rely on databases like **MySQL**, **PostgreSQL**, or **Oracle** to persist data.
    
- Without a database, there's no reliable way to maintain data between sessions or users.
    

But instead of jumping directly into a production-grade database, we will first use:

---

## 🚀 Introducing the H2 Database (In-Memory DB)

### 💡 What is H2?

- 🔌 **Embedded, lightweight, and in-memory** database
    
- 🧠 All data is stored **in RAM** (i.e., it vanishes once the app stops!)
    
- 📦 Comes bundled via **Spring Boot starter dependency**
    
- 🔧 Great for: **Testing, Demos, Learning, Prototyping**
    

### 🧰 Why Use H2 First?

|Pros of H2|Comments|
|---|---|
|No installation needed|Bundled inside your app|
|Works immediately after adding dependency|Zero setup|
|Ideal for quick demos and mockups|Not for production use|
|Accessible via web console|Query your DB through a browser|

---

## ⚙️ How to Use H2 in Your App

### 📦 Step 1: Add the Dependency

In your `pom.xml`:

	xml

	<dependency>   <groupId>com.h2database</groupId>   <artifactId>h2</artifactId> </dependency>

Just like the embedded Tomcat server, Spring Boot will recognize H2 and auto-configure it.

---

### 🗂️ Step 2: Define SQL Scripts

To make sure your database **has tables and data at startup**, create these two files in `src/main/resources/`:

1. **`schema.sql`**  
    📄 Contains `CREATE TABLE` and schema definitions
    
2. **`data.sql`**  
    📄 Contains `INSERT INTO` statements to preload data
    

✅ These scripts are automatically run by Spring Boot every time you restart the application.

⛔ Remember: Since H2 is in-memory, all data is **wiped out** upon app shutdown. These scripts make your app _reproducible_ every time it runs.

---

### 🌐 Step 3: Use the H2 Console

Once H2 is in use, Spring Boot exposes a **web-based H2 Console** at:

	bash

	http://localhost:8080/h2-console

- 👤 **Default username**: `sa`
    
- 🔐 **Default password**: _(empty)_
    

> From here, you can view tables, run queries, inspect data — all from a browser! 🧑‍💻

---

### ✏️ Optional: Customize H2 Console Path

If you don’t want to use `/h2-console`:

In `application.properties`:

	properties
	
	spring.h2.console.path=/custom-path

This helps in securing and customizing access to the console.

---

## 🚧 Limitations of H2

|Limitation|Why it matters|
|---|---|
|Data isn’t persistent|Data vanishes on app shutdown|
|Not suitable for production|No security, not scalable|
|Manual schema/data management|Needs setup on every restart|

---

## 💡 When Should You Use H2?

- For **demos**, **unit testing**, and **early dev stages**
    
- When you don’t want the hassle of setting up a full DB
    
- For **quick microservices** or **prototype builds**
    

---

## 🧭 What’s Next?

In the **next lecture**, we will:

1. ✅ Add the H2 dependency
    
2. ✅ Create `schema.sql` and `data.sql`
    
3. ✅ Launch and access the H2 console
    
4. ✅ Interact with the database from the Eazy School app
    

---

## 🧠 Summary

|Concept|Explanation|
|---|---|
|H2 Database|Embedded, in-memory database for Spring Boot|
|Use Case|Demos, prototyping, and learning|
|Schema/Data Scripts|`schema.sql` and `data.sql` for DB setup|
|H2 Console|Web-based UI for querying DB|
|Real DB Later|We’ll eventually move to **MySQL** for production|

---

🎉 You now understand why and how to use **H2 database** in your Spring Boot application! It’s a powerful tool to speed up development and testing. See you in the next lecture for the demo! 🧪💻  