## 💤 Eager vs Lazy Instantiation in Spring — A Complete Guide

### 🎯 What You’ll Learn:

- What **eager instantiation** is and how Spring handles it by default
    
- What **lazy instantiation** means and when to use it
    
- ✅ Pros and ❌ cons of each
    
- How to use the `@Lazy` annotation effectively in Spring
    

---

### 🟢 Recap: Singleton Scope Reminder

In **singleton scope**, Spring’s IoC container creates **one single bean instance** and reuses it across the entire application.  
But **when** Spring creates that instance is a matter of **instantiation strategy**.

---

### ⚡ Eager Instantiation — The Default Behavior

**Definition**:  
🧠 Spring **eagerly creates all singleton beans** at **startup time**, **whether** they are used or not.

This is known as **eager instantiation**.

#### ✅ Advantages:

- 💥 **Immediate failure** if bean creation fails — the server won’t start.
    
- ✅ Ensures all dependencies are ready to go at startup.
    
- 🧪 Great for testing initialization issues early.
    

#### ❌ Disadvantages:

- 🚫 Wastes memory if certain beans are **never used**.
    
- 🐢 Slows down startup time if there are **too many beans**.
    

---

### 🕓 Lazy Instantiation — When You Want to Wait

**Definition**:  
Spring waits to create the bean **only when it's first needed** — known as **lazy instantiation**.

You enable this using the `@Lazy` annotation:
	
	`java`
	
`@Lazy @Component public class Person { ... }`

#### ✅ When to Use It:

- 🔒 Beans tied to **rare or remote scenarios**  
    (e.g., closing/deactivating an account on an e-commerce site)
    
- 🧠 When you want to **optimize memory usage** and avoid loading unused beans
    
- 🧳 If your application has **lots of beans** and some are rarely used
    

#### ❌ Disadvantages:

- ❗ Errors show up **only at runtime** (after user interaction)
    
- 🌐 User may see exceptions on UI if bean creation fails during interaction
    

---

### 🧪 Real-World Example: Lazy Bean Instantiation

Let’s say you have a `Person` bean configured like this:
	
	`java`
	
`@Lazy @Component public class Person {     public Person() {         System.out.println("Person Bean created by Spring");     } }`

And your code includes:
	
	`java`
	
`System.out.println("Before getBean call"); Person person = context.getBean(Person.class); System.out.println("After getBean call");`

🖨️ Output:
	
	`pgsql`
	
`Before getBean call Person Bean created by Spring After getBean call`

✔ This proves:

- The bean is **not created at startup**
    
- It’s created **only** when `getBean()` or dependency injection is triggered
    

---

### 📌 Summary: Eager vs Lazy Instantiation

|Instantiation Type|Created At|Default?|Pros|Cons|
|---|---|---|---|---|
|⚡ **Eager**|At startup|✅ Yes|Catches errors early, ready to use|Slower startup, memory waste|
|💤 **Lazy**|On first use|❌ No|Saves memory, speeds up startup|Runtime errors, delayed feedback|

---

### ✅ Best Practices

- Use **eager instantiation** as the **default**, unless you have a **specific reason** not to.
    
- Apply `@Lazy` on **rarely-used beans** to improve performance.
    
- Never lazily instantiate **critical application logic** — doing so risks runtime instability.
    

---

### 📌 Final Thoughts

By understanding when to use **eager** vs **lazy** instantiation, you gain fine-grained control over your application's **performance**, **startup behavior**, and **resource utilization**.

🎉 In the next lecture, you’ll see a live demo in a Java application to reinforce these concepts.

See you then! 👋