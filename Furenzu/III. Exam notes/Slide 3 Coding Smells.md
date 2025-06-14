## 🧠 **Comprehensive Study Notes: Code Smells (JAVA-201)**

### 🔰 INTRODUCTION TO CODE SMELLS

- **Definition**: A code smell is a _surface symptom_ of a deeper design flaw. Coined by **Martin Fowler**.
    
- **Purpose**: Naming code smells allows developers to:
    
    - Identify poor design more effectively.
        
    - Improve communication and refactoring strategies.
        
- Common across Agile and Object-Oriented systems.
    

---

## 📌 CATEGORIES & SOLUTIONS TO COMMON CODE SMELLS

---

### 🟠 **1. Duplicate Behavior (Duplicate Code)**

**Symptoms**:

- Copy-paste code reused with slight variations.
    
- Maintenance becomes scattered and error-prone.
    

**Solutions**:

- Apply **DRY (Don’t Repeat Yourself)** principle.
    
- Use:
    
    - **Methods** for reuse.
        
    - **Polymorphism** or **parameters** for variation.
        
    - **Composition/Inheritance** when appropriate.
        

---

### 🟠 **2. Long Methods & Large Classes**

**Symptoms**:

- Difficult to read, scroll-heavy code.
    
- Classes with too many fields or vague names.
    

**Solutions**:

- Follow **Single Responsibility Principle (SRP)**.
    
- Break into smaller:
    
    - **Methods** (one clear purpose, no side effects).
        
    - **Classes** (high cohesion, narrow responsibilities).
        

---

### 🟠 **3. Primitive Obsession, Data Clumps & Long Parameter Lists**

**Symptoms**:

- Using primitives instead of modeling domain concepts (e.g., `int id` instead of a `Customer`).
    
- Repeated groups of related variables (Data Clumps).
    
- Long, hard-to-read method parameter lists.
    

**Solutions**:

- Encapsulate related fields into **domain-specific classes**.
    
- Move methods into classes where the data belongs (**cohesion**).
    
- Eliminate long parameter lists by passing **objects**.
    

---

### 🟠 **4. Divergent Change**

**Symptoms**:

- One class changes for different unrelated reasons.
    
- Mixes business logic, persistence, and UI logic.
    

**Solution**:

- Apply **Separation of Concerns**.
    
- Split responsibilities into separate, specialized classes.
    

---

### 🟠 **5. Shotgun Surgery**

**Symptoms**:

- One change requires edits in many classes.
    
- Opposite of Divergent Change.
    

**Solution**:

- Increase **cohesion**.
    
- Group changing parts into a single class/module.
    
- “Things that change together should live together.”
    

---

### 🟠 **6. Feature Envy**

**Symptoms**:

- Methods constantly accessing fields of other classes.
    

**Solution**:

- Move the method to the class it depends on.
    
- Enforce **object encapsulation**.
    

---

### 🟠 **7. Conditional Complexity**

**Symptoms**:

- Overuse of `if-else` or `switch` logic.
    
- Difficult to scale and maintain.
    

**Solutions**:

- Use **Polymorphism** to separate behavior.
    
- Apply **Strategy Pattern** or **State Pattern**.
    

---

### 🟠 **8. Parallel Inheritance Hierarchies**

**Symptoms**:

- For every class in one hierarchy, there’s a corresponding class in another (e.g., `Customer` → `CustomerService`).
    

**Solution**:

- Collapse hierarchies.
    
- Consolidate logic into fewer, more cohesive classes.
    

---

### 🟠 **9. Lazy Class, Middle Man, Dead Code**

**Symptoms**:

- Classes that:
    
    - Do too little (`Lazy Class`)
        
    - Just delegate (`Middle Man`)
        
    - Are never used (`Dead Code`)
        

**Solution**:

- Eliminate unnecessary code.
    
- Inline behaviors or merge classes as needed.
    

---

### 🟠 **10. Alternative Classes with Different Interfaces**

**Symptoms**:

- Similar classes with different interfaces, leading to `if-else` logic.
    

**Solution**:

- Introduce a **common interface**.
    
- Use **polymorphism** for flexibility and scalability.
    

---

### 🟠 **11. Data Class / Anemic Domain Model**

**Symptoms**:

- Classes contain only fields and getters/setters.
    
- Business logic lies _outside_ the data object.
    
- Leads to broken **encapsulation** and invalid states.
    

**Solution**:

- Implement **Rich Domain Model**:
    
    - Move behavior into the class.
        
    - Validate inside the methods.
        
    - Remove unnecessary accessors.
        

