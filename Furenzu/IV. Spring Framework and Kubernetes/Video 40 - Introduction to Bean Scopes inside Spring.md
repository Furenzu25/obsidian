## 🌱 Understanding Bean Scopes in Spring Framework

So far, you've learned how to:

- ✅ Create beans
    
- ✅ Define dependencies
    
- ✅ Inject dependencies using **Dependency Injection** and **Autowiring**
    

But a key question still remains:

> ❓ **When is a bean actually created? And how long does it live inside the Spring container?**

---

### 🧠 Real-World Scenario

Imagine this:

- You have a `Person` bean 👤
    
- That `Person` depends on a `Vehicle` bean 🚗
    
- And that `Vehicle` depends on a `VehicleService` bean 🎵🛞
    

Every time the application runs, Spring is injecting these beans — but this example only considers **one user** or **one thread**. What happens when your application has **multiple users** or **multiple threads** in production?

👉 **Does Spring return the same bean each time, or does it create a new one every time?**

---

### 💡 Enter: Bean Scopes in Spring

**Bean Scope** defines the **lifecycle and visibility** of a bean — in other words:

> “How many times should this bean be created and when should it be reused?”

Spring manages this behavior using **Bean Scopes** 🧪.

---

### 📦 Types of Bean Scopes in Spring

Here are the **5 types of bean scopes** available in Spring:

|Scope Name|Description|
|---|---|
|1️⃣ Singleton|🟢 Default scope. Only **one instance** of the bean is created per Spring container|
|2️⃣ Prototype|🆕 A **new bean instance** is created **every time** it is requested|
|3️⃣ Request|🌐 A new bean is created for **each HTTP request** _(Web apps only)_|
|4️⃣ Session|🧑‍💻 One bean per **HTTP session** _(Web apps only)_|
|5️⃣ Application|🏛️ One bean shared across the **entire application** _(Web apps only)_|

📌 **Note**: `Request`, `Session`, and `Application` scopes are only applicable when you're building **web applications** using **Spring MVC**.

---

### 🔍 What Is the Default?

By default, **Spring uses the `Singleton` scope** 🟢.

This means:

- A bean is created **once** and **shared** across the entire application.
    
- It's reused every time it is needed until the application shuts down or restarts.
    

---

### 🚦 Why Are Scopes Important?

Because in a **multi-threaded**, **multi-user** environment:

- You may not always want a **shared** bean (singleton).
    
- In some cases, a **new instance per use** (prototype) is safer and more appropriate.
    

So choosing the **right bean scope** depends entirely on your **application’s requirements** ✅

---

### 🧭 What’s Next?

In the next part of the course, we will:

- Dive deeper into **Singleton** scope 🟢
    
- Understand how it's managed by the Spring container
    
- Explore how it differs from the **Prototype** scope 🆕
    

This foundational knowledge will prepare you for using scopes effectively in **Spring MVC web applications** later on.

---

### 📝 Summary

- Spring provides **5 bean scopes**: `Singleton`, `Prototype`, `Request`, `Session`, `Application`
    
- The **default** is `Singleton`
    
- Scopes control **how and when beans are created and reused**
    
- Choosing the right scope is crucial for proper application behavior, especially in web and multi-threaded environments
    

---

👋 Thanks for learning! You now understand the **"what and why" of Spring bean scopes**.  
➡️ Up next: Understanding the **Singleton Scope** in depth. See you there! 🎓