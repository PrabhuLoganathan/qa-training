# Selenium 4 – Methods, ExpectedConditions, Actions, Select, Exceptions (Handy Guide)

> Quick, practical reference for day‑to‑day automation in Java with Selenium 4.x. Each method includes what it does and a short usage snippet.

---

## Table of Contents

1. WebDriver core
2. Navigation & Window/Tab handling
3. Timeouts & Waits (WebDriverWait)
4. WebElement API
5. Locators & Relative Locators (Selenium 4)
6. Actions class (mouse & keyboard)
7. Select class (dropdowns)
8. Alerts, Frames & Windows (Target Locator)
9. Cookies & Local Storage (via DevTools)
10. ExpectedConditions catalog (with examples)
11. Common Selenium Exceptions (what/when)
12. Tips, patterns, and gotchas

---

## 1) WebDriver Core

### Driver lifecycle

* `get(String url)`: Open a URL.

```java
driver.get("https://example.com");
```

* `quit()`: Close all windows and end session.
* `close()`: Close the current window.
* `getTitle()`, `getCurrentUrl()`, `getPageSource()`: Metadata of current page.

### Find Elements (By)

* `findElement(By locator)`: Returns first matching element or throws `NoSuchElementException`.
* `findElements(By locator)`: Returns a `List<WebElement>` (empty list if none).

```java
WebElement btn = driver.findElement(By.id("login"));
List<WebElement> rows = driver.findElements(By.cssSelector("table tr"));
```

---

## 2) Navigation & Window/Tab Handling

### Navigation

* `driver.navigate().to(url)`: Navigate to URL.
* `driver.navigate().back()`, `.forward()`, `.refresh()`.

### Windows & Tabs (Selenium 4)

* `getWindowHandle()`: Current window id.
* `getWindowHandles()`: All windows ids.
* `switchTo().window(handle)`: Switch to a window.
* `switchTo().newWindow(WindowType.TAB | WindowType.WINDOW)`: Open and switch to a new tab/window.

```java
String original = driver.getWindowHandle();
driver.switchTo().newWindow(WindowType.TAB);
driver.get("https://example.org");
driver.switchTo().window(original);
```

### Window management

* `manage().window().maximize()`, `.minimize()`, `.fullscreen()`.
* `manage().window().setSize(new Dimension(w,h))`, `.setPosition(new Point(x,y))`.

---

## 3) Timeouts & Waits (WebDriverWait)

### Timeouts

* `manage().timeouts().implicitlyWait(Duration)`: Implicit wait for element finds.
* `manage().timeouts().pageLoadTimeout(Duration)`: Page load limit.
* `manage().timeouts().scriptTimeout(Duration)`: Async script limit.

### Explicit Wait (preferred)

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
WebElement el = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("user")));
```

### Fluent Wait pattern

```java
Wait<WebDriver> fluent = new FluentWait<>(driver)
  .withTimeout(Duration.ofSeconds(20))
  .pollingEvery(Duration.ofMillis(500))
  .ignoring(NoSuchElementException.class);
