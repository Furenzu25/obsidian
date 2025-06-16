# 🛡️ Study Notes: CSRF Protection in Spring Security with Thymeleaf

---

## 🧐 Recap: Why Is CSRF a Problem?

In the last lecture, we learned that:

> **CSRF (Cross-Site Request Forgery)** is a vulnerability where a hacker can perform _unauthorized_ actions on behalf of a logged-in user — without their knowledge — using a stolen access token (like a session cookie).

This happens because:

- The **backend cannot differentiate** whether a request comes from a legit user or a malicious script.
    
- Browsers automatically send stored cookies with **every** request — even from other tabs or malicious sites.
    

---

## ✅ CSRF Solution: Use a CSRF Token!

The best way to defend against CSRF is to:

1. Generate a **unique CSRF token** per session during login.
    
2. Send this token **with every request**, but **never store it in browser cookies**.
    
3. Backend will check both:
    
    - The access token (like a session ID) ✔️
        
    - The CSRF token sent via the request ✔️
        
    - If both match → ✅ request is accepted.
        
    - If CSRF token is **missing or invalid** → ❌ request is **rejected** (403 Forbidden).
        

---

## 🔁 CSRF Flow Explained

### 🧾 Step-by-Step (Reinforced from Last Lecture):

1. **Login to netflix.com**
    
    - Session token (e.g., `JSESSIONID`) stored in browser cookie.
        
    - 🔐 CSRF token generated and added as a **hidden input** in HTML forms.
        
2. **Open evil.com (a hacker site)**
    
    - User is tempted by malicious links (e.g., “🔥 90% off on iPhone”).
        
3. **Malicious Request Sent**
    
    - A hidden form auto-submits to netflix.com.
        
    - Session token is sent, but... ❌ **No CSRF token!**
        
4. **Backend Behavior**
    
    - Session token is valid → Looks legit.
        
    - But: ❌ CSRF token is **missing** or **invalid**.
        
    - 🔐 Backend **rejects** the request with **403 Forbidden**.
        

✅ Result: CSRF attack **fails**.

---

## 🔨 CSRF Implementation Using Spring Security + Thymeleaf

The good news? **Spring Security and Thymeleaf handle most of the heavy lifting** for you!

### 🛠️ How It Works

- Spring Security **enables CSRF protection** by default.
    
- Thymeleaf automatically:
    
    - Generates the CSRF token
        
    - Injects it into HTML forms as a hidden field
        

### 🧩 HTML Code to Add in Your Forms:

	html

	<input type="hidden"         th:name="${_csrf.parameterName}"         th:value="${_csrf.token}" />

📌 Place this inside every `<form>` to ensure CSRF token is submitted with each request.

---

## ⚙️ More Developer Tips

### 🔄 When CSRF Protection Applies:

Spring Security **requires CSRF tokens** for HTTP methods that _change state_:

|HTTP Method|Requires CSRF Token?|
|---|---|
|`GET`|❌ No|
|`POST`|✅ Yes|
|`PUT`/`DELETE`|✅ Yes|

---

### 🔧 What If You Disabled CSRF Before?

You may have previously disabled CSRF in your config like this:

	java

	http.csrf().disable();

👉 Now that we’re enabling CSRF protection:

- ❌ **Remove** the `csrf().disable()` line.
    
- ✅ **Add** the hidden CSRF input to your forms.
    

---

### 🔁 Hybrid CSRF Strategy (Optional):

If you want to **disable CSRF** only for specific public pages (like `Contact`), and **keep it enabled** for protected ones (like `Dashboard`):

Use this:

	java

	http.csrf()     .ignoringRequestMatchers("/saveMsg");

This tells Spring Security:

> ❌ “Ignore CSRF for `/saveMsg` route” (e.g., public contact form)  
> ✅ “Enforce CSRF for everything else” (e.g., admin, dashboard, student pages)

---

## 🧠 Summary

|🧩 Key Point|💡 Takeaway|
|---|---|
|❗ CSRF is a dangerous exploit|Prevents unauthorized state-changing actions|
|✅ CSRF token solution|Token stored in form, **not cookies**|
|🔐 Spring + Thymeleaf integration|Makes token generation and injection automatic|
|🧾 Use hidden form input|Adds CSRF token to all secure form requests|
|⚙️ Configure carefully|Disable CSRF **only** for safe, public routes|

---

## 👀 What’s Next?

In the upcoming lecture, we will:

- **Implement this CSRF protection** into our Eazy School application
    
- Test how the application behaves with secured forms and protected endpoints
    

---

🙌 You now understand how to **defend your app against CSRF attacks** using Spring Security and Thymeleaf.  
See you in the next lecture! 🚀💻