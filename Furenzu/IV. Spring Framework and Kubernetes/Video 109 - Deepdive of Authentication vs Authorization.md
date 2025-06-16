# 🔐 Study Notes: **Authentication vs. Authorization in Spring Security**

---

## 📌 Introduction

In building a secure web application using **Spring Security**, it's critical to understand two key concepts that often confuse developers:

- ✅ **Authentication**
    
- ✅ **Authorization**
    

These two are **not the same** but are tightly connected.

---

## 🆔 What is **Authentication**?

Authentication is all about **identifying** _who_ the user is.

### 🔍 Purpose:

- To **prove the identity** of the user trying to access the application.
    
- This typically happens through:
    
    - 🧑 Username & Password
        
    - 📧 Email ID
        
    - 📱 OTP
        
    - 🔐 Biometric, etc.
        

### 💡 Real-World Analogy:

- 🏢 At your office, you **show your ID badge** or swipe it to get inside. This **confirms you are an employee**. That’s authentication.
    

---

## 🎫 What is **Authorization**?

Authorization is about **what you are allowed to do** _after_ you are authenticated.

### 🔒 Purpose:

- Once you're logged in, the system checks **your role or permissions**.
    
- It decides what features or pages you can access:
    
    - 👨‍🎓 _Student_: Can view profile and enrolled courses.
        
    - 🧑‍💼 _Admin_: Can manage students and create courses.
        

### 💡 Real-World Analogy:

- 🛫 At an airport, your **boarding pass** (authorization) lets you on **only the flight you booked**, not others. Even though you've been authenticated at the entrance, you’re only **authorized** for your specific destination.
    

---

## 🔄 Key Differences Between Authentication & Authorization

|Feature|Authentication|Authorization|
|---|---|---|
|✅ **Definition**|Verifies _who you are_|Defines _what you can access_|
|🔢 **Sequence**|Happens **first**|Happens **after** authentication|
|📝 **Data Needed**|Credentials (username, password, OTP)|Roles or authorities (admin, student, etc.)|
|🚫 **Failure Response**|❌ HTTP `401 Unauthorized`|❌ HTTP `403 Forbidden`|
|🧭 **Purpose**|Entry check into the system|Access control **inside** the system|
|🔐 **Real-world Example**|Showing ID to enter office|Using ID to access only permitted rooms|

---

## 📋 Summary

|Concept|Description|
|---|---|
|🆔 **Authentication**|"Who are you?" Prove identity with credentials.|
|🎫 **Authorization**|"What are you allowed to do?" Role-based access control.|
|🛑 **401 Error**|Authentication failed – user not recognized.|
|🛑 **403 Error**|Authorization failed – access denied due to insufficient permissions.|

---

## 📦 In the Context of Spring Security

Spring Security helps you:

- ✅ Define users and their roles.
    
- ✅ Protect routes, endpoints, and views.
    
- ✅ Handle login, logout, and session management.
    
- ✅ Guard against common vulnerabilities.
    

You'll learn how to:

- Set up **user roles** like `ROLE_STUDENT`, `ROLE_ADMIN`.
    
- Protect specific pages using **authorization rules**.
    
- Provide a custom **login page** and secure your entire app!
    

---

## 🧠 Final Thought

> **Authentication** is about proving your identity.  
> **Authorization** is about knowing your limits.

Together, they form the foundation of any secure system 🔐.