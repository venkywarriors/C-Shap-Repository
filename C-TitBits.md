### :dart:Check string value null or Empty and assign default value
```
IWebElement lstTrElem = this.Driver.FindElement(By.Xpath("//select[@class='Rumor']")));
String actualValue= string.Empty;
actualValue=lstTrElem.Text; 

if(string.IsNullOrEmpty(actualValue))
{
	actualValue=!string.IsNullOrEmpty(lstTrElem.GetAttribute("value")) ? lstTrElem.GetAttribute("value") : "0";
}
```
### :dart:NUnit - Is it possible to check in the TearDown whether the test succeeded?
```
[TearDown]
        public override void AfterEach()
        {
            if (TestContext.CurrentContext.Result.Status != TestStatus.Passed)
            {
                Screenshot screenshot = driver.GetScreenshot();
                screenshot.SaveAsFile("Screenshots\\" + DateTime.Now.ToString("yyyyMMdd_HHmm_") + TestContext.CurrentContext.Test.Name + ".png", System.Drawing.Imaging.ImageFormat.Png);
                // Dismiss alerts
                Helpers.AcceptAlert(driver);
                IEnumerable<IWebElement> EditCowButtons;
                if ((EditCowButtons = driver.FindElements(InseminationScreen.EditCowButton)).Any())
                {
                    EditCowButtons.First().Click();
                }
            }

            allPassed = allPassed && (TestContext.CurrentContext.Result.Outcome == NUnit.Framework.Interfaces.ResultState.Success);
        }
```
Using Nunit 3.0 you can achieve this with below lines...
```
TestContext.CurrentContext.Result.Outcome.Status

TestContext.CurrentContext.Result.Outcome.Status; (For test Execution Status)

TestContext.CurrentContext.Result.StackTrace; (For Stack Trace Message)

TestContext.CurrentContext.Result.Message; (For Test Result Message)

TestContext.CurrentContext.Test.Name; (For Test Method Name)
```
