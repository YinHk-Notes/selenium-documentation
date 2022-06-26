#### selenium
https://www.selenium.dev/documentation/overview/

#### selenium package document
https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/package-summary.html

#### Install web driver
[ChromeDriver - WebDriver for Chrome](https://sites.google.com/chromium.org/driver/) \
https://www.selenium.dev/documentation/webdriver/getting_started/install_drivers/

#### tutorial

https://www.guru99.com/selenium-tutorial.html \
https://www.tpisoftware.com/tpu/articleDetails/2284 \
[https://youtu.be/j7VZsCCnptM](https://www.youtube.com/watch?v=aIfP8rOx66E)

#### selenium(Java) 對網頁元素的控制
```java
WebDriver driver = new ChromeDriver();
//若瀏覽器安裝位置為預設則webDriver會自動搜尋path設定的位置，也可以使用System.setProperty 來指定路徑
System.setProperty("webdriver.chrome.driver", "C:\\Program Files (x86)\\Google\\Chrome\\Application\\chromedriver.exe");
//launching a browser is to open your website
driver.get("https://www.google.com.tw/");
driver.navigate().to(URL);
//上一頁
driver.navigate().back();
//下一頁
driver.navigate().forward();
//refresh page
driver.navigate().refresh();
//Quitting the browser only
driver.close();
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
#### drag and Drop action

```java
//action of click and hold 
.clickAndHold(WebElement element)
//move element without any click
.moveToElement(WebElement element)
//release the element
.release(WebElement element)
//build all the actions in drag and drop
.build()
```
```java
//WebElement on which drag and drop operation needs to be performed
WebElement fromElement = driver.findElement(By Locator of fromElement);

//WebElement to which the above object is dropped
WebElement toElement = driver.findElement(By Locator of toElement);

//Creating object of Actions class to build composite actions
Actions builder = new Actions(driver);

//Building a drag and drop action
Action dragAndDrop = builder
  .clickAndHold(fromElement)
    .moveToElement(toElement)
      .release(toElement)
        .build();

//Performing the drag and drop action
dragAndDrop.perform();
```
**OR**
```java
WebElement from = driver.findElement(By Locator of fromElement);  
WebElement to = driver.findElement(By Locator of toElement);

//Creating object of Actions class to build composite actions  
Actions act = new Actions(driver);  

//Performing the drag and drop action  
act.dragAndDrop(from,to).build().perform(); 
```

#### select dropdown
```java
WebElement testDropDown = driver.findElement(By.id("testingDropdown"));  
Select dropdown = new Select(testDropDown);

//3 methods for selecting item in the dropdown menu:

//by index
dropdown.selectByIndex(index);  
//by value
dropdown.selectByValue(value);
//by text on the menu
dropdown.selectByVisibleText(text);
```
```java
// Deselect an <option> based upon the <select> element's internal index
selectObject.deselectByIndex(1);

// Deselect an <option> based upon its value attribute
selectObject.deselectByValue("value1");

// Deselect an <option> based upon its text
selectObject.deselectByVisibleText("Bread");

// Deselect all selected <option> elements
selectObject.deselectAll();
```

```java
//find out if your <select> element can select multiple options 
Boolean allowMulti = selectObject.isMultiple();
```

```java
// Return a List<WebElement> of options that have been selected
List<WebElement> allSelectedOptions = selectObject.getAllSelectedOptions();

// Return a WebElement referencing the first selection option found by walking down the DOM
WebElement firstSelectedOption = selectObject.getFirstSelectedOption();

// Return a List<WebElement> of options that the <select> element contains
List<WebElement> allAvailableOptions = selectObject.getOptions();
```

#### scroll webpage
要捲動網頁，可使用JavaScript的scrollBy()方法。要執行JavaScript方法，還需要使用JavaScript執行器。 
`scrollBy`方法根據畫素採用兩個引數，每個引數用於水平和垂直捲動。
```java
JavascriptExecutor js = (JavascriptExecutor)driver;  
js.executeScript("scrollBy(x, y)");  //scroll x and y by px
```
**Eg**
```java
js.executeScript("scrollBy(0, 1500)"); //scroll down by 1500px
```

#### Working with windows and tabs
```java
//Get window handle
driver.getWindowHandle();

//Store the ID of the original window
String originalWindow = driver.getWindowHandle();

// Opens a new tab and switches to new tab
driver.switchTo().newWindow(WindowType.TAB);

// Opens a new window and switches to new window
driver.switchTo().newWindow(WindowType.WINDOW);

//Close the tab or window
driver.close();

//Switch back to the old tab or window
driver.switchTo().window(originalWindow);

//Access each dimension individually
int width = driver.manage().window().getSize().getWidth();
int height = driver.manage().window().getSize().getHeight();

//Or store the dimensions and query them later
Dimension size = driver.manage().window().getSize();
int width1 = size.getWidth();
int height1 = size.getHeight();

//Set window size
driver.manage().window().setSize(new Dimension(1024, 768));

//Set window position
//Move the window to the top left of the primary monitor
driver.manage().window().setPosition(new Point(0, 0));

//maximize window
driver.manage().window().minimize();
//minimise window
driver.manage().window().minimize();

//full screen
driver.manage().window().fullscreen();

```
#### Execute JS sript
```java
//Creating the JavascriptExecutor interface object by Type casting
JavascriptExecutor js = (JavascriptExecutor)driver;
//Button Element
WebElement button =driver.findElement(By.name("btnLogin"));
//Executing JavaScript to click on element
js.executeScript("arguments[0].click();", button);
//Get return value from script
String text = (String) js.executeScript("return arguments[0].innerText", button);
//Executing JavaScript directly
js.executeScript("console.log('hello world')");
```

#### Working with iFrames and frames
```html
<div id="modal">
  <iframe id="buttonframe" name="myframe"  src="https://seleniumhq.github.io">
   <button>Click here</button>
 </iframe>
</div>
```
**Using a WebElement**
```java
/* Using a WebElement */
//Store the web element
WebElement iframe = driver.findElement(By.cssSelector("#modal>iframe"));
//Switch to the frame
driver.switchTo().frame(iframe);
//Now we can click the button
driver.findElement(By.tagName("button")).click();

/* Using a name or ID */
//Using the ID
driver.switchTo().frame("buttonframe");
//Or using the name instead
driver.switchTo().frame("myframe");
//Now we can click the button
driver.findElement(By.tagName("button")).click();

/* Using an index */
// Switches to the second frame
driver.switchTo().frame(1);

/* Leaving a frame */
// Return to the top level
driver.switchTo().defaultContent();
```


#### alerts in browser
```java
//Using Alert class to first switch to or focus to the alert box  
Alert alert = driver.switchTo().alert();
//Wait for the alert to be displayed and store it in a variable
Alert alert = wait.until(ExpectedConditions.alertIsPresent());
//Store the alert text in a variable
String text = alert.getText();
//Press the OK/confirm/accept button
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
//response text to the alert
driver.switchTo().alert().sendKeys("Text");
```

#### prompt
prompts are similar to confirm boxes, except they also include a text input
```java
//Wait for the alert to be displayed and store it in a variable
Alert alert = wait.until(ExpectedConditions.alertIsPresent());
//Type your message
alert.sendKeys("Selenium");
//Press the OK button
alert.accept();
``` 

#### TakeScreenshot
```java
import org.apache.commons.io.FileUtils;
import org.openqa.selenium.chrome.ChromeDriver;
import java.io.*;
import org.openqa.selenium.*;

public class SeleniumTakeScreenshot {
    public static void main(String args[]) throws IOException {
        WebDriver driver = new ChromeDriver();
        driver.get("http://www.example.com");
        File scrFile = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
        FileUtils.copyFile(scrFile, new File("./image.png"));
        driver.quit();
    }
}
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
Cucumber is a Behavior Driven Development tool used to develop test cases for the behavior of software's functionality. It plays a supporting role in automated testing. \
https://cucumber.io/docs/guides/overview/ \
https://cucumber.io/docs/guides/10-minute-tutorial/#see-scenario-reported-as-failing


### Xpath
- XPath stands for XML Path Language
- XPath can be used to navigate through elements and attributes in an XML document.
https://www.w3schools.com/xml/xpath_syntax.asp \
https://devhints.io/xpath

### JUnit
https://github.com/junit-team/junit4/wiki \
https://github.com/junit-team/junit5/wiki \
https://www.youtube.com/watch?v=vZm0lHciFsQ
