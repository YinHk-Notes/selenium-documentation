https://www.guru99.com/selenium-tutorial.html


#### selenium 對網頁元素的控制
```java
WebDriver driver = new ChromeDriver();
driver.get("https://www.google.com.tw/");
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