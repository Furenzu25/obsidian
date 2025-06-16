# 🌐 Study Notes: Global Exception Handling in Spring MVC

📚 _Using `@ControllerAdvice` and `@ExceptionHandler`_

---

## 🎯 **Objective**

In a real-world production application, you should never expose raw technical error messages (stack traces, exception names, etc.) to the end-user. Instead, show a **customized, user-friendly error page** like:

> 🚫 “Something went wrong. Please contact support with Error Code #500.”

This makes your application look professional and secure.

---

## 💥 Current Problem

Right now, if a **RuntimeException** is thrown in your Spring app (e.g., during login), the user sees:

	vbnet

`Internal Server Error (500) RuntimeException: It's been a bad day 😩`

🔎 This is:

- Helpful in development ✅
    
- 🚫 Not suitable for production (users don’t understand tech errors and it exposes internal logic)
    

---

## ✅ **Solution: Custom Global Error Handling**

Spring provides two special annotations to handle exceptions **globally**:

1. `@ControllerAdvice`
    
2. `@ExceptionHandler`
    

---

## 🧩 `@ControllerAdvice` – The Global Interceptor 🛡️

### What is it?

- A **specialized annotation** (like `@Component`)
    
- Acts as a **global interceptor** for exceptions thrown from:
    
    - `@RequestMapping`
        
    - `@GetMapping`
        
    - `@PostMapping`
        
    - Any controller method
        

### How to Use:

- Create a new Java class
    
- Annotate the class with `@ControllerAdvice`
    

	java

		@ControllerAdvice public class GlobalExceptionHandler {     // Exception handling methods go here }

---

## ⚙️ `@ExceptionHandler` – Handling Specific Exceptions 🛠️

### What is it?

- Used to define **methods** that handle specific exception types.
    

### Example:

	java

	@ExceptionHandler(Exception.class) public String handleGlobalException(Exception ex, Model model) {     model.addAttribute("errorMessage", ex.getMessage());     return "custom-error"; }

- This method will run **whenever an `Exception` occurs**.
    
- You can return a custom error view (e.g., `custom-error.html`).
    

---

## 📌 Key Points:

|Feature|Description|
|---|---|
|🧠 `@ControllerAdvice`|Declares a **global exception handling class**|
|🔧 `@ExceptionHandler`|Declares a method that **handles a specific exception**|
|🎯 Exception Matching|You can write **multiple methods** for different exceptions like `NullPointerException`, `RuntimeException`, etc.|
|🌍 Scope|Works for **all controllers** in your Spring MVC or REST application|
|💡 AOP Connection|It's an **Aspect-Oriented Programming (AOP)** feature — intercepting behavior across multiple classes|

---

## 💡 Real-World Use Cases

With global exception handling, you can easily:

- Show user-friendly error pages
    
- Log exceptions into a file or database 📋
    
- Send email alerts to support team 📧
    
- Return structured error responses for REST APIs 🧾
    

---

## ❗ Interview Tip

> 🎤 **Question:** “How can you implement global exception handling in Spring MVC?”  
> ✅ **Answer:** “Using `@ControllerAdvice` and `@ExceptionHandler` annotations.”

This is a **common Spring interview question** to check if you truly understand Spring’s power and AOP capabilities.

---

## ✅ Summary

|Concept|Description|
|---|---|
|`@ControllerAdvice`|Class-level interceptor to manage global exception handling|
|`@ExceptionHandler`|Method-level handler for specific exception types|
|Use Case|Return custom error pages or perform business logic on error|
|Good For|Both MVC and REST controllers|
|Bonus|You can log, notify, or audit exceptions consistently|

---

📘 _You now have the tools to gracefully handle exceptions like a pro. Instead of panicked users, you’ll have professional error screens and stable performance!_

See you in the next lecture 👋✨