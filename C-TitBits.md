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
### :dart:How to send email with attachment from C#
```
using System;
using System.Net.Mail;

        private void SendEmailNotification(string EmailContent, bool mSuccess)
        {
		string[] ToEmails="raga@jh.com,venky@jh.com,mani@jh.com";
		string subject="Test email";
		string content="Hi....";
            try
            {
                MailMessage mail = new MailMessage();
                SmtpClient SmtpServer = new SmtpClient("mail.manulife.com");
                mail.From = new MailAddress("your_email_address@gmail.com");
                		
		foreach(string mailIds in ToEmails)
		{
		  mail.To.Add(mailIds);
		}
		
		string Content = "<Html>"+EmailContent+"</Html>";
		mail.Subject = subject+(mSuccess ?" Completed successfully":"failed")+"for processing date: "+String.Format("{0:yyyy-MM-dd}", DateTime.Now);
		string endNote="<span style='font-family: sans-serif; font-size: 10px;color:#BBBBBB;'><b>"+"This is an automatically generated email, please do not reply ..."+"</b></span>";
		mail.Body ="<span style='font-family: Arial; font-size: 13px;color:#000000;'>"+mail.Subject+"<br><br>"+(mSuccess ?content:"<u>Error in detail</u>:"+content)+"<br><br>"+endNote;
                
		mail.IsBodyHtml=true;
                System.Net.Mail.Attachment attachment;
                attachment = new System.Net.Mail.Attachment("your attachment file");
                mail.Attachments.Add(attachment);

                //SmtpServer.Port = 587;
                //SmtpServer.Credentials = new System.Net.NetworkCredential("username", "password");
                //SmtpServer.EnableSsl = true;

                SmtpServer.Send(mail);
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }
    }
```
### :dart:Send Email in C#
Following code snippets demonstrate how to send an email with HTML body using Spire.Email in C# and VB.NET.<br>

Step 1: Create an instance of MailMessage class and specify sender and recipient in its constructor.<br>
```
MailAddress addressFrom = new MailAddress("jack.du@e-iceblue.com", "Jack Du");
MailAddress addressTo = new MailAddress("susanwong32@outlook.com");
MailMessage message = new MailMessage(addressFrom, addressTo);
```
Step 2: Set the creation date, subject and html body of the message.
```
message.Date = DateTime.Now;
message.Subject = "Sending Email with HTML Body";
string htmlString = @"<html>
                      <body>
                      <p>Dear Ms. Susan,</p>
                      <p>Thank you for your letter of yesterday inviting me to come for an interview on Friday afternoon, 5th July, at 2:30.
                              I shall be happy to be there as requested and will bring my diploma and other papers with me.</p>
                      <p>Sincerely,<br>-Jack</br></p>
                      </body>
                      </html>
                     ";   
message.BodyHtml = htmlString;
```
Step 3: Create a SmtpClient instance, set its properties, and send the email using SendOne() medthod.
```
SmtpClient client= new SmtpClient();
client.Host = "smtp.outlook.com";
client.Port = 587;
client.Username = addressFrom.Address;
client.Password = "password";
client.ConnectionProtocols = ConnectionProtocols.Ssl;
client.SendOne(message);
```
