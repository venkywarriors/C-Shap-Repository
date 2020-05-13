### Check string value null or Empty and assign default value

IWebElement lstTrElem = this.Driver.FindElement(By.Xpath("//select[@class='Rumor']")));
String actualValue= string.Empty;
actualValue=lstTrElem.Text; 

if(string.IsNullOrEmpty(actualValue))
{
	actualValue=!string.IsNullOrEmpty(lstTrElem.GetAttribute("value")) ? lstTrElem.GetAttribute("value") : "0";
}
