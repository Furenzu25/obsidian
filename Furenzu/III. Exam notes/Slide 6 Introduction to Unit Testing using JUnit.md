# 🧪 Introduction to Unit Testing with JUnit – Structured Study Notes

---

## 📌 1. What Is JUnit?

- **JUnit** is the most widely used unit testing framework in Java.
    
- Written by Kent Beck and Eric Gamma, inspired by **SUnit** for Smalltalk.
    
- First released around **2000**, it now supports Java’s modern testing ecosystem via **JUnit 5** (Jupiter API).
    

📝 **Key Stats:**

- Used in ~64% of Java projects (GitHub metrics).
    
- Commonly integrated into tools like Maven, Gradle, and IDEs (Eclipse, IntelliJ).
    

---

## 🏗️ 2. Project Structure for Unit Testing

A typical Gradle/Maven project structure:
	
	bash
	
`src/  ├── main/java        # Production code  └── test/java        # Unit tests`

🧩 Ensure that both source and test classes are under the **same package** structure for proper recognition.

---

## 🔍 3. Creating a Unit Test

### ✏️ Step-by-Step (Testing `MathStuff.gcf()`):

1. **Class Under Test**:
    
    java
    
    `class MathStuff {     int gcf(int x, int y) {         return abs((y == 0) ? x : gcf(y, x % y)); // Euclid's Algorithm     } }`
    
2. **Test Class Setup**:
    
    java
	
    `import org.junit.jupiter.api.Test; import static org.junit.jupiter.api.Assertions.*;  class MathStuffTest {     @Test     void gcf_both_args_positive_and_same_value() {         int x = 5, y = 5, expected = 5;         int actual = new MathStuff().gcf(x, y);         assertEquals(expected, actual);     } }`
    

🧠 **Tip:** Test method names should be descriptive to serve as live documentation.

---

## 🛠️ 4. Running Tests

- In **IDE**: Click green triangle beside method/class.
    
- In **Gradle/Maven**: Run `mvn test` or `./gradlew test`.
    

📦 Maven also allows:

- Cross-environment execution.
    
- CI pipeline integration (e.g., Jenkins).
    

---

## 🧪 5. Testing Techniques and Best Practices

### ✅ Assertion Methods:

From `org.junit.jupiter.api.Assertions`:

- `assertEquals(expected, actual)`
    
- `assertTrue(condition)`
    
- `assertThrows(Exception.class, lambda)`
    
- `assertAll(...)`, `assertArrayEquals(...)`, etc.
    

🧠 Use static imports for cleaner syntax.

---

## 🧭 6. Principles: DRY vs DAMP in Tests

- ❌ DRY (Don't Repeat Yourself) is important in **production**.
    
- ✅ **DAMP (Descriptive And Meaningful Phrases)** is encouraged in **tests**.
    
    - Repeat values if it increases clarity.
        
    - Prioritize readability and explicit context.
        

---

## 🔥 7. Testing Exceptional Behavior

### Example: `BankAccount.withdraw()`
	
	java
	
`void withdraw(BigDecimal amount) {     if (amount == null)         throw new IllegalArgumentException("Amount parameter was null.");     if (amount.signum() < 0)         throw new IllegalArgumentException("Amount parameter was negative: " + amount);     ... }`

#### ✅ Test with assertThrows and message inspection:
	
	java
	
`@Test void withdraw_negative() {     BankAccount acct = new BankAccount(new BigDecimal("10000.00"));     Exception e = assertThrows(IllegalArgumentException.class,         () -> acct.withdraw(new BigDecimal("-1")));     assertTrue(e.getMessage().startsWith("Amount parameter was negative: ")); }`

---

## 📄 8. Testing Methods That Throw Checked Exceptions

### Problem:
	
	java
	
`String readFromFile() throws IOException;`

### 🛠 Solution:

- Avoid catching exceptions in test methods.
    
- Use `throws Exception` in test method signature. (✅ Valid in test, ❌ Avoid in prod)
    
	java
	
`@Test void readFromFile_exists_not_locked() throws Exception {     String result = new WorkWithFile("TestFile.txt").readFromFile();     assertEquals("some initial text", result); }`

---

## ♻️ 9. Ensuring Test Independence

### 🧼 Problem:

Tests may **interfere** with each other if state (e.g., files, DB) is shared.

### ✅ Solution:

- Use `@BeforeEach` to **set up** consistent preconditions.
    
- Use `@AfterEach` to **clean up** resources.
    
	java
	
`@BeforeEach void createTestFile() throws Exception {     Writer writer = new FileWriter("TestFile.txt");     writer.write("some initial text");     writer.close(); }  @AfterEach void deleteTestFile() throws Exception {     new File("TestFile.txt").delete(); }`

🔐 Ensures **repeatable, isolated, and reliable** tests.

---

## 📚 10. Additional Guidelines

### ❌ Do Not:

- Test obvious behaviors (e.g., trivial getters/setters).
    
- Leave tests that fail unattended.
    
- Let one broken test cascade into many.
    

### ✅ Do:

- Have **developers write tests** for their own code.
    
- **Run tests after every change** (pull, merge, commit).
    
- Store tests in **version control**.
    
- Make tests **environment-agnostic**.
    
    - Avoid hardcoded paths: use `getClass().getClassLoader().getResource(...)`
        

---

## 🧩 11. Summary of Key JUnit Annotations

|Annotation|Description|
|---|---|
|`@Test`|Marks a method as a test|
|`@BeforeEach`|Runs code before each test|
|`@AfterEach`|Runs code after each test|
|`@BeforeAll`|Runs once before all tests in class (static method)|
|`@AfterAll`|Runs once after all tests in class (static method)|
|`@Disabled`|Temporarily disables a test|

---

## 🧠 12. Practical Exercises (from PDF)

1. Test `gcf()` with positive values and no common factors.
    
2. Test `gcf()` with one negative input.
    
3. Refactor `gcf()` to use iteration.
    
4. Write tests for `lcd()` method.
    
5. Create `EnglishStuffTest` and write 2–3 test methods per function.
    
6. Write and verify exception-handling logic for `BankAccount.withdraw()`.
    
7. Read/write from file using `WorkWithFile` and ensure test isolation.
    

---

## 🧾 13. Final Thoughts

✅ **Good tests are:**

- Fast
    
- Isolated
    
- Repeatable
    
- Descriptive
    

🚫 **Avoid:**

- Overengineering tests
    
- Relying on test order
    
- Ignoring broken tests