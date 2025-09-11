https://seleniumbase.io/coffee/

---

### **1. Locate the "Menu" link**
- Using `aria-label`
  ```java
  driver.findElement(By.xpath("//a[@aria-label='Menu page']"));
  ```
- Using text()
  ```java
  driver.findElement(By.xpath("//a[text()='menu']"));
  ```
- Using `contains()` on text
  ```java
  driver.findElement(By.xpath("//a[contains(text(), 'menu')]"));
  ```
- Using `contains()` on `aria-label`
  ```java
  driver.findElement(By.xpath("//a[contains(@aria-label, 'Menu')]"));
  ```
- Using `starts-with()`
  ```java
  driver.findElement(By.xpath("//a[starts-with(@aria-label, 'Menu')]"));
  ```
- Using `preceding-sibling`
  ```java
  driver.findElement(By.xpath("//a[@aria-label='Cart page']/preceding-sibling::a"));
  ```
- Using `following-sibling`
  ```java
  driver.findElement(By.xpath("//a[@aria-label='GitHub page']/preceding-sibling::a[@aria-label='Menu page']"));
  ```

---

### **2. Locate the "Cart" link**
- Using `aria-label`
  ```java
  driver.findElement(By.xpath("//a[@aria-label='Cart page']"));
  ```
- Using `contains()` on text
  ```java
  driver.findElement(By.xpath("//a[contains(text(), 'cart')]"));
  ```
- Using `preceding-sibling`
  ```java
  driver.findElement(By.xpath("//a[@aria-label='GitHub page']/preceding-sibling::a"));
  ```
- Using `following-sibling`
  ```java
  driver.findElement(By.xpath("//a[@aria-label='Menu page']/following-sibling::a"));
  ```

---

### **3. Locate the "GitHub" link**
- Using `aria-label`
  ```java
  driver.findElement(By.xpath("//a[@aria-label='GitHub page']"));
  ```
- Using `contains()` on `aria-label`
  ```java
  driver.findElement(By.xpath("//a[contains(@aria-label, 'GitHub')]"));
  ```
- Using `preceding-sibling`
  ```java
  driver.findElement(By.xpath("//a[@aria-label='Cart page']/following-sibling::a"));
  ```

---

### **4. Locate the "Espresso" coffee item**
- Using `data-test`
  ```java
  driver.findElement(By.xpath("//div[@data-test='Espresso']"));
  ```
- Using `text()` inside `<h4>`
  ```java
  driver.findElement(By.xpath("//h4[text()='Espresso']"));
  ```
- Using `contains()` on `<h4>`
  ```java
  driver.findElement(By.xpath("//h4[contains(text(), 'Espresso')]"));
  ```
- Using `following-sibling`
  ```java
  driver.findElement(By.xpath("//h4[contains(text(), 'Espresso')]/following-sibling::div"));
  ```

---

### **5. Locate the "Mocha" coffee item**
- Using `data-test`
  ```java
  driver.findElement(By.xpath("//div[@data-test='Mocha']"));
  ```
- Using `contains()` on `<h4>`
  ```java
  driver.findElement(By.xpath("//h4[contains(text(), 'Mocha')]"));
  ```
- Using `following-sibling`
  ```java
  driver.findElement(By.xpath("//h4[contains(text(), 'Mocha')]/following-sibling::div"));
  ```

---

### **6. Locate the "Checkout" button**
- Using `data-test`
  ```java
  driver.findElement(By.xpath("//button[@data-test='checkout']"));
  ```
- Using `contains()` on button text
  ```java
  driver.findElement(By.xpath("//button[contains(text(), 'Total')]"));
  ```
- Using `preceding-sibling`
  ```java
  driver.findElement(By.xpath("//button[@data-test='checkout']/preceding-sibling::*"));
  ```

---

### **7. Locate the "Submit Payment" button**
- Using `id`
  ```java
  driver.findElement(By.xpath("//button[@id='submit-payment']"));
  ```
- Using button text
  ```java
  driver.findElement(By.xpath("//button[text()='Submit']"));
  ```
- Using `following-sibling`
  ```java
  driver.findElement(By.xpath("//input[@id='email']/following-sibling::button"));
  ```

---

### **8. Locate the "Name" input field**
- Using `id`
  ```java
  driver.findElement(By.xpath("//input[@id='name']"));
  ```
- Using `following-sibling`
  ```java
  driver.findElement(By.xpath("//label[@for='name']/following-sibling::input"));
  ```

---

### **9. Locate the "Email" input field**
- Using `id`
  ```java
  driver.findElement(By.xpath("//input[@id='email']"));
  ```
- Using `following-sibling`
  ```java
  driver.findElement(By.xpath("//label[@for='email']/following-sibling::input"));
  ```

---

### **10. Locate the Promotion Checkbox**
- Using `id`
  ```java
  driver.findElement(By.xpath("//input[@id='promotion']"));
  ```
- Using `following-sibling`
  ```java
  driver.findElement(By.xpath("//label[@id='promotion-label']/preceding-sibling::input"));
  ```

---

### **11. Locate the "Yes" button in the modal**
- Using `text()`
  ```java
  driver.findElement(By.xpath("//dialog//button[text()='Yes']"));
  ```
- Using `preceding-sibling`
  ```java
  driver.findElement(By.xpath("//button[text()='Yes']/preceding-sibling::p"));
  ```

---

### **12. Locate the "No" button in the modal**
- Using `text()`
  ```java
  driver.findElement(By.xpath("//dialog//button[text()='No']"));
  ```
- Using `preceding-sibling`
  ```java
  driver.findElement(By.xpath("//button[text()='No']/preceding-sibling::button[text()='Yes']"));
  ```

---

### **13. Locate all Coffee Names**
- Using `<h4>`
  ```java
  List<WebElement> coffeeNames = driver.findElements(By.xpath("//h4"));
  ```
- Using `preceding-sibling`
  ```java
  List<WebElement> coffeeNames = driver.findElements(By.xpath("//small/preceding-sibling::br/preceding-sibling::h4"));
  ```

---

### **14. Locate all Coffee Prices**
- Using `<h4>/<small>`
  ```java
  List<WebElement> coffeePrices = driver.findElements(By.xpath("//h4/small"));
  ```

---

### **15. Locate Coffee Cup with Espresso**
- Using `class` and `aria-label`
  ```java
  driver.findElement(By.xpath("//div[contains(@class, 'cup-body') and @aria-label='Espresso']"));
  ```
- Using `preceding-sibling`
  ```java
  driver.findElement(By.xpath("//div[@data-test='Espresso']/preceding-sibling::div[@class='cup-handler']"));
  ```

---

This list covers:
✅ **Direct attributes (`id`, `class`, `aria-label`)**  
✅ **Text-based searches (`text()`, `contains()`, `starts-with()`)**  
✅ **Sibling relationships (`preceding-sibling`, `following-sibling`)**  
✅ **Parent-child relationships**  

Would you like me to add any additional XPath strategies or specific conditions? 🚀