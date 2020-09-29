# C-Shap-Repository
### System Collections
This repository contains generic collection programms used in C# <br>
:+1: Click this link to view <a href="https://github.com/venkywarriors619/C-Shap-Repository/blob/master/collections.md" title="Click here to view C# Collections">*C# Collection* </a><br>
:+1: Click this link to view <a href="https://github.com/venkywarriors619/C-Shap-Repository/blob/master/C-TitBits.md" title="Click here to view C# Basics Programm">*C# Basics* </a><br>
:+1: Click this link to view <a href="https://github.com/venkywarriors619/C-Shap-Repository/blob/master/DataDriven.md" title="Click here to view Data Driven function in C# ">*Data Driven Concepts* </a><br>
:+1: Click this link to view <a href="http://automationtesting.in/generating-extent-reports-csharp/" title="Click here to view Generating Extent Reports">*Generating Extent Reports* </a>and <a href="http://automationtesting.in/capture-screenshot-in-extent-reports-csharp/" title="Click here to view Capture Screenshot in Extent Reports">*Capture Screenshot in Extent Reports* </a><br>
:+1: Click this link to view <a href="https://github.com/venkywarriors/C-Shap-Repository/blob/master/Nunit.md" title="Click here to view Basic Nunit programs in C# ">*Basic Nunit programs* </a><br>


### How to write XPath expressions
XPath is a technique in Selenium to navigate through the HTML structure of a page. XPath enables testers to navigate through the XML structure of any document, and this can be used on both HTML and XML documents. This post looks at various ways to use the XPath element in Selenium to select various elements.
<br>
<a href="https://www.lambdatest.com/blog/complete-guide-for-using-xpath-in-selenium-with-examples/">XPath In Selenium With Examples</a><br>
<a href="https://www.guru99.com/xpath-selenium.html">Different XPath expression</a>

### How to Use CSS Selector for Identifying Web Elements for Selenium
Selector Pattern is constructed using HTML tags, attributes and their values. The central theme behind the procedure to create CSS Selector and Xpath are very much similar underlying the only difference in their construction protocol.

Like Xpath, CSS selector can also locate web elements having no ID, class or Name.<br>
<a href="https://www.browserstack.com/guide/css-selectors-in-selenium">CSS Selector to locate web elements</a>
<a href="https://www.guru99.com/locators-in-selenium-ide.html">Locating by CSS Selector</a>

### The difference between driver.switchTo().defaultContent() and driver.switchTo().parentFrame() <br>
first method switches the control to the main web page regardless of the number of frames within the web page<br>
while the second method switches the control to the parent frame of the current frame.<br>

## OOPS in Automation Framework
### ABSTRACTION
In Page Object Model design pattern, we write locators (such as id, name, xpath etc.,) in a Page Class. We utilize these locators in tests but we can’t see these locators in the tests. Literally we hide the locators from the tests.
<br>
Abstraction is the methodology of hiding the implementation of internal details and showing the functionality to the users.
### INTERFACE
WebDriver itself is an Interface. So based on the above statement WebDriver driver = new FirefoxDriver(); WebDriver driver = new ChromeDriver(); we are initializing Firefox browser using Selenium WebDriver. It means we are creating a reference variable (driver) of the interface (WebDriver) and creating an Object. Here WebDriver is an Interface as mentioned earlier and FirefoxDriver is a class.
<br>
An interface in Java looks similar to a class but both the interface and class are two different concepts. An interface can have methods and variables just like the class but the methods declared in interface are by default abstract. We can achieve 100% abstraction and multiple inheritance in Java with Interface.
### INHERITANCE
We create a Base Class in the Framework to initialize WebDriver interface, WebDriver waits, Property files, Excels, etc., in the Base Class.
<br>
We extend the Base Class in other classes such as Tests and Utility Class. Extending one class into other class is known as Inheritance.We use Multi  level inheritznce
### POLYMORPHISM
#### METHOD OVERLOADING
We use implicit wait in Selenium. Implicit wait is an example of overloading. In Implicit wait we use different time stamps such as SECONDS, MINUTES, HOURS etc.,
<br>
A class having multiple methods with same name but different parameters is called Method Overloading. Browser capabilities selenium is method overloading.
<br>
Some more examples of Method Overloading in Selenium are present in methods of Actions Class and Assert class in TestNG as shown below:
#### METHOD OVERRIDING
We use a method which was already implemented in another class by changing its parameters. To.browser capabilities selenium understand this you need to understand Overriding in Java.<br>
Declaring a method in child class which is already present in the parent class is called Method Overriding. Examples are get and navigate methods of different drivers in Selenium<br>
##### Examples of Method Overriding
In the WebDriver interface, we use two different methods for navigating or accessing any website i.e. driver.get() and driver.navigate().to().
<br>These two methods are examples of Method Overriding.<br>
Enlisted below is the basic difference between the navigate() and get() method and this is frequently asked in Selenium Interviews.<br>

* The get() method does not load the web page completely if you are going to do some other operation after loading a page. This is the reason for which get() is faster than navigate().
* Using get() method, you can not traverse back and forward whereas Navigate() supports back and forth traversal of a web page using navigate().forward() and navigate().back().
### ENCAPSULATION
The classes in a framework are an example of Encapsulation. In these POM Classes, we declare the data members using @FindBy and initialize them using a constructor with initElement() to utilize them in the test methods.
<br>Encapsulation is a mechanism of binding code and data together in a single unit.
#### WEB ELEMENT:
Web element is an interface used to identify the elements in a web page.
#### WEBDRIVER:
WebDriver is an interface used to launch different browsers such as Firefox, Chrome, Internet Explorer, Safari etc.,
#### FIND BY:
FindBy is an annotation used in Page Object Model design pattern to identify the elements.
#### FIND ELEMENT:
Find Element is a method in POM to identify the elements in a web page.
