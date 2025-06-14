# 🧠 Risk-Based Testing — Study Notes

## 🎯 Overview

Risk-Based Testing (RBT) is a testing strategy that prioritizes test efforts based on risk. It shifts the focus from achieving exhaustive test coverage to **managing risk effectively** by considering **impact** and **probability**.

---

## ⚖️ Risk = Impact × Probability

This fundamental formula drives Risk-Based Testing. Each potential test scenario is evaluated based on:

- **Impact**: What happens if the defect occurs?
    
- **Probability**: How likely is it that the defect will occur?
    

Only by combining these two factors can you accurately assess risk and make smart testing decisions.

---

## 🔍 Understanding Impact

### Key Idea: Not all failures are created equal.

Impact depends heavily on **context**, such as the application’s purpose and user expectations. For example:

|Scenario|Impact|
|---|---|
|Social media glitch|Low|
|Financial transaction error|High|
|Medical device inaccuracy|Critical|
|Dropdown not working|Minor|
|User can’t log in|Major|
|Incorrect accounting entries|Severe|
|Report formatting issue|Low|
|System can’t handle peak load|High|

### Best Practices:

- Understand the **domain and stakeholders' priorities**.
    
- Do **domain-specific research**.
    
- Involve **business experts** and **stakeholders early**.
    
- Use test design as an exploratory process to **generate questions**.
    

🗣 **Talk to people early** — Don’t wait until testing time.

---

## 🎲 Understanding Probability

There are **two kinds of probabilities** to assess:

### 1. **Scenario Probability**

- How often will this scenario be encountered by users?
    
- Example: Logging in = High frequency; Admin settings = Low frequency.
    

### 2. **Bug Probability**

- What’s the likelihood that this code has a defect?
    
- Influenced by:
    
    - Code complexity
        
    - Developer skill
        
    - Usage of tested/reliable libraries
        

### Total Risk Probability
	
	mathematica
	
`Total Probability = Scenario Probability × Bug Probability`

---

## 🐞 Assessing Bug Probability

Not all code is equally risky. Some areas are inherently safer:

|Code Type|Bug Probability|
|---|---|
|Getters & Setters|Low|
|Null validations|Moderate|
|Complex calculations|High|
|Simple, clean code|Low|
|Third-party, reliable libraries|Low|

### Reduce Bug Probability By:

- Writing **clean, modular** code.
    
- Using **well-tested libraries**.
    
- Applying **static analysis** and **peer reviews**.
    

💡 **Lowering bug probability** frees up resources to test **higher-impact** areas.

---

## 🧭 Strategy Shift: Test Smarter, Not Harder

Instead of aiming for 100% test coverage:

✅ Focus on **high-risk scenarios**  
✅ Use **risk to prioritize test cases**  
✅ Spend **less time on low-impact, low-probability code**  
✅ Communicate with domain experts early to refine risk estimations

---

## 🧩 Summary of Key Concepts

|Concept|Definition|
|---|---|
|**Impact**|The severity of consequences if a defect occurs|
|**Scenario Probability**|How often a particular usage scenario is triggered|
|**Bug Probability**|Likelihood that the code for a feature has a bug|
|**Risk-Based Testing**|A test strategy focused on identifying and managing risk instead of maximizing test coverage|

---

## 🧠 Memory Aids

- **“High Risk = High Priority”**
    
- **“Test what matters most”**
    
- **“Risk = Impact × Probability”**