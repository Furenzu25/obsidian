## 🔰 INTRODUCTION: Why Learn OOD Principles?

- **Design principles are timeless**: They're applicable across tools, frameworks, and languages.
    
- **Design is about tradeoffs**: These are **guidelines**, not absolute rules.
    
- Mastery of these principles makes it easier to adopt **new technologies** and write more **maintainable, extensible** code.
    

---

## 🧠 PREVIOUSLY DISCUSSED PRINCIPLES (Review)

1. **Favor Composition Over Inheritance**: Prefer "has-a" over "is-a".
    
2. **Liskov Substitution Principle (LSP)**: Subtypes must be substitutable for their base types.
    

---

## 🔎 CORE OBJECT-ORIENTED DESIGN PRINCIPLES

---

### 🟡 1. Information Expert

> **"The class that has the information should also have the behavior."**

- Most violated in enterprise systems.
    
- Promotes **high cohesion**.
    
- Related **code smells**:
    
    - Anemic Domain Model
        
    - Feature Envy
        
    - Shotgun Surgery
        

✅ **Application**: Place methods in the class that holds the related data.

---

### 🟡 2. Law of Demeter

> **"Don't talk to strangers."**

- A method should only interact with:
    
    - Itself
        
    - Its parameters
        
    - Objects it created
        
    - Its own fields
        
- Prevents **tight coupling**.
    
- Improves **modularity and maintainability**.
    

💬 **Key Quotes**:

> “Ask for help, not information.” — Allen Holub  
> “Maintainability is inversely proportional to data flow.” — James Gosling

👃 **Code smells**:

- Message Chains / Train Wrecks
    
- Feature Envy
    

✅ **Application**: Hide chains with helper methods like `hasConflict()`.

---

### 🟡 3. Single Responsibility Principle (SRP)

> **"A class should have only one reason to change."**

- Each class/method should do one thing.
    
- Improves **cohesion** and **readability**.
    
- The "S" in **S.O.L.I.D.**
    

👃 **Code smells**:

- Long Class
    
- Long Method
    
- Divergent Change
    
- “How” Comments
    

✅ **Application**: Split responsibilities across specialized classes.

---

### 🟡 4. Separation of Concerns

> **"Don’t mix architectural concerns."**

- Keep business logic separate from:
    
    - UI
        
    - Persistence
        
    - Security
        
    - Transactions
        
- Enables **flexibility** and **reuse**.
    

👃 **Code smells**:

- Divergent Change
    
- Large Classes
    
- Long Methods
    

✅ **Application**: Separate layers into services, repositories, controllers, etc.

---

### 🟡 5. Don’t Repeat Yourself (DRY)

> **"Every piece of knowledge must have a single, unambiguous representation in the system."**

- Encourages **reuse**, improves **maintainability**.
    

👃 **Code smells**:

- Duplicate Code
    
- Shotgun Surgery
    

✅ **Application**: Extract shared logic into reusable methods or services.

---

### 🟡 6. Protected Variations

> **"Anticipate changes by protecting them with stable interfaces."**

- Keep **variation points** behind **stable abstractions**.
    
- Prevent ripple effects from changing business rules or policies.
    

🔁 **Use Case Example**:  
Invoice generation logic evolves:

- Initially: `generateInvoice(items)`
    
- Later: add VAT → `generateInvoiceWithVat()`
    
- Later: senior discounts → `generateInvoiceWithSeniorDiscount()`
    
- Results in messy, duplicated logic in multiple clients.
    

✅ **Solution**:

- Consolidate logic behind one method:
    
    java
    
    CopyEdit
    
    `Invoice generateInvoice(Customer customer, Collection<OrderItem> items)`
    
- Keep variation logic **internal** and **private**.
    

👃 **Code smells addressed**:

- Conditional Complexity
    
- Divergent Change
    

---

## 📦 PACKAGE-LEVEL DESIGN PRINCIPLES

### 📘 Package Cohesion Principles

1. **Common Reuse Principle (CRP)**
    

> Classes used together should be in the same package.  
> ✅ Example: Put custom exceptions with the services that throw them.

2. **Common Closure Principle (CCP)**
    

> Classes that change together should be packaged together.  
> ✅ Example: Interfaces and implementations should be in different packages if they change at different rates.

---

### 📘 Package Coupling Principles

1. **Acyclic Dependencies Principle (ADP)**
    

> Packages should not form dependency cycles.

2. **Stable Dependencies Principle (SDP)**
    

> Depend only on more stable (less frequently changing) packages.

✅ **Examples**:

- UI can depend on business logic (UI changes more).
    
- Business logic can depend on persistence (persistence changes less).
    

---

## 🎯 DESIGN GOAL: BALANCING COHESION AND ABSTRACTION

> “The goal of object-oriented design is to reduce cognitive load.”

- **Cohesion**: Keeping related data and logic together.
    
- **Abstraction**: Hiding details to reduce complexity.
    

🎯 Your job is to **balance** both to:

- Write **readable**, **extensible**, and **maintainable** software.
    
- Make code easier for **humans to understand**, not just computers to execute.
    

---

## ✅ FINAL SUMMARY TABLE

|Principle|Goal|Related Smells|Key Benefit|
|---|---|---|---|
|**Information Expert**|Put logic where data is|Feature Envy, Anemic Models|Cohesion|
|**Law of Demeter**|Avoid deep coupling|Message Chains|Encapsulation|
|**SRP**|One responsibility per class/method|Long Method, Divergent Change|Readability, Maintainability|
|**Separation of Concerns**|Separate architectural layers|Divergent Change|Flexibility|
|**DRY**|No duplicated logic|Duplicate Code|Maintainability|
|**Protected Variations**|Hide likely changes|Conditional Complexity|Scalability|
|**CRP/CCP**|Cohesive packaging|Shotgun Surgery|Logical Organization|
|**ADP/SDP**|Directional, stable dependencies|Package Cycles|Stability|