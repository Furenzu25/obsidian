# 📚 Study Notes: Implementing H2 Database in Eazy School Web App (Spring Boot)

---

## 🛠️ Project Setup: `example_32`

We are working with a new Spring Boot Maven project named `example_32` where we:

- Integrate **H2 in-memory database** 🔌
    
- Store **contact messages** submitted via the **Contact Page** 📨
    
- Learn **Spring JDBC** to interact with the database
    
- Configure **Spring Security** to permit access to H2 console
    

---

## 🔌 Step 1: Add H2 Dependency

In `pom.xml`, add:

xml

Copy code

`<dependency>   <groupId>com.h2database</groupId>   <artifactId>h2</artifactId>   <scope>runtime</scope> <!-- Optional but recommended --> </dependency>`

> ✅ The `runtime` scope tells Spring Boot that this dependency is needed **only at runtime**, not during compilation.

---

## 🧱 Step 2: Create Table with `schema.sql`

Place this file in `src/main/resources/` (same location as `application.properties`):

### 📄 `schema.sql`:

Creates a `contact_msg` table:

- `contact_id` (Primary Key)
    
- `name`, `mobile_num`, `email`, `subject`, `message`
    
- `status` (to track message resolution: _open_ ➡ _closed_)
    
- Common audit fields:
    
    - `created_at`, `created_by`
        
    - `updated_at`, `updated_by`
        

> ✅ We will follow this **audit column standard** for all future tables.

---

## ⚙️ Step 3: Configure `application.properties`

Set connection and console options for H2:

properties

Copy code

`# JDBC config spring.datasource.url=jdbc:h2:mem:eazyschooldb spring.datasource.driver-class-name=org.h2.Driver spring.datasource.username=sa spring.datasource.password=  # Hibernate spring.jpa.database-platform=org.hibernate.dialect.H2Dialect spring.jpa.hibernate.ddl-auto=update spring.jpa.show-sql=true  # Enable H2 console spring.h2.console.enabled=true spring.h2.console.path=/h2-console`

> 💡 `ddl-auto=update`: Prevents Hibernate from dropping existing tables — but not really relevant for H2 as it resets on each run.

---

## 🌍 Step 4: Run & Verify H2 Console

### 1. Build & Run App:

- Start the server in **debug mode**
    
- Spring Boot auto-configures H2 & logs:
    
    css
    
    Copy code
    
    `H2 console available at /h2-console`
    

### 2. Access in Browser:

Go to: `http://localhost:8080/h2-console`

Login with:

- **JDBC URL**: Same as in `application.properties`
    
- **Username**: `sa`
    
- **Password**: _(leave blank)_
    

---

## 🛡️ Step 5: Configure Spring Security

By default, Spring Security **protects everything**, including `/h2-console`.

### ✔️ Permit All Access to H2 Console

In `ProjectSecurityConfig.java`, add:

java

Copy code

`http.authorizeHttpRequests(auth ->      auth         .requestMatchers(PathRequest.toH2Console()).permitAll() );`

> 🚫 Do **not** hardcode the H2 path. Use `PathRequest.toH2Console()` instead.

### ✔️ Disable CSRF for H2

Still in `ProjectSecurityConfig.java`:

java

Copy code

`http.csrf(csrf ->      csrf.ignoringRequestMatchers(PathRequest.toH2Console()) );`

### ✔️ Allow Frames (H2 Console uses `<frame>` tags)

Also add:

java

Copy code

`http.headers(headers ->      headers.frameOptions().disable() );`

---

## ✅ Final Testing

1. Access `/h2-console` without being blocked
    
2. Ensure JDBC URL, driver, and credentials match your config
    
3. Hit **Connect** to open H2 console
    
4. Run:
    

sql

Copy code

`SELECT * FROM contact_msg;`

> You should see an **empty table**, but with columns correctly generated from `schema.sql`.

---

## 🎯 Summary: Key Takeaways

|🔑 Topic|✅ Implementation|
|---|---|
|Add H2 Database|Add to `pom.xml`|
|Define table schema|`schema.sql`|
|DB connection config|`application.properties`|
|Enable web console|`/h2-console`|
|Spring Security adjustments|Permit access, disable CSRF and frames|
|Web-accessible DB UI|Query via browser|
|Reusability|Demo/Test only — _not for production_|

---

## 🧠 Interview-Ready Insights

- **Why use H2?**  
    ➤ For demos, learning, and fast microservice development
    
- **What’s the biggest benefit?**  
    ➤ Zero setup, no MySQL or Oracle required
    
- **Production usage?**  
    ❌ Not suitable — data is ephemeral and unsecured
    

---

## 🔄 What's Next?

In the upcoming lecture:

- We'll save actual data into the `contact_msg` table using **Spring JDBC**
    
- Eventually, we’ll **replace H2 with MySQL** for a production-grade backend
    

---

📌 **Remember**: H2 is an amazing **quick-start tool**. Use it to focus on core business logic without getting bogged down by database setup.

---

👍 That’s it for now. You're now fully equipped to set up and use the H2 database in your Spring Boot app. Great job!