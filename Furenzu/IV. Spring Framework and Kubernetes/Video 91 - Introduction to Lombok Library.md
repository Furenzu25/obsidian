# 📘 Study Notes: Reducing Boilerplate Code in Java with Lombok 🚀

---

## ⚠️ The Problem with Plain Java POJOs

In a typical Java application, when we define a **POJO (Plain Old Java Object)** class:

- We manually add:
    
    - 🔁 Getters
        
    - 📝 Setters
        
    - 🔧 Constructors
        
    - 🧾 `toString()`, `equals()`, `hashCode()` methods
        
- This results in **a lot of repetitive code** — especially in large projects with hundreds or thousands of model classes.
    
- Even though IDEs can generate these methods automatically, they still clutter the source code and require maintenance over time 😩.
    

### 📁 Example:

	java

	public class Contact {   private String name;   private String email;   private String phone;    // You'd manually add or generate getters, setters, etc. }

---

## 💡 Enter **Lombok**: The Magic Wand for Java Developers 🪄

### 🌱 What is Lombok?

- **Lombok** is a **Java library** (not specific to Spring or Spring Boot) that helps eliminate boilerplate code.
    
- It works by **generating code at compile time** — methods are injected into the `.class` bytecode, not shown in the source `.java` file.
    
- This keeps your codebase **clean**, **maintainable**, and **easy to read** 🧼.
    

---

## 🧩 How Lombok Works

1. ✅ Add **Lombok dependency** to your project (via Maven or Gradle).
    
2. ✅ Annotate your POJO classes with **Lombok annotations** like `@Getter`, `@Setter`, `@Data`, etc.
    
3. ✅ Compile the code.
    
4. 🧠 During the build:
    
    - Lombok **injects methods into the class bytecode**.
        
    - The JVM can call these methods even though you don’t see them in your `.java` file.
        
    - IDEs like IntelliJ or Eclipse still recognize them, so you can use autocomplete, outlines, etc.
        

---

## 🔖 Common Lombok Annotations and Their Use Cases

|Annotation|Description|
|---|---|
|`@Getter`|Generates **getter methods** for all fields.|
|`@Setter`|Generates **setter methods** for all fields.|
|`@NoArgsConstructor`|Generates a constructor with **no arguments**.|
|`@RequiredArgsConstructor`|Generates a constructor for **final or non-null fields** only.|
|`@AllArgsConstructor`|Generates a constructor with **all fields** as parameters.|
|`@ToString`|Generates the **`toString()`** method.|
|`@EqualsAndHashCode`|Generates **`equals()` and `hashCode()`** methods.|
|`@Data`|A **combo annotation**: Includes `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode`, and `@RequiredArgsConstructor`. ✅ Most commonly used!|

---

## ✨ Example With Lombok

Without Lombok 👎:

	java

	public class Contact {   private String name;   private String email;   private String message;    // Getters, setters, constructors, toString(), etc. }

With Lombok 👍:

	java

	import lombok.Data;  @Data public class Contact {   private String name;   private String email;   private String message; }

✅ Result:

- Cleaner and easier to read.
    
- All necessary methods are generated behind the scenes.
    
- IDEs will still let you access these methods as if they were manually written.
    

---

## 🧠 Behind the Scenes: What Happens?

- You **won’t see** getters, setters, or constructors in your `.java` file.
    
- But they will be **visible in the IDE class outline** or when you inspect the compiled `.class` file.
    
- Lombok adds them during the **build/compile phase** — not at runtime.
    
- The **JVM will still recognize** these methods because they exist in the bytecode 🔍.
    

---

## 📦 Why Use Lombok?

✔️ Removes clutter from your Java classes.  
✔️ Saves time writing repetitive code.  
✔️ Helps maintain clean architecture.  
✔️ Reduces chances of human error in boilerplate methods.  
✔️ Boosts productivity for developers 🧑‍💻.

---

## 🔚 Conclusion

- Lombok is a powerful tool for simplifying Java development, especially in applications with many POJO classes.
    
- Use annotations like `@Data`, `@Getter`, `@Setter`, etc., to reduce your workload and improve code clarity.
    
- In the next lecture, you’ll implement Lombok in your **Eazy School web application**.
    

🔔 **Reminder**: Lombok is just a **compile-time helper** — it doesn’t affect your application’s runtime performance or behavior.

---

👋 Thanks for reading!  
🎯 Next: Let’s implement Lombok and clean up our model classes in Eazy School 🚀