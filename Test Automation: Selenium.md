# Test Automation

Test Automation will help us to reduce the overall time required to test the product, or a feature, with greater efficiency and accuracy.

### Common types of test automation

1.  **UI automation**: Automates the user workflows for web applications
2.  **Mobile automation**: Automates the user workflows for android, iOS or mobile-web
3.  **API automation**: Automates the REST or SOAP-based backend services

### Selenium

Selenium is a suite of tools that helps you to automate cross-browser testing for a web-based application.

### Selenium components
The Selenium comprises of these main components:

-   **Selenium WebDriver**  - is a collection of open-source APIs that helps in simulating user flows for any web-based application
-   **Selenium IDE**  - is a browser add-on that helps you to create tests quickly through its record-and-playback functionality.
-   **Selenium Grid**  - helps you in executing tests in parallel across different browsers, operating systems, and machines

#### Selenium WebDriver

WebDriver is a web framework that helps you execute **cross-browser** tests; it uses browser automation **APIs provided by browser vendors** such as Firefox, Chrome, Safari, Microsoft Internet Explorer, Microsoft Edge, Opera, etc., to interact with the browser and simulate user actions. It supports different programming languages and allows you to write the test scripts in your choice of language.


#### WebDriver architecture
https://www.educative.io/api/collection/5455247108472832/4603030201696256/page/5336047337603072/image/5065502423515136.png

#### Download WebDriver

For downloading driver executables of different browsers:

Chrome:[https://sites.google.com/a/chromium.org/chromedriver/downloads](https://sites.google.com/a/chromium.org/chromedriver/downloads)

Firefox:  [https://github.com/mozilla/geckodriver](https://github.com/mozilla/geckodriver)

Edge:  [https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/)

Internet Explorer:  [https://selenium-release.storage.googleapis.com/index.html](https://selenium-release.storage.googleapis.com/index.html)

Opera: [https://github.com/operasoftware/operachromiumdriver/releases](https://github.com/operasoftware/operachromiumdriver/releases)

## Locators in Selenium
To perform an action on any element, we first have to locate/find it on the web page through various built-in locator strategies which are being offered by Selenium WebDriver.

- **Id  :** The element whose  `id`  matches the search value.
```
<input type='email' id="mailId">

WebElement emailField = driver.findElement(By.id("mailId"));
```
- **name :** The element whose  `name`  matches the search value.
```
<input type='email' name="mailId">

WebElement emailField = driver.findElement(By.name("mailId"));
```

- **class:** Locate the element with a  `class`  name.
```
<input type='email' class="inputtext login_form_input_box">

WebElement emailField = driver.findElement(By.className("inputtext login_form_input_box"));
```
- **css:** The element matching a  `css`  selector:
```
<input type='email'>

WebElement emailField = driver.findElement(By.cssSelector("input#email"));
```
CSS  Selector  Reference: https://www.w3schools.com/cssref/css_selectors.asp

- **xpath:** Locates elements matching an  `xpath`  expression:
```
<input type='email'>

WebElement emailField = driver.findElement(By.xpath("//input[@type = 'email']"));
```
- **linkText:** The element whose visible text matches the search value:
```
<a href="www.google.com">Search result<a/>

WebElement forgottenAccount = driver.findElement(By.linkText("Search result"));
```
- **partialLinkText:** It locates anchor elements whose visible text _contains_ the search value.
```
<a href="www.google.com">Search result<a/>

WebElement forgottenAccount = driver.findElement(By.partialLinkText("Search"));
```

- **tag:** It locates elements whose `tag` name matches the search value.
```
<a href="www.google.com">Search result<a/>

WebElement facebookText = driver.findElement(By.tagName("a"));
```







