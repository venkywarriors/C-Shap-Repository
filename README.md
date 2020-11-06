# C-Shap-Repository
### System Collections
This repository contains generic collection programms used in C# <br>
:+1: Click this link to view <a href="https://github.com/venkywarriors619/C-Shap-Repository/blob/master/collections.md" title="Click here to view C# Collections">*C# Collection* </a><br>
:+1: Click this link to view <a href="https://github.com/venkywarriors619/C-Shap-Repository/blob/master/C-TitBits.md" title="Click here to view C# Basics Programm">*C# Basics* </a><br>
:+1: Click this link to view <a href="https://github.com/venkywarriors619/C-Shap-Repository/blob/master/DataDriven.md" title="Click here to view Data Driven function in C# ">*Data Driven Concepts* </a><br>
:+1: Click this link to view <a href="http://automationtesting.in/generating-extent-reports-csharp/" title="Click here to view Generating Extent Reports">*Generating Extent Reports* </a>and <a href="http://automationtesting.in/capture-screenshot-in-extent-reports-csharp/" title="Click here to view Capture Screenshot in Extent Reports">*Capture Screenshot in Extent Reports* </a><br>
:+1: Click this link to view <a href="https://github.com/venkywarriors/C-Shap-Repository/blob/master/Nunit.md" title="Click here to view Basic Nunit programs in C# ">*Basic Nunit programs* </a><br>
:+1: Click this link to view <a href="https://github.com/venkywarriors/C-Shap-Repository/blob/master/SQL.md" title="Click here to view SQL queries">*SQL queries*</a><br>
:+1: Click this link to view <a href="https://michaelscodingspot.com/debugging-part1/" title="Click here to view Debugging in Visual Studio">*Debugging in Visual Studio*</a><br>

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
### <a href="https://dotnettutorials.net/lesson/multiple-inheritance-csharp/">INTERFACE</a>
WebDriver itself is an Interface. So based on the above statement WebDriver driver = new FirefoxDriver(); WebDriver driver = new ChromeDriver(); we are initializing Firefox browser using Selenium WebDriver. <br>It means we are creating a reference variable (driver) of the interface (WebDriver) and creating an Object. Here WebDriver is an Interface as mentioned earlier and FirefoxDriver is a class.
<br>
An interface in Java looks similar to a class but both the interface and class are two different concepts.<br> An interface can have methods and variables just like the class but the methods declared in interface are by default abstract. We can achieve 100% abstraction and multiple inheritance in Java with Interface.
### INHERITANCE
We create a Base Class in the Framework to initialize WebDriver interface, WebDriver waits, Property files, Excels, etc., in the Base Class.
<br>
We extend the Base Class in other classes such as Tests and Utility Class. Extending one class into other class is known as Inheritance.We use Multi  level inheritznce
### POLYMORPHISM
1. Method Overloading in Java – This is an example of compile time (or static polymorphism)(or early binding)<br>
2. Method Overriding in Java – This is an example of runtime time (or dynamic polymorphism)(or late binding)<br> 
<strong>Three ways to overload a method</strong>
* Number of parameters.   add(int, int) or add(int, int, int)
* Data type of parameters.  add(int, int) or add(int, float)
* Sequence of Data type of parameters. add(int, float) or add(float, int)
* Invalid case of method overloading  if two methods have same name, same parameters and have different return type ex: int add(int, int) or float add(int, int)
* Valid case of method overloading  if two methods have same name, different parameters and have different return type ex: int add(int, int) or double add(float, int)
#### METHOD OVERLOADING
We use implicit wait in Selenium. Implicit wait is an example of overloading. In Implicit wait we use different time stamps such as SECONDS, MINUTES, HOURS etc.,
<br>
A class having multiple methods with same name but different parameters is called Method Overloading. Browser capabilities selenium is method overloading.
<br>
Some more examples of Method Overloading in Selenium are present in methods of Actions Class and Assert class in TestNG and driver.switchto().frame(parameter)
```
class Demo {
 public void displayPattern(){
   for(int i = 0; i < 10; i++) {
     System.out.print("*");
   }
 }
 private void displayPattern(char symbol) {
   for(int i = 0; i < 10; i++) {
     System.out.print(symbol);
   }
 }
 public static void main(String[] args) {
   Demo d1 = new Demo();
   d1.displayPattern();
   System.out.println("\n");
   d1.displayPattern('#');
 }
}

Output:
**********
##########
```
#### METHOD OVERRIDING
Browser capabilities selenium understand this you need to understand Overriding in Java.<br>
Declaring a method in child class which is already present in the parent class is called Method Overriding. Examples are get and navigate methods of different drivers in Selenium<br>
<strong>Rules of method overriding</strong>
* Argument list: The argument list of overriding method (method of child class) must match the Overridden method(the method of parent class). The data types of the arguments and their sequence should exactly match.
* Access Modifier of the overriding method (method of subclass) cannot be more restrictive than the overridden method of parent class. For e.g. if the Access Modifier of parent class method is public then the overriding method (child class method ) cannot have private, protected and default Access modifier,because all of these three access modifiers are more restrictive than public.
```
class MyBaseClass{
   public void disp()
   {
       System.out.println("Parent class method");
   }
}
class MyChildClass extends MyBaseClass{
   protected void disp(){
      System.out.println("Child class method");
   }
   public static void main( String args[]) {
      MyChildClass obj = new MyChildClass();
      obj.disp();
   }
}
Output:

Exception in thread "main" java.lang.Error: Unresolved compilation 
problem: Cannot reduce the visibility of the inherited method from MyBaseClass
```
This is <strong>not allowed </strong>as child class disp method is more restrictive(protected) than base class(public)
```
class MyBaseClass{
   protected void disp()
   {
       System.out.println("Parent class method");
   }
}
class MyChildClass extends MyBaseClass{
   public void disp(){
      System.out.println("Child class method");
   }
   public static void main( String args[]) {
      MyChildClass obj = new MyChildClass();
      obj.disp();
   }
}
Output:

Child class method
```
However this is <strong>perfectly valid scenario</strong> as public is less restrictive than protected. Same access modifier is also a valid one.
* Private, static and final methods cannot be overridden as they are local to the class. However static methods can be re-declared in the sub class, in this case the sub-class method would act differently and will have nothing to do with the same static method of parent class.<br>
<a href="https://www.toolsqa.com/selenium-webdriver/retry-failed-tests-testng/">Retrying a failed test case</a> in TestNG is example for Method Overriding.
##### Examples of Method Overriding
In the WebDriver interface, we use two different methods for navigating or accessing any website i.e. <strong>driver.get() and driver.navigate().to(). these two methods are examples of Method Overriding.</strong><br>
<strong>Enlisted below is the basic difference between the navigate() and get() method and this is frequently asked in Selenium Interviews.<br></strong>
* The get() method does not load the web page completely if you are going to do some other operation after loading a page. This is the reason for which get() is faster than navigate().
* Using get() method, you can not traverse back and forward whereas Navigate() supports back and forth traversal of a web page using navigate().forward() and navigate().back().
#### Super keyword in Method Overriding
```
class ABC{
   public void myMethod()
   {
	System.out.println("Overridden method");
   }	   
}
class Demo extends ABC{
   public void myMethod(){
	//This will call the myMethod() of parent class
	super.myMethod();
	System.out.println("Overriding method");
   }
   public static void main( String args[]) {
	Demo obj = new Demo();
	obj.myMethod();
   }
}
Output:

Overridden method
Overriding method
```
#### Runtime polymorphism can't be achieved by data members.
A method is overridden, not the data members, so runtime polymorphism can't be achieved by data members.
```
class Bike{  
 int speedlimit=90;  
}  
class Honda3 extends Bike{  
 int speedlimit=150;  
  
 public static void main(String args[]){  
  Bike obj=new Honda3();  
  System.out.println(obj.speedlimit);//90  
}  

Output:
90
```
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
### What Are Desired Capabilities?
Desired Capabilities class is a component of the org.openqa.selenium.remote.DesiredCapabilities package. It helps Selenium WebDriver set the properties for the browsers. Using different capabilities from Desired Capabilities class we can set the properties of browsers. For example, the name of the browser, the version of the browser, etc. We use these capabilities as key-value pairs to set them for browsers.<br>
<a href="https://www.guru99.com/desired-capabilities-selenium.html">Desired Capabilities selenium</a>
```
//Accept all certificates Chrome
DesiredCapabilities capability = DesiredCapabilities.Chrome();
capability.SetCapability(CapabilityType.ACCEPT_SSL_CERTS, true);
System.setProperty("webdriver.ie.driver","IEDriverServer.exe");
IWebDriver driver = new RemoteWebDriver(capability);

//Set Chrome options.
ChromeOptions options = new ChromeOptions();
DesiredCapabilities dc = DesiredCapabilities.Chrome();
dc.SetCapability(ChromeOptions.Capability, options);
IWebDriver driver = new RemoteWebDriver(dc);

//Turn off the JavaScript Firefox
FirefoxProfileManager profileManager = new FirefoxProfileManager();
FirefoxProfile profile = profileManager.GetProfile("TestProfile");
profile.SetPreference("javascript.enabled", false);
IWebDriver driver = new FirefoxDriver(profile);

//Set the default page load timeout
driver.Manage().Timeouts().SetPageLoadTimeout(new TimeSpan(10));

//Start Firefox with plugins
FirefoxProfile prof = new FirefoxProfile();
profile.AddExtension(@"C:Location of extension.xpi");
IWebDriver driver = new FirefoxDriver(prof);

//Start Chrome with an unpacked extension
ChromeOptions options = new ChromeOptions();
options.AddArguments("load-extension=/pathTo/extension");
DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.SetCapability(ChromeOptions.Capability, options);
DesiredCapabilities dc = DesiredCapabilities.Chrome();
dc.SetCapability(ChromeOptions.Capability, options);
IWebDriver driver = new RemoteWebDriver(dc);

//Start Chrome with a packed extension
ChromeOptions options = new ChromeOptions();
options.AddExtension(Path.GetFullPath("localpathto/extension.crx"));
DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.SetCapability(ChromeOptions.Capability, options);
DesiredCapabilities dc = DesiredCapabilities.Chrome();
dc.SetCapability(ChromeOptions.Capability, options);
IWebDriver driver = new RemoteWebDriver(dc);
```
### Automate Attachmate IBM Reflection 2014 Terminal
```
using System;
using System.Configuration;
using Attachmate. Reflection Framework;
using Attachmate. Reflection. Emulation. IbmHosts;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SIG_TRS_FEED_AUTOMATION

class MainframeLayer
{
public Application reflectionApplication = null;
string sessionPath = Environment.GetEnvironmentVariable("USERPROFILE") + Configuration Manager.AppSettings.Get("screenPath");

public string ReadDataFromMainframeConsole(int x, int y, int length)
{
try
{
IIbmScreen screen - GetScreenObject();
string value = screen. GetText(x, y, length);
return !string.IsNullOrEmpty(value) ? value : null;
}
catch (Exception ex)
{
throw ex;
}
}

public IIbmScreen GetScreenObject()
{
IIbmScreen screen = null;
reflection pplication = MyReflection.ActiveApplication;
if (reflectionApplication != null)
object[] terminals = reflectionApplication.GetControlsByFilePath(sessionPath);
if (terminals != null & terminals.Length > 0)
{
IIbmTerminal terminal = (IIbm Terminal)terminals[0];
screen = terminal.Screen;
}
}
return screen;
}

public bool ValidateApollo()
{
bool isApolloOpened = false;
IIbmScreen screen = GetScreenObject();
if (screen.Get Text(7, 35, 6).Equals("APOLLO")))
{
isApolloOpened = true;
}
return isApolloOpened;
}

public bool ValidateMainFrameScreen(string screen_Name)
{
bool isMatched = false;
try
{
IIbmScreen screen = GetScreenObject();
if (screen.GetText(1, 73, 7).Equals(screen_Name))
{
isMatched = true;
}
}
catch (Exception ex)
{
throw (ex);
}
return isMatched;
}

public bool CheckMainframeIsOpened()
{
reflectionApplication = MyReflection. ActiveApplication;
return reflectionApplication != null ? true : false;
}

public void SetCursorPosition(int x, int y) 
{
IIbmScreen screen = GetScreenObject();
screen. SetSelection StartPos(x, y);
}

```