---

### 🟠 **12. Refused Bequest**

**Symptoms**:

- A subclass inherits methods it doesn’t use or shouldn't use.
    

**Solution**:

- **Favor composition over inheritance**.
    
- Eliminate or encapsulate unused members.
    

---

### 🟠 **13. Speculative Generality**

**Symptoms**:

- Over-engineering for “future flexibility.”
    
- Includes unused parameters, interfaces, subtypes.
    

**Solution**:

- Apply **YAGNI**: “You Ain’t Gonna Need It”.
    
- Keep it simple: **DTSTTCPW** – Do The Simplest Thing That Could Possibly Work.
    

---

### 🟠 **14. God Class / God Method**

**Symptoms**:

- All logic centralized in one class or method.
    

**Solutions**:

- Apply:
    
    - **Single Responsibility Principle**
        
    - **Information Expert**
        
    - **Law of Demeter**
        

---

### 🟠 **15. Temporary Field**

**Symptoms**:

- Fields used temporarily within a method.
    

**Solution**:

- Use **local variables** instead.
    
- If grouped, encapsulate in a helper class.
    

---

### 🟠 **16. Message Chains / Train Wrecks**

**Symptoms**:

- Chaining multiple method calls to navigate nested objects (e.g. `a.b().c().d()`).
    

**Solution**:

- Apply **Law of Demeter**.
    
- Use intermediary methods like `hasConflict()`.
    
- Improves encapsulation and readability.
    

---

### 🟠 **17. “How” Comments**

**Symptoms**:

- Comments explain _how_ code works.
    
- Indicates unreadable code.
    

**Solutions**:

- Refactor code to be self-explanatory.
    
    - Use **descriptive method/variable names**.
        
    - Replace **magic numbers** with constants.
        
- Preserve “why” comments (e.g., regulations, constraints).
    

---

### 🟠 **18. Flag Arguments**

**Symptoms**:

- Boolean parameters change method behavior (`login(creds, true)`).
    

**Solutions**:

- Extract separate methods (`adminLogin()`, `userLogin()`).
    
- Use **enums** or **strategy pattern** for clarity and flexibility.
    

---

## ✅ BEST PRACTICES SUMMARY

| Problem Category       | Core Solution Principle          |
| ---------------------- | -------------------------------- |
| Duplication            | DRY, Refactor to Methods         |
| Large Methods/Classes  | SRP, Extract Classes/Methods     |
| Long Parameter Lists   | Encapsulation, Cohesion          |
| Scattered Changes      | Group Related Behaviors          |
| Excessive Conditions   | Polymorphism, Strategy Pattern   |
| Messy Interfaces       | Common Interface, Clean API      |
| Misused Inheritance    | Favor Composition                |
| Premature Abstractions | YAGNI, Simplicity                |
| Code Readability       | Naming, Refactoring, Constants   |
| Logic Outside Data     | Rich Domain Model, Encapsulation |


## 📦 **On Packages in the Context of Code Smells**

### 🔸 Mention in the Slides:

Packages are directly discussed under the **“Shotgun Surgery”** section (Slide 16), with this key insight:

> “Things that change together should be together.  
> Also applies to **packages** — classes that change together should be in the same package.”

### 🔸 Related Principle: **Package Cohesion**

Just as **class cohesion** deals with grouping related behaviors and data in one class, **package cohesion** deals with organizing related classes:

- If classes frequently change for the same reasons, they **belong together in one package**.
    
- Otherwise, splitting them across unrelated packages causes:
    
    - **Scattered changes**
        
    - **Increased fragility**
        
    - **Violation of Separation of Concerns at the module level**
        

---

### ✅ Best Practices on Packages (from context & implication):

|Scenario|Best Practice|
|---|---|
|Classes are tightly coupled logically or behaviorally|Group into the same package|
|Only grouped by technical function (e.g. `util`, `service`, `impl`)|Refactor based on domain-driven design instead|
|Changes to one class require changes in another|Move them to the same package to improve locality|
|Class is reused across many unrelated packages|Consider creating a shared core or domain package|
|Parallel Inheritance Hierarchies (e.g. `Customer`, `CustomerService`)|Collapse packages if duplication exists|

---

### 🔸 You Can Think of a “Package Smell” If:

- **Changes ripple across many packages** for a single feature change.
    
- Packages are named generically but are full of unrelated classes.
    
- There’s **tight coupling between packages** when it should be internal to a class or submodule.
    

---

### 🧭 Design Rule Reinforced:

> **"High cohesion and low coupling applies to packages, too."**