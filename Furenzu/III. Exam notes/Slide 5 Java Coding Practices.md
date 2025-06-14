## 📘 Java Coding Practices – Study Notes

---

### 📍1. String Management

#### 🧠 **String Pool & Immutability**

- Strings in Java are stored in a **String Pool** to **optimize memory** and **reuse objects**.
    
- Use of `==` for comparison may return true if strings are from the pool.
    
- **Immutability** means operations like concatenation create new objects:
    
    java
	
    `greeting = greeting + "day"; // creates multiple String instances`
    
- Overuse leads to **memory bloat** and **slow performance**.
    

#### ✅ **Avoid:**
	
	java
	
`String s = new String("Hello"); // Creates unnecessary objects`

---

### 🔧2. StringBuilder for Efficient Manipulation

#### 💡 Use `StringBuilder` when:

- Repeated modifications are required.
    
- Performance is critical.
    

#### ✅ Good Practice:
	
	java
	
`StringBuilder sb = new StringBuilder("Hello"); sb.append(" World").append("!"); String result = sb.toString();`

- Use `+` only when concatenation is **simple and rare** (like logs).
    

---

### 🔒3. Parameter and Field Validation

#### ✅ For Public Methods:

- **Throw `IllegalArgumentException`** for invalid inputs.
    
	java
	
`if (x < 0) throw new IllegalArgumentException("x must be positive: " + x);`

#### ✅ For Fields:

- **Throw `IllegalStateException`** to prevent using invalid object state.
    

#### 🔎 Type Safety:

- Use `instanceof` before casting:
    
	java
	
`if (obj instanceof Number) { ... }`

---

### 💰4. Avoiding float/double for Precision

#### ❌ Avoid `float`/`double` for:

- Financial or exact decimal calculations.
    

#### ✅ Use `BigDecimal`:
	
	java
	
`BigDecimal price = new BigDecimal("0.10"); // String constructor preferred`

#### 📉 Performance tip:

- For speed, use `int`/`long` with scaling:
    
	java
	
`int funds = 100; // Php1.00 as cents`

---

### 📦5. Use Enums Instead of Constants

#### ❌ Constants:

- Error-prone, hard to maintain, and unscalable.
    

#### ✅ Enums:
	
	java
	
`enum Suit { CLUBS, SPADES, HEARTS, DIAMONDS }`

- Enums support **fields, methods**, and **type safety**.
    

---

### 📚6. Java Collections – Choosing the Right One

#### ✅ **List:**

- `ArrayList`: fast for random access
    
- `LinkedList`: efficient insertions/removals
    

#### ✅ **Set:**

- `HashSet`: fast, no order
    
- `TreeSet`: sorted
    
- `LinkedHashSet`: maintains insertion order
    

#### ✅ **Queue:**

- `PriorityQueue`, `Deque`, `BlockingQueue`
    

#### ✅ **Map:**

- `HashMap`, `TreeMap`, `LinkedHashMap`
    

---

### 🔄7. Iteration in Collections

#### ✅ Options:

- **For-each loop**: simple traversal
    
- **Iterator**: allows safe removal
    
- **Streams**: functional approach (Java 8+)
    

---

### 🛡️8. Defensive Programming

#### ✅ Defensive Copies:

- Prevent internal data leaks:
    
	java
	
`Set<Section> getSections() {     return new HashSet<>(sections); }`

#### ❌ Avoid exposing mutable objects directly.

---

### 🔐9. Favor Immutable Fields

#### ✅ Benefits:

- Thread-safety
    
- Less error-prone
    

#### ✅ Use `final` fields + remove setters.

- If using `Date`, clone it when returning to prevent mutation.
    

---

### 📝10. Override toString(), equals(), and hashCode()

#### ✅ `toString()`:

- Meaningful output helps with debugging.
    
- Avoid infinite recursion or long dumps.
    

#### ✅ `equals()` and `hashCode()`:

- Must obey **reflexivity, symmetry, transitivity, consistency**, and `null` safety.
    
- Ensure they’re consistent with each other to support collections like `Set`, `Map`.
    

---

### 🚫11. Avoid Passing Null

#### ❌ Problems with `null`:

- Causes `NullPointerException`
    
- Makes debugging hard
    

#### ✅ Instead:

- Initialize variables
    
- Return empty collections or Optional
    
	java
	
`return Optional.ofNullable(student);`

#### 🧱 Use Null Object Pattern:
	
	java
	
`public static final Student NONE = new Student(0);`

---

### ⚠️12. Exception Handling Best Practices

#### ✅ Never Leave Catch Blocks Empty

#### ✅ Catch Specific Exceptions
	
	java
	
`try {     ... } catch (IOException e) {     ... }`

#### ✅ Use try-with-resources (Java 7+)
	
	java
	
`try (Connection conn = ...) {     ... }`

#### ✅ Embed Useful Debug Info
	
	java
	
`throw new CustomException("Conflict: " + existing + ", " + newSec);`

---

### 🔁13. Exception Translation Pattern

#### ✅ Wrap low-level exceptions into higher-level exceptions:
	
	java
	
`catch (SQLException e) {     throw new DataAccessException("DB failed", e); }`

#### 🎯 Benefits:

- **Preserves method signatures**
    
- **Improves encapsulation**
    
- **Decouples client from data source**
    

---

### 🧵14. Concurrency & Synchronization

#### ❌ Avoid synchronizing whole methods

- Use minimal **synchronized blocks** to reduce contention.
    
	java
	
`synchronized (sections) {     if (...) { ... } }`

#### ❌ Don’t Synchronize DB Calls

- DBs are better equipped for **locking**, **rollback**, and **transactions**.
    
- Synchronizing in Java can lead to:
    
    - Performance degradation
        
    - Inconsistent locking
        
    - Hard-to-maintain code
        

---

### 📚15. Final Reminders

- This is not exhaustive. Keep learning!
    
- Recommended resource: [http://javapractices.com](http://javapractices.com)
    

---

### 🏁 Conclusion

Good Java practices enhance:

- Code **clarity**
    
- **Performance**
    
- **Safety** in concurrent environments
    
- **Maintainability** in large systems
    

They also reduce technical debt and future bugs. Stick to the principles discussed and build a habit of **writing clean, efficient, and defensive Java code**.