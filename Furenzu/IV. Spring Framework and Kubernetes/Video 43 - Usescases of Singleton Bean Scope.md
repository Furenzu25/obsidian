## 🟢 Singleton Bean Scope in Spring — When and Why to Use It

### 🚀 What You’ll Learn:

In this lecture, we dive into:

- **What singleton beans are**
    
- **When to use them effectively**
    
- ⚠️ **Common pitfalls** to avoid
    
- ✅ Best practices for implementation
    

---

### 🧩 What is a Singleton Bean?

- **Singleton** is the **default scope** in Spring — meaning:
    
    > Spring creates **only one instance** of the bean per container, and that same instance is reused throughout the application.
    

You don’t need to explicitly define it unless you’re changing to another scope.

---

### 📌 When Should You Use Singleton Beans?

✅ **Use Singleton** when your class:

- Contains **only business logic**
    
- Has **no mutable fields** (i.e., no data that needs to change after creation)
    
- Is designed to be **immutable**
    

💡 Typical examples:

- Service classes 🛠️
    
- Repository classes 🗄️
    
- Utility beans 🔧
    

---

### ⚠️ When _Not_ to Use Singleton

Avoid singleton beans if:

- Your bean holds **mutable state** (e.g., fields like `name`, `age`, etc. that may change)
    
- Multiple threads could be accessing and modifying the bean simultaneously
    

🛑 **Why?**

- It introduces **race conditions** in multi-threaded environments
    
- It can lead to complex **synchronization issues**
    
- Adds significant **performance overhead** due to locking mechanisms
    

---

### 💥 Example of What _Not_ to Do

Imagine a bean with:
	
	`java`
	
`String name; int age;`

If any logic in the application updates these values, **this bean is mutable** — and using it as a singleton will create bugs and inconsistencies when accessed by multiple threads. ❌

---

### 🛠️ Tip: Use Constructor Injection

✔ Constructor injection promotes immutability  
✔ It allows you to declare fields as `final`  
✔ This ensures the singleton bean remains unchanged after initialization

---

### 📉 Why Mutable Singletons are a Bad Idea

Using mutable singletons:

- Forces you to add **locks and synchronization**
    
- Introduces **performance degradation**
    
- Increases the **complexity** of your code
    

🧊 Keep your beans **immutable** to avoid these issues.

---

### 🔍 Avoid Creating Beans Unnecessarily

Don’t create beans for:

- Simple **POJOs** (Plain Old Java Objects) 💾
    
- Classes with **only getters, setters, and fields**, and **no business logic**
    

📝 If your class is just a data container (like a DTO), it **shouldn’t be a Spring-managed bean**.

---

### ✅ Summary: Best Practices for Singleton Beans

|✔️ Do|❌ Don’t|
|---|---|
|Use singleton scope for **stateless, immutable logic**|Use singleton scope for **mutable stateful beans**|
|Inject dependencies via **constructor** for immutability|Depend on **mutable field injection**|
|Keep business logic inside beans|Turn simple data classes into beans|
|Leverage singleton for **services & repositories**|Add synchronization just to manage bean safety|

---

### 🧪 Bonus Insight

🧬 In a demo, comparing hash codes of multiple singleton references proved that:

> Spring returns the **same object reference** every time.

This reinforces why the singleton pattern demands **careful design**!

---

🎉 Now you're crystal clear on **when and how to use singleton beans in Spring**.  
Up next: Learn how **Prototype scope** works and when it might be the better choice. See you in the next lecture! 👋