WebElement el = fluent.until(d -> d.findElement(By.id("user")));
```

> **Tip:** Prefer explicit waits targeted to specific states; keep implicit wait low or zero to avoid compounded delays.

---

## 4) WebElement API

* `click()`: Click element.
* `sendKeys(CharSequence...)`: Type text/keys.
* `clear()`: Clear input/textarea.
* `getText()`: Visible text.
* `getAttribute(String)`: Attribute value (e.g., `value`, `href`).
* `getDomProperty(String)`: Live DOM property (Selenium 4).
* `getDomAttribute(String)`: Live DOM attribute (Selenium 4).
* `getCssValue(String)`: Computed CSS.
* `isDisplayed()`, `isEnabled()`, `isSelected()`.
* `submit()`: Submits a form (if applicable).
* `getRect()`: `Dimension` + `Point` (size/position).
* `getAriaRole()` / `getAccessibleName()` (Selenium 4, accessibility helpers).

```java
WebElement user = driver.findElement(By.name("username"));
user.clear();
user.sendKeys("nilav.tester");
boolean enabled = user.isEnabled();
String role = user.getAriaRole();
```

---

## 5) Locators & Relative Locators (Selenium 4)

### Classic `By`

* `By.id`, `By.name`, `By.className`, `By.tagName`, `By.linkText`, `By.partialLinkText`, `By.cssSelector`, `By.xpath`.

### Relative Locators (a.k.a. Friendly Locators)

* `RelativeLocator.with(By.tagName("input")).above(element)`
* `.below(element)`, `.toLeftOf(element)`, `.toRightOf(element)`, `.near(element)`

```java
WebElement label = driver.findElement(By.xpath("//label[text()='Email']"));
WebElement email = driver.findElement(with(By.tagName("input")).below(label));
```

---

## 6) Actions Class (Mouse & Keyboard)

Create once and reuse:

```java
Actions actions = new Actions(driver);
```

### Mouse

* `moveToElement(el)`: Hover.
* `click(el)`, `doubleClick(el)`, `contextClick(el)`.
* `clickAndHold(el)`, `release(el)`.
* `dragAndDrop(src, dst)`, `dragAndDropBy(src, xOffset, yOffset)`.
* `moveByOffset(x,y)`, `moveToElement(el, xOffset, yOffset)`.

```java
actions.moveToElement(menu).perform();
actions.dragAndDrop(card, dropZone).perform();
```

### Keyboard

* `sendKeys(Keys.ENTER)`, `keyDown(Keys.SHIFT)`, `keyUp(Keys.SHIFT)`.

```java
actions.keyDown(Keys.CONTROL).sendKeys("a").keyUp(Keys.CONTROL).perform();
```

### Composite sequences

* Chain multiple steps, finish with `.build().perform()` or just `.perform()`.

> **Tip:** For reliable drag‑drop in some UIs, consider JS helpers or `clickAndHold` + `moveToElement` + `release` sequence.

---

## 7) Select Class (HTML `<select>` only)

```java
WebElement ddl = driver.findElement(By.id("country"));
Select select = new Select(ddl);
```

* `selectByVisibleText(String)`
* `selectByValue(String)`
* `selectByIndex(int)`
* `getFirstSelectedOption()`
* `getAllSelectedOptions()`
* `getOptions()`
* `deselectAll()` (only for multi‑selects)
* `deselectByVisibleText/Value/Index`

```java
select.selectByVisibleText("India");
List<WebElement> options = select.getOptions();
```

---

## 8) Alerts, Frames & Windows (Target Locator)

### Alerts

* `switchTo().alert()`: Returns `Alert`.
* `getText()`, `accept()`, `dismiss()`, `sendKeys(String)` (prompts).

### Frames & iFrames

* `switchTo().frame(int | String | WebElement)`, `parentFrame()`, `defaultContent()`.

```java
driver.switchTo().frame("payment-iframe");
// interact
driver.switchTo().defaultContent();
```

### Active element

* `switchTo().activeElement()`: Current focused element (useful after dialogs, etc.).

---

## 9) Cookies & Local Storage (incl. DevTools)

### Cookies (WebDriver)

* `manage().getCookies()`, `getCookieNamed(String)`, `addCookie(Cookie)`, `deleteCookie(Cookie|String)`, `deleteAllCookies()`.

```java
Cookie session = new Cookie("sessionId", "abc123");
driver.manage().addCookie(session);
```

### Local/Session Storage (via JS)

```java
JavascriptExecutor js = (JavascriptExecutor) driver;
js.executeScript("return window.localStorage.setItem(arguments[0], arguments[1]);", "token", "xyz");
Object token = js.executeScript("return window.localStorage.getItem('token');");
```

### Chrome DevTools Protocol (Selenium 4)

```java
DevTools dev = ((HasDevTools) driver).getDevTools();
dev.createSession();
dev.send(Network.enable(Optional.empty(), Optional.empty(), Optional.empty()));
```

Common CDP tasks: network interception, console logs, geolocation override, basic performance tracing.

---

## 10) ExpectedConditions – Catalog with Quick Use

> Import: `import static org.openqa.selenium.support.ui.ExpectedConditions.*;`

**Visibility/Presence**

* `presenceOfElementLocated(By)`: Present in DOM (may be hidden).
* `visibilityOf(WebElement)` / `visibilityOfElementLocated(By)`: Present **and** visible.
* `visibilityOfAllElements(List<WebElement> | By)`
* `invisibilityOf(WebElement | By | String text)`

```java
wait.until(visibilityOfElementLocated(By.id("user")));
```

**Clickability & Selection**

* `elementToBeClickable(By | WebElement)`
* `elementToBeSelected(By | WebElement)` / `elementSelectionStateToBe(WebElement, boolean)`

**Text & Attribute**

* `textToBePresentInElement(WebElement, String)` / `...Located(By, String)`
* `textToBePresentInElementValue(By | WebElement, String)`
* `attributeToBe(By | WebElement, String name, String value)`
* `attributeContains(By | WebElement, String name, String fraction)`
* `attributeToBeNotEmpty(WebElement, String)`

**Frames & Alerts & Windows**

* `frameToBeAvailableAndSwitchToIt(int | String | By | WebElement)`
* `alertIsPresent()`
* `numberOfWindowsToBe(int)`

**Elements Count & State**

* `numberOfElementsToBe(By, int)`
* `numberOfElementsToBeMoreThan(By, int)`
* `stalenessOf(WebElement)` (element detached from DOM)

**URL & Title**

* `titleIs(String)`, `titleContains(String)`
* `urlToBe(String)`, `urlContains(String)`, `urlMatches(String regex)`

**Example – wait for new tab and switch**

```java
String current = driver.getWindowHandle();
wait.until(numberOfWindowsToBe(2));
for (String h : driver.getWindowHandles()) {
  if (!h.equals(current)) driver.switchTo().window(h);
}
```

---

## 11) Common Selenium Exceptions (What/When)

* **`NoSuchElementException`**: Element not found with given locator.

  * *Fix:* Check locator, add explicit wait for presence/visibility.
* **`StaleElementReferenceException`**: Element is no longer attached to DOM.

  * *Fix:* Re‑locate element after DOM updates; use `stalenessOf` + re‑find.
* **`TimeoutException`**: Wait condition not met in time.

  * *Fix:* Increase timeout, correct condition/locator.
* **`ElementClickInterceptedException`**: Another element overlays target.

  * *Fix:* Scroll/hover, wait for `elementToBeClickable`, close overlays.
* **`ElementNotInteractableException`**: Hidden/disabled element when interacting.

  * *Fix:* Wait for visible+enabled, or interact via JS if appropriate.
* **`NoSuchWindowException` / `NoSuchFrameException`**: Invalid window/frame handle.

  * *Fix:* Ensure it exists; wait for `numberOfWindowsToBe` or `frameToBeAvailable...`.
* **`UnexpectedAlertPresentException`**: Alert interrupted the action.

  * *Fix:* Handle alert first `switchTo().alert().accept()`.
* **`InvalidSelectorException`**: Malformed CSS/XPath.
* **`MoveTargetOutOfBoundsException`**: Off‑screen coordinates in Actions.
* **`UnreachableBrowserException`**: Driver/browser crash or lost connection.
* **`SessionNotCreatedException`**: Driver–browser version mismatch.
* **`WebDriverException`**: Generic underlying driver error.

> **Pro‑tip:** Wrap risky interactions with short retries (e.g., `FluentWait` ignoring `StaleElementReferenceException`).

---

## 12) Tips, Patterns, and Gotchas

* **Prefer explicit waits** tied to a specific condition over large implicit waits.
* **Stable locators:** Favor `data-testid`/`data-qa` if available; avoid brittle XPaths.
* **Page Objects + Components:** Encapsulate element locators & actions; expose business‑level methods.
* **Resilient clicks:** Wait for `elementToBeClickable` and scroll into view when needed.
* **File uploads:** Use `input[type='file']` `sendKeys(path)`; avoid robot classes when possible.
* **Shadow DOM:** Selenium 4 supports `getShadowRoot()` on a shadow host.

```java
WebElement host = driver.findElement(By.cssSelector("custom-el"));
SearchContext shadow = host.getShadowRoot();
WebElement inside = shadow.findElement(By.cssSelector("#inner"));
```

* **Relative locators:** Great for stable layout‑based references.
* **DevTools:** Useful for network mocking, capturing console, device emulation.

---

## Mini Cookbook (Copy‑Paste)

**Wait visible + click**

```java
WebElement btn = wait.until(visibilityOfElementLocated(By.id("submit")));
wait.until(elementToBeClickable(btn)).click();
```

**Safe type text**

```java
WebElement input = wait.until(elementToBeClickable(By.name("email")));
input.clear();
input.sendKeys("prabhu@example.com");
```

**Retry on Stale**

```java
WebElement row = driver.findElement(By.cssSelector("tr.highlight"));
wait.until(stalenessOf(row));
row = driver.findElement(By.cssSelector("tr.highlight"));
```

**Select dropdown**

```java
Select s = new Select(wait.until(visibilityOfElementLocated(By.id("country"))));
s.selectByVisibleText("India");
```

**Drag and drop**

```java
actions.clickAndHold(src).moveToElement(dst).release().perform();
```

**Alert handling**

```java
Alert a = wait.until(alertIsPresent());
a.accept();
```

**Open in new tab and switch**

```java
String orig = driver.getWindowHandle();
driver.switchTo().newWindow(WindowType.TAB);
driver.get("https://google.com");
for (String h : driver.getWindowHandles()) if(!h.equals(orig)) driver.switchTo().window(h);
```

**Shadow DOM find**

```java
SearchContext shadow = driver.findElement(By.id("host")).getShadowRoot();
WebElement inner = shadow.findElement(By.cssSelector("#inner"));
```

