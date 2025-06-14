# 📚 Study Notes: What is a Domain Model? & Machine Problem (JAVA-201)

---

## 🧩 1. What is a Domain Model?

A **Domain Model** represents **real-world business concepts** in code. It captures **entities**, **relationships**, and **rules** of a specific business domain.

> ✅ **Goal**: Make complex business logic more **understandable**, **maintainable**, and **communicable**.

---

## ❗ 2. The Core Problem

### Developers & Business Stakeholders Miscommunicate:

- They use **different terminology**.
    
- Knowledge is often **tribal**—lost when people leave.
    
- Business understanding doesn’t translate cleanly into code.
    

---

## 💡 3. The Solution: Ubiquitous Language

Create a **shared language** between developers and business experts by:

- Modeling code using the **language of the business**.
    
- Naming **classes**, **methods**, and **variables** after **business terms**.
    

> 🧠 “Code becomes documentation.”

---

## 🧱 4. Entities vs Value Objects

|Category|Entity|Value Object|
|---|---|---|
|Identity|Yes – identified by ID|No – identified by value|
|Equality|Based on ID|Based on all fields|
|Mutability|Often mutable|Preferably immutable|
|Usage|Mapped to DB rows|Interchangeable, replaceable|
|Copying|No defensive copy (DB-bound)|Defensive copy if mutable|

---

## 🏛️ 5. Hexagonal Architecture

The **Domain Model** is the **core** of the system.  
It is surrounded by:

- **Infrastructure** (databases, messaging)
    
- **UI** (web, mobile interfaces)
    

> 🔄 These outer layers depend on the core, **not vice versa**.

---

## ⚠️ 6. Why Modeling Right Matters

**Mistakes in Domain Model → Costly Fixes Later**

- Changing the model = altering **DB schema**.
    
- **Production migrations** are risky.
    
- Requires **blue-green deployments** or **downtime**.
    

> ✅ **Mitigation**: Understand the domain **deeply** before coding.

---

## 📚 7. Learn from Experts

- Consult experienced developers and domain experts.
    
- Use resources like:
    
    > _“The Data Model Resource Book”_  
    > A reference for common data models across domains.
    

---

## ⚖️ 8. When NOT to Use Domain Models

Avoid them when:

- Retrieving **massive datasets** (e.g., reports).
    
- Handling **batch jobs** (e.g., payroll).
    
- Performing **aggregations** or **filtering** (sum, count, where).
    

> ✅ Use **optimized SQL** or **CQRS pattern** for such cases.

---

## 🔁 9–11. TDD on Multiple Classes: University Enlistment Domain

### Domain Requirements:

#### 🧑‍🎓 Student:

- Identified by **non-negative student number**.
    
- Can **enlist** in multiple sections.
    

#### 📚 Section:

- Identified by **alphanumeric section ID**.
    
- Cannot be enlisted **twice** by the same student.
    
- Cannot conflict in **schedule**.
    

#### ⏰ Schedule:

- Days: Mon/Thu, Tue/Fri, Wed/Sat
    
- Periods: 8:30–10am, 10–11:30am … 4–5:30pm
    
- **Conflict** = Overlapping time & day.
    

#### 🏫 Room:

- Identified by **room name**.
    
- Has a **capacity**: Enlistment cannot exceed this.
    

---

## 👩‍🏫 16–17. Additional Requirements (Machine Problem)

- A section has exactly **one subject**.
    
- Subjects:
    
    - Identified by **Subject ID**
        
    - May have **prerequisites**
        
    - Have **units**
        
    - Can be **laboratory subjects**
        
- Student cannot enlist:
    
    - In **two sections** of the **same subject**
        
    - If **prerequisites** not completed
        
- Room cannot be shared for **conflicting schedules**
    
- Instructors:
    
    - Must be assigned to each section.
        
    - Cannot teach overlapping sections.
        
- Student can **cancel enlistment**
    
- **Assessment**: Cost computation
    
    - ₱2,000 per unit
        
    - ₱1,234.56 for lab subjects
        
    - ₱3,456.78 misc fee
        
    - +12% VAT
        

---

## 🧪 12. Running Multiple JUnit Tests in Eclipse

- Run all tests in `src/test/java`: Right-click → `Run As` → JUnit Test
    
- Run all tests in a **package** similarly
    

---

## 🔄 13. Version Control Best Practices

- **Commit early and often**
    
- Use **small, atomic commits**
    
- Write **descriptive messages**
    
- **Push and pull regularly**
    
- Run **tests before merging/pushing**
    
- Use a `.gitignore` to exclude:
    
    - `target/`
        
    - `.project`, `.classpath`, `.settings/`
        

> Suggested template: [GitHub Gist](https://gist.github.com/dedunumax/54e82214715e35439227)

---

## 🧠 18. No Best Practices — Only Trade-Offs

Software design is about **contextual decision-making**:

- Evaluate based on **business value**
    
- Consider **time, effort, cost**, and **maintainability**
    

> 🚫 “Best practice” is misleading. Design is **economics**, not dogma.

---

## 🧭 19. Recommended Next Steps

### For Developers:

- **Java Enterprise Development** (5 days)
    
    - Persistence, Concurrency, Web Layers
        

### For Managers:

- **Agile Software Development** (2 days)
    
    - Scrum, XP, Kanban
        

---

## ✅ Summary Checklist

|Concept|Core Idea|
|---|---|
|Domain Model|Code structure based on business entities & logic|
|Ubiquitous Language|Shared terms between devs & stakeholders|
|Entity vs Value Object|Identity vs interchangeable value containers|
|Hexagonal Architecture|Domain core, UI/infra as external layers|
|Domain Model Pitfalls|Hard to change once in production|
|Machine Problem Goals|Apply TDD on a real domain scenario|
|Git Best Practices|Clean, testable, well-documented version history|