# 📘 Study Notes: Handling Path Variables in Spring MVC 🌐

---

## 🔁 Recap: What We Already Know

In previous lectures, we discussed **query parameters**:

- Appended after a `?` in the URL (e.g., `?filter=new&sort=popular`)
    
- Used with the `@RequestParam` annotation
    
- Key-value style filters for dynamic content
    

---

## 🚪 Introduction to Path Variables

Now let’s understand a different approach — **Path Variables** (aka **Path Params**).

### ❓ What Are Path Variables?

- They are **dynamic parts of the URL path**.
    
- Unlike query params, they don’t use `=` or `&`.
    
- They’re placed **directly into the URL path**.
    

📌 Example:

	bash

	/products/popular /products/newest /products/oldest

Here, `popular`, `newest`, and `oldest` are **path variables** — values that change depending on the user’s action or selection.

---

## 🔍 Query Params vs Path Variables

|Feature|Query Params|Path Variables|
|---|---|---|
|Format|`?key=value` (e.g. `?sort=popular`)|`/value` (e.g. `/popular`)|
|Syntax|Uses `?` and `&` for multiple values|Uses `/` to separate values|
|Use Case|Filtering, searching, optional parameters|Route-based decisions, cleaner URLs|
|Annotation in Spring|`@RequestParam`|`@PathVariable`|
|Can have default?|✅ Yes (via `defaultValue`)|❌ No default value support|

---

## 💡 When to Use Path Variables

- When you want **cleaner URLs**.
    
- When the path **itself represents a resource** or state.
    
- Example:
    
    - `/holidays/all` → Show all holidays
        
    - `/holidays/federal` → Show only federal holidays
        
    - `/holidays/festival` → Show only festival holidays
        

---

## 🛠 Accepting Path Variables in Spring MVC

### ✅ Using `@PathVariable` Annotation

You define a method to receive a path variable by:

1. Specifying the dynamic part in `{}` in the URL
    
2. Using `@PathVariable` in the method parameter
    

📌 Example:
	
	java
	
	@GetMapping("/holidays/{display}") public String displayHolidays(@PathVariable String display) {     // Use 'display' to control what holidays to show }

### Explanation:

- `/holidays/{display}` → this means the `{display}` part is dynamic.
    
- `@PathVariable String display` → this binds the URL value to the method argument.
    

If someone visits:

- `/holidays/all` → `display = "all"`
    
- `/holidays/federal` → `display = "federal"`
    
- `/holidays/festival` → `display = "festival"`
    

---

## 🧩 Multiple Path Variables

You can also use **multiple path variables** by chaining with `/`.

📌 Example:

	bash

	/users/123/orders/456

	java

	@GetMapping("/users/{userId}/orders/{orderId}") public String getOrderDetails(@PathVariable int userId, @PathVariable int orderId) {     // Logic here... }

---

## ⚙️ Additional Attributes in `@PathVariable`

Just like `@RequestParam`, `@PathVariable` supports some optional attributes:

|Attribute|Description|
|---|---|
|`name`|Alias for the variable name in the URL path|
|`value`|Same as `name`|
|`required`|Makes the path variable optional (default: `true`)|

🛑 **Important**: Unlike `@RequestParam`, `@PathVariable` does **not** support `defaultValue`.

---

## 📦 Summary

|Concept|Description|
|---|---|
|**Path Variable**|Dynamic value inside the URL path (e.g., `/products/popular`)|
|**Annotation Used**|`@PathVariable`|
|**Use Case**|Route-based decisions, user-specific paths, cleaner RESTful URLs|
|**Compared to Query Param**|Path variables are cleaner but less flexible with optional/default values|
|**Multiple Variables**|Supported using `/value1/value2/...`|

---

## 🏗 Coming Up Next...

🎯 In the **next lecture**, you'll **enhance the Eazy School web application**:

- Accept path variables from the frontend
    
- Use them to control what kind of holidays to display on the `/holidays` page
    

---

👋 Thanks for reading!  
Keep experimenting with both query and path variables in your Spring Boot apps — they’re essential tools for building clean, user-friendly APIs.  
See you in the next lecture! 🚀