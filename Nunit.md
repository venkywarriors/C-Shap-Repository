[Basic Nunit Program](https://github.com/venkywarriors/C-Shap-Repository/blob/master/nunit.pdf)<br>
# Testing Framework Comparison

| Feature | NUnit | MSTest | xUnit |
| --- | --- | --- | --- |
| **Test Class Attribute** | `[TestFixture]` | `[TestClass]` | `[TestClass]` |
| **Test Method Attribute** | `[Test]` | `[TestMethod]` | `[Fact]` |
| **Test Initialization** | `[SetUp]` | `[TestInitialize]` | Constructor or `[ClassFixture]` |
| **Test Cleanup** | `[TearDown]` | `[TestCleanup]` | Destructor or `[ClassFixture]` |
| **Class Initialization** | `[TestFixtureSetUp]` | `[ClassInitialize]` | N/A |
| **Class Cleanup** | `[TestFixtureTearDown]` | `[ClassCleanup]` | N/A |
| **One-Time Initialization for All Tests in One Class** | `[OneTimeSetUp]` `[OneTimeTearDown]` | `[MemberData]` Or `[ClassData]` `[MethodMember]` or `[PropertyMember]` | `[ClassInitialize]` `[ClassCleanup]` |
| **One-Time Initialization for All Tests in One Assembly** | Dedicated class with `[SetUpFixture]` + `[OneTimeSetUp]` `[OneTimeTearDown]` | `[MemberData]` Or `[ClassData]`,`[PropertyMember]` | `[TestClass]` + `[AssemblyInitialize]` `[AssemblyCleanup]` |
| **Skipping a Test** | `[Fact (Skip="reason")]` | `[Ignore("reason")]` | `[Ignore]` |
| **Timeout Value for Test Cases in Execution** | `[TimeOut]` | `[Timeout(5000)]` | `Timeout(1000)` |
| **Re-runs the Test Cases** | `[Retry]` | Install the `MSTest.TestFramework` NuGet package: `[RetryTest(3)]` | Install the `Xunit.Retry` NuGet package: `[RetryFact(MaxRetries = 3)]` |
| **Marks the Method as a Test and Passes Inline Parameters for Parameterized Tests** | `[TestCase]` | `[TestMethod]` `[DataRow(1, 2, 3)]` | `[Theory]` `[InlineData(1, 2, 3)]` |
| **Random Value for Parameterized Tests** | `[Random]` | | |
| **Marks a Test Method Expected to Throw a Particular Exception Type** | `[ExpectedException(ExceptionType)]` | `[ExpectedException(typeof(MyCustomException), "ExpectedMessage")]` | Use `Assert.Throws<T>` |
| **Set Priority** | `[Test, Order(1)]` | Create a custom attribute (TestPriority in this example): `[Fact, TestPriority(1)]` | `IClassFixture` interface and the `IUseFixture` interface |
| **Categorize Test Cases or Classes** | `[Category()]` | `[TestCategory("")]` | `[Trait("Category", "")]` |
| **Identifies a Method That Needs to Be Called Before the Execution of Any Tests in Test Assembly** | N/A | `[AssemblyInitialize]` | N/A |
| **Identifies a Method That Needs to Be Called After Execution of Tests in Test Assembly** | N/A | `[AssemblyCleanUp]` | N/A |
| **Attribute Adds Information About the Author of the Tests** | `[Author("John Doe")]` | `[Owner("John Doe")]` | Use `ITestOutputHelper` interface: `[Trait("Author", "John Doe")]` |
| **Parallelism** | `[assembly: LevelOfParallelism(3)]` | N/A | `[assembly: CollectionBehavior(DisableTestParallelization = false)]` `[Collection("YourCollectionName")]` |
| **Attribute Used for Maximum Time in Milliseconds for a Test Case** | `[Test, MaxTime(2000)]` | | |
| **Attribute Used on a Test Method to Specify Execution Multiple Times** | `[Repeat(25)]` | `[TestMethod]` `[DataRow(1)]` | `[Theory]` `[InlineData(1)]` |
| **Sets the Description Property of the Test** | `[Test]` `[Description("This is a description of the test")]` | `[TestMethod]` `[Description("This is a description of the test")]` | `/// <summary>` `/// This is a description of the test` `/// </summary>` `[Fact]` |

### :dart:Run tests in parallel<br> 
In NUnit, the ParallelScope is an enumeration that determines the scope of parallel execution for tests. It allows you to control which level of the test hierarchy (assembly, namespace, fixture, or individual test) should run in parallel.

The ParallelScope enum has the following values:

- None: No parallel execution. Tests are executed sequentially.
- Self: Tests in the same fixture (class) can run in parallel, but different fixtures run sequentially.
- Children: Child items of the same parent (e.g., tests in the same namespace or fixture) can run in parallel, but different parents run sequentially.
- Fixtures: Entire fixtures (classes) can run in parallel, but different fixtures run sequentially.
- All: All tests, regardless of their hierarchy, can run in parallel.

Here is an example of how to use ParallelScope in NUnit:
### At Assembly Level:
```
[assembly: Parallelizable(ParallelScope.Fixtures)]
```
This attribute specifies that all fixtures (test classes) in the assembly can be run in parallel.
### At Assembly Level:
```
[assembly: Parallelizable(ParallelScope.Fixtures)]
```
### At Class Level:
```
[Parallelizable(ParallelScope.Children)]
public class YourTestClass
{
    // Your test methods here
}
```
This attribute specifies that all test methods within the class can be run in parallel.
### At Method Level:
```
[Test, Parallelizable(ParallelScope.Self)]
public void YourTestMethod()
{
    // Your test logic here
}
```
### :dart:PageObjects and PageFactory in C#<br> 
The PageObject Design Pattern models areas of an UI as objects within test code which can also be considered as Object Repository for Web UI Elements. The functionality classes (PageObjects) in this design represent a logical relationship between the pages of the application. Each class is referred to as a PageObjects and returns other PageObjects to facilitate the flow between pages. Page Object class is responsible to find the WebElements of that page and also hold methods that perform operations on those WebElements.
```
using OpenQA.Selenium;
using OpenQA.Selenium.Support.PageObjects;

namespace OnlineStore.PageObjects
{
    public class LoginPage
    {
        private IWebDriver driver;

        [FindsBy(How = How.Id, Using = "log")]
        public IWebElement UserName { get; set; }

        [FindsBy(How = How.Id, Using = "pwd")]
        public IWebElement Password { get; set; }

        [FindsBy(How = How.Id, Using = "login")]
        public IWebElement Submit { get; set; }
    }
}
```
```
using NUnit.Framework;
using OnlineStore.PageObjects;
using OpenQA.Selenium;
using OpenQA.Selenium.Firefox;
using OpenQA.Selenium.Support.PageObjects;

namespace OnlineStore.TestCases
{

    class LogInTest
    {
        [Test]
        public void Test() {

            IWebDriver driver = new FirefoxDriver();
            driver.Url = "https://www.store.demoqa.com";

            var homePage = new HomePage();
            PageFactory.InitElements(driver, homePage);
            homePage.MyAccount.Click();

            var loginPage = new LoginPage();
            PageFactory.InitElements(driver, loginPage);
            loginPage.UserName.SendKeys("TestUser_1");
            loginPage.Password.SendKeys("Test@123");
            loginPage.Submit.Submit();
        }    

    }
}
```
#### PageFactory CacheLookup<br>
PageFactory also provide CacheLookup attribute to cache the WebElements. This attribute helps scripts to instruct the InitElements method to cache the element once it’s located. In other words, any attribute marked [CacheLookup] will not be searched over and over again – this is especially useful for elements that are always going to be there (not always true for AJAX apps). It means the elements of the page will be cached once searched. All elements used in the HomePage & LoginPage class are static and are always present. So it is better to cache objects and save execution time of the test run.
```
[FindsBy(How = How.Id, Using = “account”)]
[CacheLookup]
public IWebElement MyAccount { get; set; }
```
PageFactory functionality resides in <strong>OpenQA.Selenium.Support.PageObjects.CacheLookupAttribute.</strong><br>

<strong> Optimizing Page Object Model for selenium version >3.11 <br> </strong>
```
using OpenQA.Selenium;
using OpenQA.Selenium.Support.PageObjects;

namespace OnlineStore.PageObjects
{
    public class LoginPage
    {
        private RemoteWebDriver _driver;

        public LoginPage(RemoteWebDriver _driver) => _driver=driver; 

        IWebElement city => _driver.findElementByName("city");
        IWebElement state => _driver.findElementByName("state");
     }

}

```
<strong>Advantages</strong><br>
* When the PageFactory is initialised the proxies are configured, but the WebElements are not found at that point (so you won’t get a NoSuchElementException).
* Every time you use a WebElement it will go and find it again so you shouldn’t see StaleElementException’s.
* But when you use the @CacheLookup annotation, which is losing you the second benefit as it will find the element once and then keep a reference to it, you are now far more likely to see StaleElementExceptions.<br>
<strong>Differences between C# and Java Implementation</strong><br>
* In C# the PageFactory.InitElements returns void, whereas in Java it returns the Page Objects.<br>
* The PageFactory implementation for C# only searches for elements using the ID. It does not locate the elements using the NAME property. Whereas in Java it also tries to find the element with Name property, if it is not able to find it with ID.<br>
* The Java implementation can locate the element even without the FindsBy attribute. This isn’t the case for C#.<br>
