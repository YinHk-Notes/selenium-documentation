#### selenium
https://www.selenium.dev/documentation/overview/

#### selenium package document
https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/package-summary.html

#### tutorial

https://www.guru99.com/selenium-tutorial.html \
https://www.tpisoftware.com/tpu/articleDetails/2284

#### selenium(Java) 對網頁元素的控制
```java
WebDriver driver = new ChromeDriver();
//launching a browser is to open your website
driver.get("https://www.google.com.tw/");
//上一頁
driver.navigate().back();
//下一頁
driver.navigate().forward();
//refresh page
driver.navigate().refresh();
//Quitting the browser at the end of a session
driver.quit();
//定位網頁元素
WebElement element = driver.findElement(By.name("q"));
//對元素點擊
element.click();
//清空內容(例如input欄位)
element.clear();
//對元素輸入內容(例如input欄位輸入資料)
element.sendKeys("selenium");
//元素是否可見(true:是，false:否)
element.isDisplayed();
//元素是否啟用
element.isEnabled();
//元素是否已選
element.isSelected();
//對元素做FormSubmit的操控
element.submit();
```

#### alerts in browser
```java
//Wait for the alert to be displayed and store it in a variable
Alert alert = wait.until(ExpectedConditions.alertIsPresent());
//Store the alert text in a variable
String text = alert.getText();
//Press the OK button
alert.accept();
```

#### confirm box
```java
//Wait for the alert to be displayed
wait.until(ExpectedConditions.alertIsPresent());
//Store the alert in a variable
Alert alert = driver.switchTo().alert();
//Store the alert in a variable for reuse
String text = alert.getText();
//Press the Cancel button
alert.dismiss();
```

#### Prompt
Prompts are similar to confirm boxes, except they also include a text input
```java
/Wait for the alert to be displayed and store it in a variable
Alert alert = wait.until(ExpectedConditions.alertIsPresent());
//Type your message
alert.sendKeys("Selenium");
//Press the OK button
alert.accept();
```

#### selenium 提供了8種的定位方式
```java
driver.findElement(By.id("elementId")); // 用元素的id屬性值來定位元素
driver.findElement(By.name("elementName")); // 用元素的name屬性值來定位元素
driver.findElement(By.className("elementClass")); // 用元素的class名稱來定位元素
driver.findElement(By.tagName("input")); // 用元素的tag標籤來定位元素
driver.findElement(By.linkText("登入")); // 用元素的文字內容來定位元素
driver.findElement(By.partialLinkText("測試")); // 用元素的部分文字內容來定位元素
driver.findElement(By.xpath("//input[@id='kw']")); // 用xpath語法來定位元素
driver.findElement(By.cssSelector("#kw")); // 用CSS選擇器來定位元素
```

#### 如果是複數元素的話，只需要改寫成findElements
```java
driver.findElements(By.id("elementId")); // 用元素的id屬性值來定位元素
driver.findElements(By.name("elementName")); // 用元素的name屬性值來定位元素
driver.findElements(By.className("elementClass")); // 用元素的class名稱來定位元素
driver.findElements(By.tagName("input")); // 用元素的tag標籤來定位元素
driver.findElements(By.linkText("登入")); // 用元素的文字內容來定位元素
driver.findElements(By.partialLinkText("測試")); // 用元素的部分文字內容來定位元素
driver.findElements(By.xpath("//input[@id='kw']")); // 用xpath語法來定位元素
driver.findElements(By.cssSelector("#kw")); // 用CSS選擇器來定位元素

```

|findElement|findElements|
|-|-|
|Returns the first matching web element if multiple web elements are discovered by the locator|Returns a list of multiple matching web elements|
|Throws NoSuchElementException if the element is not found|Returns an empty list if no matching element is found|
|Detects a unique web element|Returns a collection of matching elements|


### cucumber
https://cucumber.io/docs/guides/overview/

### Xpath
https://www.w3schools.com/xml/xpath_syntax.asp \
https://devhints.io/xpath
