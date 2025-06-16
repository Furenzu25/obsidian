# 🛡️ Study Notes: Understanding CSRF (Cross-Site Request Forgery) in Spring Security

---

## 🔍 What is CSRF?

**CSRF (Cross-Site Request Forgery)** is a security vulnerability where:

> 🚨 A malicious site tricks a user's browser into performing **unauthorized actions** on a trusted website where the user is already authenticated.

---

## 🧠 Real-World Analogy:

Imagine you're logged in to your **bank website**, and in another browser tab, you visit a **malicious website**. Without your knowledge, this second site submits a form to the bank to **transfer money** — using your session.

This is exactly what CSRF does. It uses your **active session/token** to send **forged requests**.

---

## 🕵️ CSRF Attack Flow (Step-by-Step Example)

Let’s say you’re logged in to **Netflix.com**, and you then visit **evil.com** (a hacker site).

### 🔐 Step 1: Login and Token Creation

- You log in to `Netflix.com` ✅
    
- The **backend generates an access token (e.g., JSESSIONID)** and stores it in your **browser's cookies** (specific to the domain).
    

### 🧪 Demo:

- In DevTools → `Application` tab → Cookies → `JSESSIONID` token visible.
    
- When you log in, the token value **changes** and is now sent with all future requests automatically.
    

---

### 🧨 Step 2: Visit Evil.com

- You open another tab and visit `evil.com`.
    
- Evil.com shows a tempting link:  
    👉 _“🔥 90% Off on iPhones – Click Now!”_
    

---

### 🧟 Step 3: The Trap is Triggered

- You **click the link**.
    
- Behind the scenes, a **hidden HTML form** is submitted:
    
	    html
	
	    <form action="https://netflix.com/change-email" method="POST" id="form">     <input type="hidden" name="email" value="hacker@evil.com"> </form> <script>document.getElementById('form').submit();</script>
    
- Since you're still logged into Netflix:
    
    - Your browser automatically includes the **valid cookie/token**.
        
    - Netflix's backend **trusts** this request.
        
    - ✅ Email address gets changed — **without your knowledge or consent**!
        

---

## 🤯 Why This Happens?

Browsers **automatically attach cookies** to requests for the same domain, regardless of **which tab or website** triggered them.

So Netflix backend can’t tell:

- If the request came from _you_ or
    
- From _a malicious script in another site_.
    

---

## 🚫 Why Disabling CSRF Is Dangerous

You may have temporarily disabled CSRF protection in development for convenience (e.g., on a public Contact page), but:

- ✅ Okay for _non-secured_, anonymous endpoints
    
- ❌ NOT safe for _secured_ endpoints (like Dashboards, Profile Updates, Admin Actions, etc.)
    

---

## ⚠️ Key CSRF Characteristics

|🔐 Concept|💡 Description|
|---|---|
|🌐 Cross-site|Request is made from a different **origin** (evil.com → netflix.com)|
|🎭 Forgery|Hacker _impersonates_ the legitimate user using their session credentials|
|🔁 Automatic behavior|Browser sends cookies with every request to the matching domain|
|👨‍💻 Victim’s awareness|Victim remains **unaware**; actions happen behind the scenes|

---

## 🏁 Historical Context

- CSRF was **very common** in the 2000s and early 2010s.
    
- Now, modern frameworks like **Spring Security** provide **built-in defenses**.
    
- Industry has realized how dangerous CSRF can be and now **treats it as a must-defend threat**.
    

---

## ✅ Summary

|✅ What You Learned|💡 Takeaway|
|---|---|
|🔐 What CSRF Is|A form of attack that performs unauthorized actions using a valid session|
|📋 How It Works|The browser sends a valid session cookie with a forged request|
|🧪 Real Example|Clicking a malicious link changes Netflix account email without login again|
|❌ Why Disabling CSRF Is Dangerous|Makes sensitive POST/PUT endpoints vulnerable to exploitation|
|🛡️ Spring Security’s Role|Helps mitigate CSRF through token-based protection and configuration|

---

## 🔜 Coming Next

➡️ **How to properly enable and implement CSRF protection** using **Spring Security** and **Thymeleaf**.

---

🙌 Stay secure, code smart, and protect your users!  
📚 _See you in the next lecture! Bye! 👋_