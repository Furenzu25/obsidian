## 📘 Overview & Review of Object-Oriented Programming (JAVA-201)

---

### 🔸 1. Course Overview

- The course is Agile-focused, but emphasizes **Agile coding**, not just project management.
    
- Core practices:
    
    - **Object-Oriented Programming (OOP)**
        
    - **Test-Driven Development (TDD)**
        
    - **Refactoring**
        
- Contrast:
    
    - **School Programming**: Often solo, short-term, functionality-focused.
        
    - **Real-World Programming**: Collaborative, maintainable, and built for change.
        

---

### 🔸 2. Good Engineering Practices

- Agile development demands **shippable code every sprint**.
    
- Lacking technical discipline leads to failure even with Agile rituals in place.
    
- Real Agile = working code + sustainable design.
    

---

### 🔸 3. Technical Debt

- **Definition**: Poorly written code that makes future changes harder.
    
- Accumulates like **interest**—small issues compound over time.
    
- Impacts:
    
    - Slower onboarding
        
    - Harder debugging
        
    - Increased fragility
        
- **Solution**: Invest in good architecture, continuous refactoring, and clean code.


---

### 🔸 4. Abstraction

- **Concept**: Focus on **high-level behavior**, hiding the details.
    
- Benefits:
    
    - Reduces cognitive load
        
    - Allows building reusable components
        
- Examples:
    
    - Functions: Encapsulate routines
        
    - Structs/Objects: Group data and behaviors
        
    - OO Abstraction: Each object is a self-contained unit with logic + state
        

---

### 🔸 5. Objects

- **Definition**: Bundles of data (state) and related behavior (methods).
    
- Modeled using **classes** as templates.
    
- Promote modularity and real-world modeling (e.g. `Student`, `BankAccount`).
    

---

### 🔸 6. Interface

- **Public face of an object**: the methods and properties accessible from outside.
    
- Best practices:
    
    - Simple and easy to understand
        
    - Avoid invalid states (limit public setters)
        
    - Minimize changes (design for stability)
        
- Validation and logic should happen **within** methods, not outside.
    

---

### 🔸 7. Encapsulation

- **Hiding internal state and logic**, exposing only necessary parts.
    
- Prevents misuse and unintended side effects.
    
- Leads to:
    
    - More reliable components
        
    - Simpler APIs
        
    - Increased task separation
        

---

### 🔸 8. Composition & Delegation

- **Composition**: Build complex systems by combining simpler components.
    
- **Delegation**: Assign responsibility to specialized objects.
    
- Promotes:
    
    - High cohesion (each class does one thing well)
        
    - Separation of concerns
        
    - Code reuse and flexibility
        
- **Prefer composition over inheritance** whenever possible.
    

---

### 🔸 9. Inheritance

- Allows a class to acquire properties and methods from another class.
    
- Useful for:
    
    - Modeling real-world hierarchies
        
    - Sharing behavior across related classes
        
- **Dangers**:
    
    - Fragile base class problem
        
    - Refused bequest
        
    - Deep inheritance hierarchies = complex maintenance
        
- Use sparingly and carefully.
    

---

### 🔸 10. Polymorphism

- Enables **interchangeable behavior** using different object types.
    
- Achieved via:
    
    - **Interfaces** (preferred)
        
    - **Inheritance**
        
- Benefits:
    
    - Cleaner code with fewer conditionals
        
    - Easier extension
        
    - Greater flexibility and decoupling
        
- Example: A method accepting any type of `InputStream`, not just `FileInputStream`.
    

---

### 🔸 11. Liskov Substitution Principle (LSP)

- Subtypes must behave **consistently** with the behavior of their parent type.
    
- Violations (like `Square` inheriting from `Rectangle`) cause bugs and confusion.
    
- Solutions:
    
    - Refactor hierarchy
        
    - Use composition instead
        
    - Make fields immutable when necessary
        

---

### 🔸 Design Principles Reinforced

- **Design by Contract**: Subtypes must honor behavior contracts of base types.
    
- **Principle of Least Surprise**: Code should behave predictably and intuitively.