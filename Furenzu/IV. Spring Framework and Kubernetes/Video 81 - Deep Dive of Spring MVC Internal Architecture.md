## 🧠 Introduction to MVC Pattern

### 📌 MVC stands for:

- **M**odel — Represents the **data** or business objects.
    
- **V**iew — The **UI** part, like HTML/CSS/JS that the user sees.
    
- **C**ontroller — The **brain** that processes input, interacts with the model, and selects the view to render.
    

---

## 🏗️ Why MVC Pattern?

Before MVC (in early 2000s):

- Developers used **Servlets + JSP + JDBC** all in one file 😖.
    
- Business logic, UI code, and database code were **mixed together**, making changes hard and buggy.
    
- It was difficult to debug or enhance an application.
    

With MVC:

- Each component has a **separate responsibility**.
    
- Easy to maintain, enhance, and **debug** 🛠️.
    
- Encourages **loose coupling** 🔗 between logic, UI, and data.
    

---

## 🧬 Components of MVC

|Component|Responsibility|
|---|---|
|**Model**|Holds application data (like a `Student` object). Interacts with the database.|
|**View**|Displays data using HTML, CSS, JS. Receives data from the controller.|
|**Controller**|Processes requests, interacts with model, and returns a view.|

📌 Example: When a user wants to see student details:

1. Controller receives the request.
    
2. It fetches data from the Model.
    
3. Passes the data to the View to render as HTML.
    

---

## 🌐 Spring MVC Architecture (Internal Flow)

Understanding the **internal steps** of Spring MVC is **crucial** for interviews and real development.

### 🔁 Step-by-Step Flow:

1. **🧑‍💻 Client Request**
    
    - A user (from browser/mobile/desktop) makes an HTTP request like `/home`.
        
2. **📥 Tomcat Receives Request**
    
    - Tomcat (servlet container) converts the HTTP request into a **Servlet request**.
        
3. **📮 DispatcherServlet Handles It**
    
    - Acts as **Front Controller** 🚪.
        
    - Receives every web request and delegates it further.
        
4. **🧭 HandlerMapping**
    
    - Looks up which **controller & method** should handle the request.
        
    - Example: `/home` → `HomeController.displayHomePage()`.
        
5. **🎯 Controller Executes Logic**
    
    - Executes business logic.
        
    - Returns a **view name** like `"home.html"` and a **model** (data).
        
6. **🧩 ViewResolver Takes Over**
    
    - Resolves the logical view name to the **actual HTML template**.
        
    - Populates dynamic data from the model into the template.
        
7. **📤 DispatcherServlet Returns Response**
    
    - Takes the final HTML from ViewResolver and sends it back to Tomcat.
        
8. **🌐 Browser Displays Output**
    
    - Tomcat converts the servlet response into HTTP and sends it to the user.
        
    - User sees a fully rendered page with CSS/JS/HTML.
        

---

## 📦 Summary Table: Components in Action

|Component|Description|
|---|---|
|**DispatcherServlet**|Front controller. Handles all web requests.|
|**HandlerMapping**|Maps URLs to the right controller/method.|
|**Controller**|Executes business logic and returns view + model.|
|**ViewResolver**|Resolves the view and inserts model data into template.|
|**Tomcat**|Web server that handles HTTP <-> Servlet conversions.|

---

## 💡 Developer's Role in Spring MVC

As a Spring MVC developer, you **don’t need to define** DispatcherServlet or HandlerMapping manually. Spring handles it all!

Instead, your tasks are:

- ✅ Create **Controllers** with logic.
    
- ✅ Use `@RequestMapping` to define paths.
    
- ✅ Define **Views** (like `home.html`) for rendering.
    
- ✅ Use **Model** objects to pass data to the view.
    

📁 Example:

- `HomeController.java` → contains `@RequestMapping("/home")` method.
    
- `home.html` → the view template.
    
- `Student.java` → model with data.
    

---

## 🧠 Key Takeaways

✅ **MVC separates concerns**: View = UI, Controller = Logic, Model = Data.  
✅ Spring MVC uses **DispatcherServlet** as a **front controller**.  
✅ **Loose coupling** makes your code more maintainable and scalable.  
✅ Internals like HandlerMapping, ViewResolver are automatically handled.  
✅ Focus on writing clean **Controller**, **Model**, and **View** components.

---

## 🎓 Final Advice

- Spend time understanding the **Spring MVC flow diagram**.
    
- Practice explaining the flow step-by-step.
    
- Try building a sample app using Controller + Model + View.
    

🧑‍💻 Once you get this architecture, building complex Spring web apps becomes a breeze!

---

📚 _Next: Learn how to fetch real data from databases using model objects and display them in the view. Coming soon in the next lecture!_

![[Pasted image 20250615220402.png]]