# Day02 Selenium Overview — Notes

## Topics Covered
- What is Selenium?
- Selenium History
- Selenium IDE
- Selenium RC
- Selenium Grid (overview)
- Selenium WebDriver
- WebDriver Architecture
- Selenium 4 — what's new
- (Brief) Web automation tools landscape: Playwright, Appium, AccELQ

## References
- (Add links to official docs/blogs/videos)

# Selenium - Detailed Documentation with Real-Time Examples 🎯🔥🚀

## 1. What is Selenium? 🤖🌍💡

✔️ Selenium is an open-source automation testing framework. 🤖
✔️ It supports multiple browsers and operating systems. 🌍
✔️ Test scripts can be written in Java, Python, C#, JavaScript, etc. 💻

### Real-Time Example:
✅ Automating search functionality for an e-commerce platform like Amazon. 🛒💻🔍

---

## 2. Selenium History 📜⌛🖥

📌 **Selenium Core (2004):** JavaScript-based automation. 📝
📌 **Selenium RC (2005):** First cross-browser testing tool. 🌐
📌 **Selenium IDE (2006):** Record and playback extension. 🎥
📌 **Selenium WebDriver (2008):** Improved automation without an intermediate server. 🚗
📌 **Selenium Grid (2009):** Parallel test execution. 🔄
📌 **Selenium 4 (2021):** Enhanced support for modern web applications. 🚀

### Real-Time Example:
🚀 Migrating from **Selenium RC** to **Selenium WebDriver** for better performance. ⚡🔄📊

---

## 3. Selenium IDE 🖱🎥🔄

### Key Features:
🔹 Record and playback functionality. 🎬
🔹 No programming knowledge required. 📝
🔹 Supports multiple scripting languages. 🌍

### Limitations:
⚠️ Not suitable for complex test scenarios. ❌
⚠️ No parallel execution support. ⏳

### Real-Time Example:
📝 Recording login test cases quickly using **Selenium IDE**. 🔐🖥✅

---

## 4. Selenium RC (Remote Control) 🚦📡🔄

### Key Features:
💡 Supports multiple programming languages. 📜
💡 Requires a Selenium server in the background. ⚙️
💡 Handles AJAX-based UI testing. 🔄

### Limitations:
⚠️ Slower execution. 🐢
⚠️ Complex setup. 🔧
⚠️ Deprecated after WebDriver. ❌

### Real-Time Example:
🔄 Transitioning a legacy e-commerce automation from **Selenium RC** to **WebDriver**. 🏪💳📈

---

## 5. Selenium Grid 🕸🖥📊

### Key Features:
🔄 Parallel execution. ⚡
🔄 Works with multiple browsers and platforms. 🌐
🔄 Uses a hub-node architecture for distributed testing. 🖥

### Usage Scenarios:
✔️ Cross-browser testing. 🌍
✔️ Running tests in different environments. 🔄
✔️ Distributed test execution. 🏭

### Real-Time Example:
🏦 A banking application using Selenium Grid for multi-browser testing. 💰🔐💻

---

## 6. Selenium WebDriver 🚗🌍🔧

### Key Features:
🌍 Supports multiple browsers (Chrome, Firefox, Edge, Safari, etc.). 🖥
🌍 Allows testing in multiple programming languages. 🔤
🌍 Handles dynamic elements, AJAX applications, pop-ups. 🔄
🌍 No need for a Selenium server for local execution. 🚀

### Advantages over Selenium RC:
⚡ Faster execution. 🚗
⚡ Efficient handling of web elements. 🎯
⚡ Better integration with modern automation frameworks. 🔌

### Real-Time Example:
✈️ Automating an airline ticket booking process. 🏨🛫🎫

---

## 7. WebDriver Architecture 🏗🔩💻

### Components:
1️⃣ **Selenium Client Libraries** - Multi-language support. 📚
2️⃣ **JSON Wire Protocol** - Communication mechanism. 🔗
3️⃣ **Browser Drivers** - ChromeDriver, GeckoDriver, EdgeDriver. 🌍
4️⃣ **Real Browser** - Executes test cases. 🖥

### How It Works:
🔹 The script interacts with the WebDriver API. 🎯
🔹 WebDriver communicates with the browser driver. 🌍
🔹 The browser driver executes commands on the browser. ⚙️
🔹 Test results are returned. 📊

### Real-Time Example:
🛫 Automating a travel website’s flight search functionality. 🌍🎟✈

---

## 8. Selenium 4 - What's New? 🚀✨💡

