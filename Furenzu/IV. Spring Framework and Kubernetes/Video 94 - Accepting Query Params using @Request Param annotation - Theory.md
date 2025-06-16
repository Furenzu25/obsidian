# 📘 Study Notes: Handling Query Parameters in Spring MVC 🌐

---

## 🧠 What Are Query Parameters?

- **Query parameters** are key-value pairs that you append to a URL to send extra data to the server.
    
- They are most commonly used with **GET requests** (but can apply to others too).
    

📌 Example URL:

	bash

	localhost:8080/holidays?festival=true&federal=true

👉 In this case:

- The path is `/holidays`
    
- There are **two query parameters**: `festival=true` and `federal=true`
    

---

## 🛠 Use Case: Filtering Based on Query Params

Imagine you're building a holiday page that displays both:

- 🎉 Festival holidays
    
- 🏛️ Federal holidays
    

With query params:

- `?festival=true&federal=true` → show both
    
- `?festival=true` only → show just festival holidays
    
- `?federal=true` only → show just federal holidays
    

💡 These query parameters act like **filters**, helping users get more specific content.

---

## 🛒 Real-World Example: E-Commerce Sites

You’ve likely seen URLs like this when shopping:

	bash

	/products?order=popular&newOnly=true

- `order=popular` → sort products by popularity
    
- `newOnly=true` → show only new items
    

🔎 Filters like these are passed to the backend as **query parameters**.

---

## 🧩 Query Param Structure

To add query parameters to a GET URL:

1. Start with your **base path**, e.g., `/products`
    
2. Use a **question mark (?)** to add the first query param  
    `?key=value`
    
3. Use **ampersands (&)** to add more params  
    `?key1=value1&key2=value2`
    

✅ Best Practice: Keep your query params short (ideally 3–4). Don’t overload your URL with 20+ parameters — it makes things hard to read.

---

## 🛠 How to Handle Query Params in Spring MVC

Use the annotation `@RequestParam` to accept query parameters in your controller.

📌 Example:

	java

	@GetMapping("/holidays") public String displayHolidays(     @RequestParam boolean festival,     @RequestParam boolean federal,     Model model) {     // Logic here... }

In this code:

- The parameters `festival` and `federal` are automatically extracted from the query string in the URL.
    
- Spring assigns the values to the corresponding method arguments.
    

---

## 🔄 Reusing `@RequestParam` for Form Data

Remember this? 📝

- When we saved contact form data using:
    

	java

	@RequestParam String name @RequestParam String email ...

📌 `@RequestParam` works for both:

- **Query parameters in the URL**
    
- **Form fields submitted from HTML forms**
    

---

## ⚙️ Advanced `@RequestParam` Options

You can customize how query params are handled using these attributes inside `@RequestParam`:

|Attribute|Purpose|
|---|---|
|`required = true`|(default) The param **must be present**. Missing it throws an error.|
|`required = false`|Makes the param **optional**. Safe if the value might not be passed.|
|`defaultValue = "x"`|Uses the default if the param is **not sent in the request**.|
|`name = "param"`|Explicitly **binds** the query param to a different method name.|
|`value = "param"`|Same as `name`. Used to define an **alias**.|

### 💡 Example with Optional and Default Value

	java

	@RequestParam(required = false, defaultValue = "false") boolean festival

- This allows you to skip the `festival` param in the URL.
    
- If skipped, it defaults to `false`.
    

---

## 🔁 Matching Names

Spring MVC will auto-map query params from the URL to method parameters if **their names match**.

💡 But if your method parameter name differs, use the `name` or `value` attribute:

	java

	@RequestParam(name = "festival") boolean isFestival

---

## 📌 Key Takeaways

✅ Query parameters allow users to **filter, sort, or modify** results.  
✅ In Spring MVC, use `@RequestParam` to access these params.  
✅ Make params optional or provide default values to avoid errors.  
✅ Keep your URLs readable and manageable — don’t overload with too many query params.

---

## 💬 Coming Up Next…

In the **next lecture**, you'll enhance the **Eazy School holiday page** to dynamically show:

- Only federal holidays 🏛️
    
- Only festival holidays 🎉
    
- Or both — depending on the query params in the URL!
    

---

👋 That’s it for this lecture.  
🎯 Practice using `@RequestParam` with optional fields, defaults, and real data filtering.  
Happy coding and see you next time!