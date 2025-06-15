## 🧠 Recap: Building Web Applications with Spring Boot 🚀

Let's take a moment to reflect on what we've covered so far in our Spring Boot journey. This recap highlights the key concepts and technical steps in setting up a Java-based web application using **Spring Boot + Spring MVC**.

---

### 🏗️ What is a Web Application?

We started by understanding:

- The role of **Servlets** and **Servlet Containers** (e.g., Tomcat) in web development
    
- How Spring Boot simplifies development by abstracting away low-level details
    

---

### ⚙️ Spring Boot Project Setup

**Step 1: Scaffold the Project**

- Visit 🔗 [start.spring.io](https://start.spring.io)
    
- Choose **Maven** as the build tool
    
- Add dependencies like `spring-boot-starter-web`
    
- Download and import the project into **IntelliJ**
    

**Result**:  
Spring Boot provides:

- Folder structure
    
- Required dependencies
    
- Embedded Tomcat
    
- Auto-configuration ✨
    

---

### 🏁 Identifying the Main Class

The entry point of a Spring Boot application is marked with:

`java`

`@SpringBootApplication`

This annotation is a meta-annotation composed of:

1. **@EnableAutoConfiguration** – Enables Spring Boot’s auto configuration
    
2. **@ComponentScan** – Scans for classes annotated with `@Component`, `@Controller`, etc.
    
3. **@SpringBootConfiguration** – A variant of `@Configuration` for boot applications
    

📌 Note:  
If your custom components are outside the base package of the main class, manually specify them using `@ComponentScan(basePackages = "your.package")`.

---

### 🌐 Creating Web Routes

To define HTTP routes, we used:

`java`

`@RequestMapping("/home")`

This tells Spring MVC to call the mapped method whenever `/home` is hit, regardless of whether it's a GET or POST request.

- Though `@RequestMapping` is from Spring MVC, it's integrated seamlessly with Spring Boot when building MVC-style apps.
    

---

### 🛠️ Configuring Server Properties

We learned how to override default server settings in `application.properties`:

`properties`

`server.port=8081           # Custom port server.context-path=/app   # Custom context path server.port=0              # Let Spring Boot pick a random port`

---

### 📋 Auto-Configuration Insights

To _inspect auto-configuration decisions_, enable debug mode:

`properties`

`debug=true`

🧾 This allows you to view the auto-configuration report during application startup.

#### ⛔ Excluding Auto-Configurations

You can prevent specific configurations using:

`java`

`@SpringBootApplication(exclude = {SomeAutoConfiguration.class})`

---

### 🎯 Milestone Achieved!

You now understand:

- How to scaffold and run a Spring Boot web app
    
- Core Spring annotations
    
- HTTP routing with Spring MVC
    
- Customizing and controlling Spring Boot behavior
    

---

### ☕ Take a Well-Deserved Break 🎉

You've earned it! Grab your favorite coffee or tea, listen to some music, and recharge.  
See you in the next lecture. 👋