### :dart:PageObjects and PageFactory in C#<br> 
The PageObject Design Pattern models areas of an UI as objects within test code which can also be considered as Object Repository for Web UI Elements. The functionality classes (PageObjects) in this design represent a logical relationship between the pages of the application. Each class is referred to as a PageObjects and returns other PageObjects to facilitate the flow between pages. Page Object class is responsible to find the WebElements of that page and also hold methods that perform operations on those WebElements.
```
FindsBy(How = How.Id, Using = “username“)]
private IWebElement UserName { get; set; }
```
#### PageFactory CacheLookup<br>
PageFactory also provide CacheLookup attribute to cache the WebElements. This attribute helps scripts to instruct the InitElements method to cache the element once it’s located. In other words, any attribute marked [CacheLookup] will not be searched over and over again – this is especially useful for elements that are always going to be there (not always true for AJAX apps). It means the elements of the page will be cached once searched. All elements used in the HomePage & LoginPage class are static and are always present. So it is better to cache objects and save execution time of the test run.
```
[FindsBy(How = How.Id, Using = “account”)]
[CacheLookup]
public IWebElement MyAccount { get; set; }
```
PageFactory functionality resides in <strong>OpenQA.Selenium.Support.PageObjects.CacheLookupAttribute.</strong><br>
<br><strong>Advantages</strong><br>
<ol>
<li>When the PageFactory is initialised the proxies are configured, but the WebElements are not found at that point (so you won’t get a NoSuchElementException).</li>
<li>Every time you use a WebElement it will go and find it again so you shouldn’t see StaleElementException’s.</li>
<li>But when you use the @CacheLookup annotation, which is losing you the second benefit as it will find the element once and then keep a reference to it, you are now far more likely to see StaleElementExceptions.</li>
</ol>
<br><strong>Differences between C# and Java Implementation</strong><br>
<ol>
<li>In C# the PageFactory.InitElements returns void, whereas in Java it returns the Page Objects.<br></li>
<li>The PageFactory implementation for C# only searches for elements using the ID. It does not locate the elements using the NAME property. Whereas in Java it also tries to find the element with Name property, if it is not able to find it with ID.<br></li>
<li>The Java implementation can locate the element even without the FindsBy attribute. This isn’t the case for C#. </li>
</ol>
### :dart:PageObjects and PageFactory in C#<br> 
