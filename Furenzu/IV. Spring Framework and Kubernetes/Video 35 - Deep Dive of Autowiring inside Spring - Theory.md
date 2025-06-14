## 🔁 Spring Framework: Deep Dive into Autowiring Internals

When building applications with the Spring Framework, **autowiring** is a core concept that simplifies how beans are connected. But things get tricky when you have **multiple beans of the same type** 😬. So how does Spring know which bean to inject?

Let’s explore the **internal steps Spring follows for autowiring**, especially in **ambiguous situations**. 🧠

---

### 🔍 What Is Autowiring?

Autowiring in Spring allows the framework to automatically inject dependencies between beans. By default, it works **by type** — Spring looks at the data type and injects the matching bean.

👉 For example, if there's **only one `Vehicle` bean**, Spring injects it wherever `Vehicle` is required. No ambiguity, no problems.

---

### ❓ What Happens When There Are Multiple Beans?

Let’s say your context contains:

- `vehicleOne 🚗`
    
- `vehicleTwo 🚙`
    
- `vehicleThree 🛺`
    

If Spring sees a constructor like this:

java

CopyEdit

`public Person(Vehicle vehicle) { ... }`

It’s not sure **which vehicle bean to inject**. Here’s how Spring resolves this:

---

### 🧭 **Step-by-Step Autowiring Resolution**

#### **✅ Step 1: Match by Parameter Name (By Name)**

Spring will **first check if the constructor parameter name** matches a bean name in the context.

java

CopyEdit

`public Person(Vehicle vehicleOne) { ... }`

- If a bean named `vehicleOne` exists, Spring will use it.
    
- ✅ `vehicleOne` gets injected!
    
- ❌ `vehicleTwo` and `vehicleThree` are ignored.
    

📌 **This step works only if parameter names match bean names.**

---

#### **✅ Step 2: Use @Primary Annotation**

If there’s **no matching parameter name**, Spring moves to the next rule:

> 🔎 Look for a bean annotated with `@Primary`.

java

CopyEdit

`@Bean @Primary public Vehicle vehicleThree() { ... }`

- Even if the constructor is just:
    
    java
    
    CopyEdit
    
    `public Person(Vehicle vehicle) { ... }`
    
- ✅ Spring injects `vehicleThree` because it's marked `@Primary`.
    

---

#### **✅ Step 3: Use @Qualifier Annotation**

If no `@Primary` is found or more control is needed, use `@Qualifier`.

java

CopyEdit

`public Person(@Qualifier("vehicleTwo") Vehicle vehicle) { ... }`

This tells Spring:

> “Inject the **`vehicleTwo` bean** — no matter what the parameter name is.”

📌 **Advantages**:

- Clearer, more maintainable
    
- Prevents accidental errors if someone renames parameters
    

---

### 🚫 What If None of These Work?

If Spring **still can't decide** which bean to inject (after trying by name, by primary, and by qualifier), it throws a **startup exception** ❌💥.

---

### 🧠 Summary of Autowiring Logic

|Step|Strategy|How It Works|Example|
|---|---|---|---|
|1️⃣|**By Name**|Matches bean name with parameter name|`vehicleOne` param → `vehicleOne` bean|
|2️⃣|**@Primary**|Uses the bean marked with `@Primary`|Injects `vehicleThree` if it's `@Primary`|
|3️⃣|**@Qualifier**|Explicitly names the bean to inject|`@Qualifier("vehicleTwo")` → injects that bean|

---

### ⚠️ Key Reminders

- 🔧 Autowiring **defaults to by type**.
    
- When multiple beans of the same type exist:
    
    - Spring checks by **name** 🏷️
        
    - Then by **@Primary** 📌
        
    - Then by **@Qualifier** 🎯
        
- These apply to **constructor**, **field**, or **setter** injections alike.
    
- If all else fails → **exception on startup** 🚨
    

---

### 📦 Coming Up Next...

In the next lecture, we’ll implement all three steps in a **real project** — so you can see them in action! 💻

Until then, keep wiring smart 🔌😉