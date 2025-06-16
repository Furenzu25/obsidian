# 📘 Study Notes: Server-Side Validations using Bean Validation in Spring Boot 🛡️

---

## 🧠 Why Server-Side Validations Matter

Validations are a **critical part of any web application**. They ensure data correctness, prevent malicious input, and improve reliability.

⚠️ **Never rely solely on client-side validations** (like JavaScript or HTML5 constraints). These can be bypassed easily.

✅ **Always enforce validations on the server** to maintain data integrity.

---

## 🌱 What Is Bean Validation?

Bean Validation is a **standard Java-based approach** to apply validations on Java classes, especially POJOs (Plain Old Java Objects).

- Beans = Java classes that carry data (aka models or DTOs).
    
- With **Bean Validation**, we apply constraints (rules) directly to fields or methods using **annotations**.
    
- These validations occur **before the business logic** runs.
    

📌 **Standard Name**: Jakarta Bean Validation (formerly Javax Bean Validation)

---

## 🔍 Who Maintains It?

- Originally part of **Java EE (Enterprise Edition)**.
    
- Now maintained by the **Jakarta EE community**.
    
- Adopted widely across Java frameworks like **Spring Boot, Hibernate, JSF, etc.**
    

👀 Funny side note: The official logo shows Java’s Duke mascot inspecting a "bean" for issues — fitting, right? 😄

---

## 📦 How to Enable Bean Validation in Spring Boot

To use it in a Spring Boot project:

1. Add the **Spring Boot Starter Validation** dependency:
    

		xml

	`<dependency>     <groupId>org.springframework.boot</groupId>     <artifactId>spring-boot-starter-validation</artifactId> </dependency>`

2. Annotate your model (bean) fields with the appropriate constraints (e.g., `@NotNull`, `@Email`).
    
3. Use `@Valid` annotation in your **controller methods** to trigger validation when a form is submitted.
    

---

## ✨ Example: Validating a User Object

	java

	public class User {     @NotNull     @Email     private String email; }

- `@NotNull`: Email must not be `null`.
    
- `@Email`: Must follow a valid email format (e.g., `user@example.com`).
    

---

## 📋 Important Annotation Packages

### ✅ 1. Jakarta Bean Validation (formerly Javax)

Package: `jakarta.validation.constraints`  
(Old versions may use `javax.validation.constraints`)

Common annotations:

|Annotation|Purpose|
|---|---|
|`@NotNull`|Field must not be `null`|
|`@NotEmpty`|Field must not be empty (`""`)|
|`@NotBlank`|Field must not be just whitespace|
|`@Email`|Validates email format|
|`@Size`|Sets min and max length (e.g., for strings)|
|`@Pattern`|Validates string against regex pattern|
|`@Digits`|Restricts to digits only (no letters)|
|`@Max`, `@Min`|Sets numeric boundaries|

---

### 🔧 2. Hibernate Validator (extension of Jakarta)

Package: `org.hibernate.validator.constraints`

Extra annotations:

|Annotation|Purpose|
|---|---|
|`@Length`|Alternative to `@Size` for string length|
|`@Range`|Sets a numeric range|
|`@CreditCardNumber`|Validates credit card formats|
|`@URL`|Validates URL structure|
|`@Currency`|Validates currency format|
|`@UniqueElements`|Ensures collection values are unique|
|`@EAN`, `@ISBN`|Validates book/article codes|

---

## 🛠 Applying Validations in Controller

Use the `@Valid` annotation to trigger validation logic inside your controllers:

	java

	@PostMapping("/submit") public String handleForm(@Valid @ModelAttribute Contact contact, BindingResult result) {     if (result.hasErrors()) {         return "contact-form"; // Redisplay form with errors     }     // Proceed with business logic }

---

## 📅 Version Note: Javax vs Jakarta

- **Old Versions** (Java < 17): Use `javax.validation.constraints`
    
- **New Versions** (Java 17+): Use `jakarta.validation.constraints`
    

🔁 This change occurred because **Jakarta EE** took over Java EE, hence the package rename.

---

## ✅ Summary

|Topic|Description|
|---|---|
|**Bean Validation**|Standard method of validating Java objects (beans)|
|**Where to Use**|POJO fields, controller methods|
|**Annotations**|`@NotNull`, `@Email`, `@Size`, `@Pattern`, etc.|
|**Trigger Validations**|Use `@Valid` in controllers|
|**Starter Dependency**|`spring-boot-starter-validation`|
|**Two Libraries**|Jakarta + Hibernate Validator|
|**Version Note**|Javax (older) → Jakarta (Java 17+)|

---

## 🔜 Coming Up Next

In the **next lecture**, we’ll implement these validations in the **Contact page** of the Eazy School web app — ensuring clean, validated, and reliable input from users! 🏫✨

---

Thanks for reading!  
You're now ready to write solid, validated Java web apps with confidence. 🚀🧑‍💻  
See you in the next lecture! 👋