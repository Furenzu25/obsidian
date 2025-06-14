# 🧪 Introduction to Test-Driven Development (TDD) — Structured Study Notes

---

## 🚩 1. Why TDD?

### ❌ The Problem with Traditional Unit Testing

- Tightly coupled code is hard to test.
    
- Developers delay testing if code “works”.
    
- Retrofitting tests leads to incomplete, unreliable coverage.
    

---

## ✅ 2. The Solution: **Test First**

> “Think like the programmer who will call your code.”

### Key Benefits:

- **Promotes loose coupling**
    
- **Encourages interface-first design**
    
- **Improves testability and readability**
    
- **Leads to focused, goal-oriented development**
    
- Encourages **YAGNI** (You Ain’t Gonna Need It) and **DTSTTCPW** (Do The Simplest Thing That Could Possibly Work)
    

---

## 🔁 3. Test as You Code: The Rhythm of TDD

> Test a little... Code a little... Repeat.

### Core Development Loop:

1. Write a small, failing test.
    
2. Write the minimal code to make it pass.
    
3. Refactor mercilessly.
    
4. Repeat.
    

This cycle prevents overengineering and ensures feature-driven progress.

---

## 🔂 4. The **5 Steps of TDD** (One per Scenario)

|Step|Description|
|---|---|
|1️⃣|Write a failing **unit test**. This defines the desired behavior.|
|2️⃣|Run the test to confirm it fails (red).|
|3️⃣|Write just enough **production code** to make it pass (green).|
|4️⃣|Run the test again to confirm it passes.|
|5️⃣|**Refactor** the code to improve structure without changing behavior.|

> You gain confidence in refactoring because you have tests to prove behavior remains intact.

---

## 🧼 5. Refactoring: The **Boy Scout Rule**

> _“Leave the code cleaner than you found it.”_

Refactoring improves:

- Readability
    
- Maintainability
    
- Team productivity
    

### 🧰 Common Refactorings (From Martin Fowler’s Catalog):

- Rename method/variable
    
- Extract method/class
    
- Inline class/method
    
- Move field/method
    
- Pull up / Push down field/method
    

🔗 [Refactoring Catalog](https://www.refactoring.com/catalog/)

---

## 🔨 6. **Applying TDD to a Method**: Roman Numeral Exercise

### Requirements:

- Build a method that converts to Roman numerals.
    
- Use **TDD and refactoring principles** rather than maximizing test cases.
    
- Apply:
    
    - Java best practices
        
    - Clean method/class/variable naming
        
    - One test per scenario group (not per case)
        

⚠️ Avoid implementing algorithms found online — focus on your logic & TDD process.

---

## 💵 7. **TDD on a Class**: The `Money` Class Exercise

### Core Requirements:

1. Stores monetary value split into:
    
    - `int dollars`
        
    - `int cents`
        
2. Supports currencies: **PHP**, **USD**, **EUR**
    
3. Supports **negative values** (e.g., for debt)
    
4. `toString()` output formats:
    
    nginx
    
    CopyEdit
    
    `PHP 1.50, PHP -1.05, EUR 0.05`
    

---

### 🧮 Additional Functional Requirements

- Arithmetic: **Addition and subtraction** with other `Money` objects
    
    - ❗Throws exception on currency mismatch
        
- Proper `equals()` and `hashCode()` implementations
    

---

### 🚫 Extra Constraints (For Challenge):

- No use of `BigDecimal`
    
- Must store as **two separate integers**
    
- ❌ Cannot merge `dollars` and `cents` into a single number
    
- ❌ Cannot use `String.format(...)` for zero-padding
    

🔎 This enforces **precision**, **manual formatting**, and **deeper arithmetic logic**.

---

## 🔁 8. Summary Flow of TDD Practice
	
	java
	
`FOR EACH SCENARIO:     ↓ Write a failing test (assert expected behavior)     ↓ Write minimum code to pass the test     ↓ Run the test (GREEN)     ↓ Refactor and simplify (if needed)     ↓ Repeat`

---

## 🧠 9. Mindset Shift with TDD

### From:

- "I’ll write tests if I have time."
    
- "My code works, why test?"
    

### To:

- “Tests define what my code should do.”
    
- “Code is only correct if it passes my tests.”
    

### Benefits:

- Fewer regressions
    
- Safer refactoring
    
- Stronger confidence in changes
    
- Modular, testable, clean design
    

---

## ✅ 10. Final Takeaways

|🔥 Principle|🚀 Benefit|
|---|---|
|Test First|Ensures only needed code is written|
|Loosely Coupled Design|Promotes testability and maintainability|
|Small Iterations|Keeps development focused|
|Clean Code via Refactoring|Improves team velocity|
|Descriptive Tests|Become living documentation|

---

## 🧪 Exercises Summary (for Practice)

1. Implement a method using TDD (e.g., Roman numeral conversion).
    
2. Design a robust `Money` class using TDD.
    
    - Store values using two `int` fields.
        
    - Handle operations and constraints.
        
    - Ensure correct formatting without built-in helpers.