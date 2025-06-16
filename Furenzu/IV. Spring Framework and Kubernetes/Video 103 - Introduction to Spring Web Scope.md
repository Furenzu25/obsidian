# 📘 Study Notes: Spring Web Scopes Explained 🌐

---

## 🧩 Recap: Bean Scopes in Spring

Spring Framework provides **5 primary bean scopes**:

1. 🟦 **Singleton** – One shared bean across the application (default).
    
2. 🟢 **Prototype** – New bean created **each time** it’s requested.
    
3. 🔵 **Request** – New bean per **HTTP request** (Web apps only).
    
4. 🟠 **Session** – New bean per **HTTP session** (Web apps only).
    
5. 🔴 **Application** – One bean for the **entire web app** (Web apps only).
    

> Singleton and Prototype can be used in _any_ kind of application (web or non-web).  
> Request, Session, and Application scopes are **specific to web applications**.

---

## 🌐 Why Are Web Scopes Special?

Web scopes exist because **web apps run on HTTP requests and sessions**. Each user interaction (like login, form submission, browsing pages) triggers HTTP requests. Spring leverages these to manage bean lifecycles.

---

## 🔹 1. Request Scope (`@RequestScope`)

📌 **Definition**: Creates a **new bean instance for every HTTP request**.

### 📥 When to Use:

- You want short-lived data tied only to a single request.
    
- Perfect for one-time use beans (e.g., request metadata, form handlers).
    

### 📅 Example Scenario:

- A user submits a form → new bean instance created just for that request.
    

### 🔄 Result:

- If 5 users perform 10 actions in 5 minutes → 50 HTTP requests = 50 bean instances.
    

---

## 🔸 2. Session Scope (`@SessionScope`)

📌 **Definition**: Creates a **bean instance per user session**. The bean lives **as long as the session is active**.

### 👤 When to Use:

- You want to preserve data **for the duration of a user's session**.
    
- Ideal for login sessions, shopping carts, or temporary user preferences.
    

### 📅 Example Scenario:

- A user logs in → a bean is created and reused **until logout, browser close, or session expiration**.
    

### 🔄 Result:

- 5 users = 5 sessions → 5 unique beans (one per session).
    

---

## 🔻 3. Application Scope (`@ApplicationScope`)

📌 **Definition**: Creates a **single bean instance shared across the entire application**.

### 🌍 When to Use:

- You want to maintain **global state or configuration** that doesn’t change per request or session.
    
- Useful for caching, application-wide settings, shared resources.
    

### 📅 Example Scenario:

- A logger, global counters, or centralized configuration.
    

### 🔄 Result:

- Regardless of how many users or requests → only **1 instance of the bean** exists.
    

---

## ⚖️ Summary Table: Web Scopes in Spring

|Scope|Lifetime|Number of Beans|Annotation|
|---|---|---|---|
|🟦 Singleton|Entire application|1|`@Scope("singleton")` _(default)_|
|🟢 Prototype|New per request/programmatic use|Many|`@Scope("prototype")`|
|🔵 Request|Per HTTP request|1 per request|`@RequestScope`|
|🟠 Session|Per HTTP session (per user)|1 per session|`@SessionScope`|
|🔴 Application|Entire web app (shared globally)|1|`@ApplicationScope`|

---

## 🧠 Key Takeaways

- 🌐 Web-specific scopes help manage beans **according to HTTP context**.
    
- 👁️ Use `@RequestScope`, `@SessionScope`, and `@ApplicationScope` **only in Spring Web applications**.
    
- 🧪 Test and monitor bean behavior if your application handles large traffic or critical state per user/session/request.
    
- ✅ Choose scope based on **how long you need to retain data** and **who needs access to it**.
    

---

## 📍 Coming Next…

In the next lecture, we’ll explore **real-world use cases** for each of these web scopes and learn how to apply them in a Spring web application effectively.

---

✅ **You now understand how to control the lifecycle of beans in web applications using scopes**.  
See you in the next lecture! 👋💻