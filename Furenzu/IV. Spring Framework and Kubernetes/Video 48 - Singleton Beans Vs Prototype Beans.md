## 🧠 Singleton vs Prototype Scope in Spring

Understanding the differences between **singleton** and **prototype** scopes is essential when managing bean lifecycles in Spring Framework.

---

### 🔍 Scope Overview

|Scope|Behavior|Use Case|
|---|---|---|
|**Singleton** 🔁|One shared instance|Default; common business logic|
|**Prototype** 🎯|New instance per request|Mutable data, multithreading|

---

### 🥇 1. **Default Nature**

- **Singleton**: ✅ Default bean scope in Spring.
    
- **Prototype**: ❌ Not default. Must be **explicitly declared** with `@Scope("prototype")`.


	`java`
	
`@Scope("prototype") @Bean public VehicleService vehicleService() { ... }`

---

### 🧱 2. **Instance Creation**

- **Singleton**: Same instance is returned every time the bean is accessed.
    
- **Prototype**: A **new object instance is returned each time** you access the bean.
    

🧪 Example:  
Accessing a prototype bean 5 times = 5 different objects.

---

### ⏳ 3. **Initialization Strategy**

- **Singleton**:
    
    - Can be created **eagerly** at application startup.
        
    - Can also be created **lazily** when first accessed (with `@Lazy` annotation).
        
- **Prototype**:
    
    - No concept of eager or lazy initialization.
        
    - ⚠️ Spring creates a new instance **each time** it's requested — always on-demand.
        

💡 While this may **look** like lazy initialization, it's technically **not the same** as lazy/eager in singleton terms. Don't confuse them!

---

### 🧬 4. **Mutability & Use Cases**

- **Singleton**: Best suited for **immutable** objects.  
    → Once created, the object state does **not change**.
    
- **Prototype**: Best suited for **mutable** objects.  
    → Useful when object state **changes after creation**, especially in:
    
    - Multi-threaded applications 🧵
        
    - Scenarios needing isolated state per use
        

---

### ⚖️ 5. **Popularity & Practical Advice**

- **Singleton**: Most common, widely used, and ideal for **business logic classes**.
    
- **Prototype**: Less common, and only used when:
    
    - You’re handling **race conditions** 🏁
        
    - Avoiding **shared mutable state** across threads
        

⚠️ Avoid creating beans for POJOs that only have **getters/setters** with no logic — they don’t need to be Spring beans.

---

### 💡 Developer Tips

🔧 Always assess:

- Does this bean need to maintain shared state? → Singleton ✅
    
- Does this bean need a fresh state for each use/thread? → Prototype ✅
    

🔬 Test examples from practice projects to observe:

- Hash code differences
    
- Object lifecycle behavior
    
- Memory and performance implications
    

---

### 🌐 What’s Next?

📚 In upcoming lectures, we’ll explore other Spring scopes:

- `@RequestScope` 🌍
    
- `@SessionScope` 🧑‍💻
    
- `@ApplicationScope` 🏢
    

These are especially useful in **Spring MVC web applications** — stay tuned! 📺

---

### 🎓 Summary

|Aspect|Singleton|Prototype|
|---|---|---|
|Default Scope|✅ Yes|❌ No|
|Instance|One shared|New per access|
|Initialization|Eager/Lazy|Always on-demand|
|Best for|Immutable logic|Mutable objects|
|Common Use|✅ Very|⚠️ Rare|

---

Thanks for learning! 🚀  
You’re now clear on **singleton vs prototype** scopes in Spring.  
Keep experimenting with real examples to reinforce your understanding! 💻🔁