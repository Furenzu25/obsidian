## 🔁 Prototype Scope in Spring Framework

### 🎯 Objective:

Understand the **prototype bean scope** in Spring, its behavior, suitable use cases, and key considerations—especially when injecting prototype beans into singleton beans.

---

### 🔍 What is Prototype Scope?

- In **prototype scope**, every time you request a bean from the **Spring IoC container**, a **brand new object instance** is created.
    
- This is **opposite** to singleton scope, where the same instance is reused across the application.

	`java`
	
	`@Scope("prototype") @Component public class VehicleService { ... }`

---

### 🧠 When to Use Prototype Scope?

Use it when:

- Your bean **changes internal state frequently** 💥
    
- You want to **avoid race conditions** in a **multi-threaded environment**
    
- Each thread or component needs a **fresh instance** of the bean
    

✅ _Each thread gets its own instance — preventing shared state issues!_

---

### 🧪 Code Demo Recap:

Let’s say you call `getBean(VehicleService.class)` twice:
	
	`java`
	
`VehicleService vs1 = context.getBean(VehicleService.class); VehicleService vs2 = context.getBean(VehicleService.class);`

- Since the scope is prototype, 🛠️ two different **objects are created**.
    
- Their **hashcodes differ**, proving they are **independent instances**.
    

### 💡 Observation:

In the demo output, the bean was created **three times**, not two. Why?

👀 Here's why:

- One instance was created **at startup** because another bean (`Vehicle`) with **singleton scope** had an `@Autowired` reference to `VehicleService`.
    
- Since **singleton beans are eagerly created** at startup, Spring also had to create the dependent `VehicleService` instance — even though it's a prototype.
    

---

### ⚠️ Important Gotcha: Injecting Prototype into Singleton

📌 If you **inject a prototype bean into a singleton bean**, the prototype behaves **like a singleton**.

#### Example:
	
`java`

	`@Component @Scope("singleton") public class Vehicle {   @Autowired   private VehicleService vehicleService; // prototype scoped }`

- Even if `VehicleService` is prototype scoped, the moment it’s injected into the singleton `Vehicle`, it will be treated as a **single shared instance**.
    
- 💡 So calling `vehicleService` multiple times inside `Vehicle` will return the **same object**.
    

✅ If **both Vehicle and VehicleService are prototype**, then a **new instance** will be created each time.

---

### 🧠 Key Takeaways

|Feature|Prototype Scope|
|---|---|
|🔄 Behavior|New object for **each request**|
|🔧 Use Case|Frequent state changes, thread safety|
|🚫 Don't Do|Inject into a singleton if expecting unique instance|
|☝️ When Injected into Singleton|Loses its prototype behavior — acts like a singleton|
|🧪 Verification|Check with `hashCode()` to confirm uniqueness|
|⚠️ Risk|Unexpected sharing of prototype bean when auto-wired into singleton beans|

---

### ✅ When to Use

- ✔️ Beans with **heavy data manipulation**
    
- ✔️ Beans accessed by **multiple threads**
    
- ✔️ Components that should be **isolated per request**
    

---

### 🧬 Summary:

> **Prototype beans = fresh beans 🫘.**
> 
> Use when you need a **new object every time**.  
> But beware of injecting them into **singleton beans**, as they’ll no longer behave as you expect.  
> Always assess your scope needs based on **data mutability** and **thread-safety**!

---

👋 That wraps up **Prototype Scope** in Spring!

Next stop: exploring more advanced bean scopes and best practices.  
See you in the next lecture! 🎓✨