### Key Features:
🚀 **W3C WebDriver Standardization** - Improved stability. 🔄
🚀 **Relative Locators** - Find elements relative to others. 🧭
🚀 **Enhanced Selenium Grid** - Supports Docker containers. 🛠
🚀 **Improved Debugging & Logging** - Built-in network logs. 📝
🚀 **Better Window & Tab Management** - Manage multiple tabs easily. 🖥
🚀 **Chromium DevTools Protocol (CDP) Support** - Performance analysis automation. 📊

### Why Upgrade to Selenium 4?
✔️ Improved automation reliability. 🔄
✔️ Better browser compatibility. 🌍
✔️ Enhanced debugging and reporting. 📝

### Real-Time Example:
📊 A digital marketing agency using **CDP in Selenium 4** for network monitoring. 📈🛠🔍

---

## Conclusion ✅📌🚀

✅ Selenium is a powerful framework for web automation. 🤖
✅ It supports multiple tools like **WebDriver**, **Selenium Grid**, and **Selenium IDE**. 🛠
✅ Enables cross-browser testing and enhances software quality. 💡🖥💯

--------------------------------------------------------------------------------------------



# Selenium 4 Architecture and Updated Methods

---

## 🔹 Selenium 4 Architecture

### 1. Old Architecture (Selenium 3 and below)

* **Client Libraries** (Java, Python, C#, etc.) communicated with Selenium Server using **JSON Wire Protocol**.
* Selenium Server translated requests into browser-specific commands.
* Required a **bridge layer**, which often caused inconsistencies between browsers.

### 2. New Architecture (Selenium 4)

* Fully **W3C WebDriver Protocol compliant**.
* Client libraries directly communicate with **browser drivers** (ChromeDriver, GeckoDriver, EdgeDriver).
* No need for JSON Wire Protocol translation.
* Benefits:

  * Faster execution
  * More stable tests
  * Reduced flakiness

**Flow:**
👉 Client Bindings → W3C HTTP Requests → Browser Driver → Browser

---

## 🔹 Key Updates & Features in Selenium 4

### 1. Relative Locators (Friendly Locators)

Locate elements based on their position relative to other elements.

```java
WebElement password = driver.findElement(By.name("password"));
WebElement username = driver.findElement(RelativeLocator.with(By.tagName("input")).above(password));
```

Options: `above()`, `below()`, `toLeftOf()`, `toRightOf()`, `near()`

---

### 2. Improved Window & Tab Management

```java
// Open a new tab
driver.switchTo().newWindow(WindowType.TAB);

// Open a new window
driver.switchTo().newWindow(WindowType.WINDOW);
```

---

### 3. Better Actions API (Mouse & Keyboard)

```java
Actions actions = new Actions(driver);
actions.moveToElement(element).click().perform();

// Scrolling with wheel
actions.scrollByAmount(0, 500).perform();
```

---

### 4. Enhanced Screenshots

```java
// Full page screenshot
File src = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);

// Element screenshot
WebElement logo = driver.findElement(By.id("logo"));
File srcElement = logo.getScreenshotAs(OutputType.FILE);
```

---

### 5. CDP (Chrome DevTools Protocol) Integration

```java
DevTools devTools = ((HasDevTools) driver).getDevTools();
devTools.createSession();
devTools.send(Network.enable(Optional.empty(), Optional.empty(), Optional.empty()));
```

Use cases:

* Capture network requests/responses
* Mock geolocation
* Simulate device mode

---

### 6. New Wait Improvements

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("loginBtn")));
```

---

### 7. Improved Grid 4

* Fully distributed architecture
* Supports Docker & Kubernetes
* Auto-discovery of nodes
* Supports video recording & observability

---

## 🔹 Comparison: Selenium 3 vs Selenium 4

| Feature             | Selenium 3              | Selenium 4                         |
| ------------------- | ----------------------- | ---------------------------------- |
| Protocol            | JSON Wire               | W3C WebDriver                      |
| Relative Locators   | ❌                       | ✅                                  |
| Window/Tab Handling | Limited                 | `newWindow()` API                  |
| Screenshots         | Full page only          | Element & section level            |
| Actions API         | Basic                   | Enhanced with wheel/zoom           |
| DevTools            | ❌                       | ✅ Built-in                         |
| Grid                | Hub/Node (manual setup) | Distributed, Docker, Observability |

---

## ✅ Summary

Selenium 4 is **faster, more stable, and feature-rich** thanks to:

* W3C compliance
* New locators
* Better window handling
* DevTools integration
* Improved waits
* Enhanced Grid 4
