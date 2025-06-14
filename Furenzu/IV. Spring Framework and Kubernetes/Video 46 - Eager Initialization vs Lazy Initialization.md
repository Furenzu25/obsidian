## ⚡ Eager vs 💤 Lazy Instantiation in Spring Framework

### 📚 Objective:

Understand the **differences between eager and lazy instantiation** styles when dealing with **singleton beans** in Spring, and learn **when to use each approach** wisely.

---

### 1️⃣ Default Behavior in Spring

- 🔧 **Eager Instantiation** is the **default** in Spring.
    
- 💤 **Lazy Instantiation** must be **explicitly enabled** using the `@Lazy` annotation.
    
	
	`java`
	
`@Lazy @Component public class MyBean { ... }`

---

### 2️⃣ When is the Bean Created?

|Instantiation Type|Creation Time|
|---|---|
|⚡ **Eager**|During **startup** of the Spring container|
|💤 **Lazy**|At **first use**, when the application **actually refers to** the bean|

---

### 3️⃣ Error Handling 🧨

- ⚡ **Eager**:  
    ➤ If a bean fails to initialize, the server **won’t start**.  
    ➤ You’ll know the error **immediately**.
    
- 💤 **Lazy**:  
    ➤ The app will **start normally** even if the bean has issues.  
    ➤ But the error will **surprise you** later — possibly on the **user interface** during runtime.
    

---

### 4️⃣ Memory & Performance 📊

#### ⚡ Eager Instantiation:

- All beans are created at startup — even unused ones.
    
- Leads to **higher memory consumption** and **slower startup**.
    

#### 💤 Lazy Instantiation:

- Saves memory by **deferring creation**.
    
- ⚠️ But can cause a **slight performance delay** when the bean is accessed for the first time.
    

🧠 Why?  
Spring needs to check:

1. Is the bean already created?
    
2. If not, it has to create it **on-the-fly**, which adds to response time — especially if the bean’s constructor contains **heavy logic**.
    

---

### 5️⃣ Usage Recommendation 🎯

- ✅ **Use Eager Instantiation** for:
    
    - Beans used **commonly and frequently**
        
    - Core components and services
        
    - Initialization where **fail fast** behavior is preferred
        
- ✅ **Use Lazy Instantiation** for:
    
    - Beans used in **rare or remote scenarios**
        
    - Optional features or background utilities
        
    - Costly beans that may **never be needed**
        

---

### 6️⃣ The Golden Rule ⚖️

> "Balance is key."

🔢 While there’s no strict formula, a **90% eager, 10% lazy** rule of thumb can be a good starting point.

🔍 However, this ratio **varies by application** — as a developer, it’s your **responsibility to analyze** each use case.

---

### 🧠 Summary Table

|Feature|⚡ Eager|💤 Lazy|
|---|---|---|
|**Default?**|✅ Yes|❌ No (use `@Lazy`)|
|**Bean Created When?**|App startup|First use|
|**Startup Impact**|⏱️ Slower, heavier memory|🚀 Faster, lightweight|
|**Error Timing**|❌ Immediate on failure|⚠️ Delayed (runtime surprise)|
|**Best For**|Common beans, core logic|Remote features, optional logic|
|**Performance Hit**|Front-loaded|Deferred, slight runtime cost|

---

### 🔚 Final Words

- Be **intentional**: Don’t blindly make everything lazy or eager.
    
- Analyze usage, resource demands, and performance goals.
    
- Understand the **trade-offs** and design your bean lifecycle **strategically**.
    

🎉 You’re now super clear on how **eager and lazy instantiation** work in Spring!  
Next up: **Prototype Scope** — a whole new behavior to explore. See you in the next lecture! 👋