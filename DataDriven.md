### :dart:Read Configuration File in C# using ConfigurationManager
Add Reference to ConfigurationManager
Right Click on the References and select Add Reference... Now search for System.ConfigurationManager. Select it and this will add to your Project References
App.config File
```
<configuration>
 <connectionStrings>
 <add name="DBConnection" connectionString="Data Source=(LocalDB)\v11.0;Initial Catalog=WingtipToys;Integrated Security=True;Pooling=False"/>
 </connectionStrings>
</configuration>
```
The code in c# to read the config strings will be like this:
```
var dbString = ConfigurationManager.ConnectionStrings[“DBConnection”].ConnectionString;
```
App.config File
```
<configuration>
    <appSettings>
          <add key="URL" value="http://www.store.demoqa.com"/>
   <add key="FolderPath"="C:\Users\lakshay.sharma\Downloads\"/>
    </appSettings>
</configuration>
```
To read the Url from the above config file, use the below code:
```
var url = ConfigurationManager.AppSettings[“URL”];

var folderPath = ConfigurationManager.AppSettings[“FolderPath”];
```
### :dart:Read Configuration File in C# using ConfigurationManager
Add Reference to ConfigurationManager
Right Click on the References and select Add Reference... Now search for System.ConfigurationManager. Select it and this will add to your Project References
```
IWebElement lstTrElem = this.Driver.FindElement(By.Xpath("//select[@class='Rumor']")));
String actualValue= string.Empty;
actualValue=lstTrElem.Text; 

if(string.IsNullOrEmpty(actualValue))
{
	actualValue=!string.IsNullOrEmpty(lstTrElem.GetAttribute("value")) ? lstTrElem.GetAttribute("value") : "0";
}
```
