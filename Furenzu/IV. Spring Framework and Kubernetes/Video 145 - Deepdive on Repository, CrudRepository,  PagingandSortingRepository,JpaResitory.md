# 📘 Study Notes: Core Interfaces in Spring Data & Introduction to `JpaRepository`

---

## 🚀 Why These Interfaces Matter

Spring Data lets developers **skip writing SQL** and **avoid boilerplate code**. Instead, Spring handles the logic to fetch, save, update, and delete records — **automatically**.

💡 To achieve this magic, Spring Data relies on **key interfaces**. Understanding them is essential if you want to:

- Build database-backed applications easily
    
- Pass technical interviews on Spring
    
- Use Spring Data JPA like a pro
    

---

## 🏛️ Base Interface: `Repository<T, ID>`

### 🧭 What It Is:

- A **marker interface** — has **no methods**, just a placeholder
    
- Found in `spring-data-commons` (automatically included in your dependencies)
    

### 🔧 Purpose:

- Acts as a base for all Spring Data repositories
    
- Used during classpath scanning to identify repository beans
    

### 🧠 Type Parameters:

|Parameter|Meaning|
|---|---|
|`T`|The domain/entity class (e.g., `Person`, `Product`)|
|`ID`|The primary key type (e.g., `Long`, `String`)|

📌 Example:

	java

	`public interface PersonRepository extends Repository<Person, Long> {}`

---

## 🔁 `CrudRepository<T, ID>`

### 🔧 Provides basic CRUD operations:

|Method|Purpose|
|---|---|
|`save()`|Insert/update an entity|
|`findById()`|Fetch by primary key|
|`findAll()`|Fetch all records|
|`deleteById()`|Delete by ID|
|`deleteAll()`|Delete all records|

✨ Spring automatically **generates implementations** of these methods at runtime.

---

## 📋 `ListCrudRepository<T, ID>`

### 💡 Difference from `CrudRepository`:

- All return types are `List<T>` instead of `Iterable<T>`
    

Use this when you prefer **List collections** over Iterable.

---

## 📚 `PagingAndSortingRepository<T, ID>`

### 🌐 Adds support for:

- **Pagination** (dividing results into pages)
    
- **Sorting** (ordering by fields)
    

### 🔍 Important Methods:

|Method|Description|
|---|---|
|`findAll(Sort sort)`|Sort records by a field|
|`findAll(Pageable page)`|Fetch records in a paged format|

> Don’t worry if you’re not familiar with `Pageable` or `Sort` — they’ll be explained in detail later.

---

## 📋 `ListPagingAndSortingRepository<T, ID>`

Same as above, but returns a `List<T>` instead of `Iterable<T>`.

---

## 🧱 Interface Hierarchy Overview

java

           `Repository                │  ┌─────────────┴─────────────┐  │                           │ CrudRepository     PagingAndSortingRepository      │                           │ ListCrudRepository     ListPagingAndSortingRepository                              │                     JpaRepository (extends both!)`

---

## 💎 `JpaRepository<T, ID>`

### 🧠 What Makes It Powerful:

- Part of **Spring Data JPA** (not `spring-data-commons`)
    
- Extends:
    
    - `ListCrudRepository`
        
    - `ListPagingAndSortingRepository`
        
- Adds **JPA-specific methods** like:
    
    - `saveAndFlush()`
        
    - `deleteAllInBatch()`
        
    - `flush()`
        

📌 Recommendation:  
If you're using Spring Data JPA, **always extend `JpaRepository`** — you’ll get everything in one place.

---

## ⚠️ Important Clarifications

### 1. `@Repository` vs `Repository` Interface

|`@Repository` (annotation)|`Repository` (interface)|
|---|---|
|A **Spring stereotype** annotation|A **marker interface** for Spring Data|
|Indicates the class is a repository|Base interface for creating data access layers|
|Improves readability & bean detection|Doesn't contain methods directly|

---

### 2. Why So Many Interfaces?

🧠 Answer: **Interface Segregation Principle**

> Give developers exactly what they need — nothing more, nothing less.

Examples:

- Only need basic CRUD? Use `CrudRepository`
    
- Need paging/sorting too? Use `PagingAndSortingRepository`
    
- Need everything in `List` form? Use the list variants
    
- Using JPA? Go with `JpaRepository`
    

🎯 Keeps your code **clean**, **lean**, and **purpose-specific**.

---

## 🌎 Subprojects of Spring Data

Spring Data is an umbrella project. Based on your database, use:

|Use Case|Subproject|
|---|---|
|SQL DB (e.g. MySQL)|Spring Data JPA|
|Plain JDBC|Spring Data JDBC|
|MongoDB|Spring Data MongoDB|
|Redis|Spring Data Redis|

✅ All of them rely on **common interfaces** from `spring-data-commons`.

---

## ✨ Summary

🔹 `Repository` is the root marker interface  
🔹 `CrudRepository` provides basic create, read, update, delete methods  
🔹 `PagingAndSortingRepository` adds paging and sorting  
🔹 `List...` interfaces give you List return types  
🔹 `JpaRepository` combines all of the above + JPA-specific features  
🔹 Use **only what you need**, thanks to **interface segregation**  
🔹 `@Repository` annotation ≠ `Repository` interface  
🔹 All common interfaces live in `spring-data-commons`  
🔹 `JpaRepository` lives in the `spring-data-jpa` module

---

## 🔮 Coming Up Next

In the next lecture, we’ll **deep dive into `JpaRepository`**, its features, and how it works with **Hibernate** behind the scenes to make JPA even more powerful in Spring Boot applications.

---

👋 Thank you and see you in the next class! Let's keep learning Spring the smart way! ☕📚💻