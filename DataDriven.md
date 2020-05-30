### :dart:Read Configuration File in C# using ConfigurationManager
Connection strings can be stored as key/value pairs in the connectionStrings section of the configuration element of an application configuration file. Child elements include add, clear, and remove.

Step 1: Right-click on references tab to add reference.<br>
Step 2: Click on Assemblies tab<br>
Step 3: Search for 'System.Configuration'<br>
Step 4: Click OK.<br>
<img src="https://toolsqa.com/wp-content/gallery/csharp/ConfigurationManager_1.png" alt="Configuration Manager" width="1000" height="400">
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

var folderPath = ConfigurationManager.AppSettings.Get(“FolderPath”);
```
Another possible solution:
```
var MyReader = new System.Configuration.AppSettingsReader();
string keyvalue = MyReader.GetValue("keyalue",typeof(string)).ToString();
```
App.config File
```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <configSections>
    <sectionGroup name="BlogGroup">
      <section name="PostSetting" type="System.Configuration.NameValueSectionHandler"/>
    </sectionGroup>
    <section name="ProductSettings" type="ConfigurationExample.ProductSettings, ConfigurationExample"/>
  </configSections>

  <BlogGroup>
    <PostSetting>
      <add key="PostName" value="Getting Started With Config Section in .Net"/>
      <add key="Category" value="C#"></add>
      <add key="Author" value="Mukesh Kumar"></add>
      <add key="PostedDate" value="28 Feb 2017"></add>
    </PostSetting>
  </BlogGroup>

  <ProductSettings>
    <DellSettings ProductNumber="20001" ProductName="Dell Inspiron" Color="Black" Warranty="2 Years" ></DellSettings>
  </ProductSettings>

  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
  </startup>
</configuration>
```
To read these types of configuration setting, we need to access section based on section group and then we can get all the keys and their values as following code is doing.
```
public static void GetConfigurationUsingSectionGroup()
{
    var PostSetting = ConfigurationManager.GetSection("BlogGroup/PostSetting") as NameValueCollection;
    if (PostSetting.Count == 0)
    {
        Console.WriteLine("Post Settings are not defined");
    }
    else
    {
        foreach (var key in PostSetting.AllKeys)
        {
            Console.WriteLine(key + " = " + PostSetting[key]);
        }
    }
}
```
### :dart:Connect C# to MySQL
We will start by adding the MySql Connector library:
```
//Add MySql Library
using MySql.Data.MySqlClient;
```
The code in c# to read the data from DB :
```
class DBConnect
{
    private SqlConnection connection;
    private string server;
    private string database;
    private string uid;
    private string password;

    //Constructor
    public DBConnect()
    {
        Initialize();
    }

    //Initialize values
    private void Initialize()
    {
        server = "localhost"
        database = "connectcsharptomysql";
        uid = "username";
        password = "password";
        string connectionString;
        connectionString = "Data Source=" + server + ";" + "Initial Catalog=" + 
		database + ";" + "UID=" + uid + ";" + "PASSWORD=" + password + ";";

        connection = new SqlConnection(connectionString);
    }

//open connection to database
private bool OpenConnection()
{
    try
    {
        connection.Open();
        return true;
    }
    catch (MySqlException ex)
    {
	Console.WriteLine(ex.Message);
        return false;
    }
}

//Close connection
private bool CloseConnection()
{
    try
    {
        connection.Close();
        return true;
    }
    catch (MySqlException ex)
    {
        Console.WriteLine(ex.Message);
        return false;
    }
}

public List< string > Select()
{
    string query = "SELECT * FROM tableinfo";

    //Create a list to store the result
    List< string > list = new List< string >();


    //Open connection
    if (this.OpenConnection() == true)
    {
        //Create Command
        SqlCommand cmd = new SqlCommand(query, connection);
        //Create a data reader and Execute the command
        DataReader dataReader = cmd.ExecuteReader();
        //Column Count 
	int rowCount dataReader.VisibleFieldCount;
        //Read the data and store them in the list
        while (dataReader.Read())
        {
            list.Add(dataReader["id"]);
            list.Add(dataReader["name"]);
            list.Add(dataReader["age"]);
        }

        //close Data Reader
        dataReader.Close();

        //close Connection
        this.CloseConnection();

        //return list to be displayed
        return list;
    }
    else
    {
        return list;
    }
}

//Get data from SQL
public List< string > GetDataFromDB()
{
    string query = @"SELECT * FROM tableinfo";

    //Create a list to store the result
    List< string > list = new List< string >();


    //Open connection
    if (this.OpenConnection() == true)
    {
        //Create Command
        SqlCommand cmd = new SqlCommand(query, connection);
        //Create a data reader and Execute the command
        DataReader dataReader = cmd.ExecuteReader();
        
        //Read the data and store them in the list
        DataTable dataTable = new DataTable();
	dataTable.Load(dataReader);
	//Read Row count
	int rowCount = dataTable.Rows.Count;
	//Read Column count
	int colCount = dataTable.Columns.Count;
	//Read Column names
	foreach (DataRow col in dataTable.columns)
	{
	   list.add(col.ColumnName);
	}			
	foreach (DataRow row in dataTable.Rows)
	{
		foreach (DataRow col in dataTable.columns)
		{
	   		list.add(Convert.ToString(row[col.ColumnName]));
		}
	}			
	
        //close Data Reader
        dataReader.Close();

        //close Connection
        this.CloseConnection();

        //return list to be displayed
        return list;
    }
    else
    {
        return list;
    }
}

//Get Rows Count
public int RowsCont()
{
    string query = "SELECT * FROM tableinfo";
	int count=0;
    //Open connection
    if (this.OpenConnection() == true)
    {
        //Create Command
        SqlCommand cmd = new SqlCommand(query, connection);
        //Create a data reader and Execute the command
        DataReader dataReader = cmd.ExecuteReader();

        while (dataReader.Read())
        {
           count++;
        }
	return count;
dataReader.close();	
}
```
### :dart:Read and Write Data in Excel sheet using Microsoft.Office.Interop.Excel
For this we need to have the below pre-requisites:

Create a Console Application in Visual Studio
Install Office.Interop.Excel Nuget Package by following below steps
Under your Console Application, Right Click on reference, Click on Manage Nuget Package
Go to Browse
Under Browse search for “Microsoft.Office.Interop.Excel”
click on “Microsoft.Office.Interop.Excel” and then Click Install
Make sure that your package got installed and appears under References folder under your Console App.
```
using System;
using System.Collections;
using System.Runtime.InteropServices;
using xl = Microsoft.Office.Interop.Excel;
 
namespace CSharpPractice
{
    class ExcelApiTest
    {
        xl.Application xlApp = null;
        xl.Workbooks workbooks = null;
        xl.Workbook workbook = null;
        Hashtable sheets;
        public string xlFilePath;
 
        public ExcelApiTest(string xlFilePath)
        {
            this.xlFilePath = xlFilePath;
        }
 
        public void OpenExcel()
        {
            xlApp = new xl.Application();
            workbooks = xlApp.Workbooks;
            workbook = workbooks.Open(xlFilePath);
            sheets = new Hashtable();
            int count = 1;
            // Storing worksheet names in Hashtable.
            foreach (xl.Worksheet sheet in workbook.Sheets)
            {
                sheets[count] = sheet.Name;
                count++;
            }
        }
 
        public void CloseExcel()
        {
            workbook.Close(false, xlFilePath, null); // Close the connection to workbook
            Marshal.FinalReleaseComObject(workbook); // Release unmanaged object references.
            workbook = null;
 
            workbooks.Close();
            Marshal.FinalReleaseComObject(workbooks);
            workbooks = null;
 
            xlApp.Quit();
            Marshal.FinalReleaseComObject(xlApp);
            xlApp = null;
        }
	
	public void CreateExcelDocument()
	{
	// If you are a commercial business and have
	// purchased commercial licenses use the static property
	// LicenseContext of the ExcelPackage class:
	ExcelPackage.LicenseContext = LicenseContext.Commercial;

	// If you use EPPlus in a noncommercial context
	// according to the Polyform Noncommercial license:
	ExcelPackage.LicenseContext = LicenseContext.NonCommercial;
	    String path = @"D:\temp\testsheet3.xlsx";
	    using (ExcelPackage excel = new ExcelPackage())
	    {
		excel.Workbook.Worksheets.Add("Sheet1"); 
		FileInfo newFile = new FileInfo(path);
		excel.SaveAs(newFile)
		//Close Excel package 
		excel.Dispose(); 
	    }
	}

	public void AddNewSheet(string sheetName)
	{
		OpenExcel();
		workbook.Sheets.Add(After: workbook.Sheets[workbook.Sheets.Count]);
		xl.Worksheet worksheet = workbook.Worksheets[workbook.Sheets.Count] as xl.Worksheet;
		workbook.Name = sheetName;            
		workbook.Save();
		workbook.Close();
		CloseExcel();
	}
	//Below are the Methods will use to get the CellData using Column number
        public string GetCellData(string sheetName, int colNumber, int rowNumber)
        {
            OpenExcel();
 
            string value = string.Empty;
            int sheetValue = 0;
 
            if (sheets.ContainsValue(sheetName))
            {
                foreach (DictionaryEntry sheet in sheets)
                {
                    if (sheet.Value.Equals(sheetName))
                    {
                        sheetValue = (int)sheet.Key;
                    }
                }
                xl.Worksheet worksheet = null;
                worksheet = workbook.Worksheets[sheetValue] as xl.Worksheet;
                xl.Range range = worksheet.UsedRange;
 
                value = Convert.ToString((range.Cells[rowNumber, colNumber] as xl.Range).Value2);
                Marshal.FinalReleaseComObject(worksheet);
                worksheet = null;
            }
            CloseExcel();
            return value;
        }

	//Methods will use to get the CellData using Column name
	public string GetCellData(string sheetName, string colName, int rowNumber)
        {
            OpenExcel();
 
            string value = string.Empty;
            int sheetValue = 0;
            int colNumber = 0;
 
            if (sheets.ContainsValue(sheetName))
            {
                foreach (DictionaryEntry sheet in sheets)
                {
                    if (sheet.Value.Equals(sheetName))
                    {
                        sheetValue = (int)sheet.Key;
                    }
                }
                xl.Worksheet worksheet = null;
                worksheet = workbook.Worksheets[sheetValue] as xl.Worksheet;
                xl.Range range = worksheet.UsedRange;
 
                for (int i = 1; i <= range.Columns.Count; i++)
                {
                    string colNameValue = Convert.ToString((range.Cells[1,i] as xl.Range).Value2);
 
                    if (colNameValue.ToLower() == colName.ToLower())
                    {
                        colNumber = i;
                        break;
                    }
                }
 
                value = Convert.ToString((range.Cells[rowNumber, colNumber] as xl.Range).Value2);
                Marshal.FinalReleaseComObject(worksheet);
                worksheet = null;
            }
	}

	//Methods will use to set the cell data using column number
	public bool SetCellData(string sheetName, int colNumber, int rowNumber, string value)
        {
            OpenExcel();
 
            int sheetValue = 0;
 
            try
            {
                if (sheets.ContainsValue(sheetName))
                {
                    foreach (DictionaryEntry sheet in sheets)
                    {
                        if (sheet.Value.Equals(sheetName))
                        {
                            sheetValue = (int)sheet.Key;
                        }
                    }
 
                    xl.Worksheet worksheet = null;
                    worksheet = workbook.Worksheets[sheetValue] as xl.Worksheet;
                    xl.Range range = worksheet.UsedRange;
 
                    range.Cells[rowNumber, colNumber] = value;
 
                    workbook.Save();
 
                    Marshal.FinalReleaseComObject(worksheet);
                    worksheet = null;
                    CloseExcel();
                }
            }
            catch (Exception ex)
            {
                return false;
            }
            return true;
        }

 //Methods will use to set the cell data using column name
  public bool SetCellData(string sheetName, string colName, int rowNumber, string value)
        {
            OpenExcel();
 
            int sheetValue = 0;
            int colNumber = 0;
 
            try
            {
                if (sheets.ContainsValue(sheetName))
                {
                    foreach (DictionaryEntry sheet in sheets)
                    {
                        if (sheet.Value.Equals(sheetName))
                        {
                            sheetValue = (int)sheet.Key;
                        }
                    }
 
                    xl.Worksheet worksheet = null;
                    worksheet = workbook.Worksheets[sheetValue] as xl.Worksheet;
                    xl.Range range = worksheet.UsedRange;
 
                    for (int i = 1; i <= range.Columns.Count; i++)
                    {
                        string colNameValue = Convert.ToString((range.Cells[1,i] as xl.Range).Value2);
                        if (colNameValue.ToLower() == colName.ToLower())
                        {
                            colNumber = i;
                            break;
                        }
                    }
 
                    range.Cells[rowNumber, colNumber] = value;
 
                    workbook.Save();
                    Marshal.FinalReleaseComObject(worksheet);
                    worksheet = null;
 
                    CloseExcel();
                }
            }
            catch (Exception ex)
            {
                return false;
            }
            return true;
        }
 
    public int GetColumnCount(string sheetName)
        {
            OpenExcel();
 
            int columnCount = 0;
            int sheetValue = 0;
 
            if (sheets.ContainsValue(sheetName))
            {
                foreach (DictionaryEntry sheet in sheets)
                {
                    if (sheet.Value.Equals(sheetName))
                    {
                        sheetValue = (int)sheet.Key;
                    }
                }
                xl.Worksheet worksheet = workbook.Worksheets[sheetValue] as xl.Worksheet;
                xl.Range range = worksheet.UsedRange;
                columnCount = range.Columns.Count;
            }
            CloseExcel();
 
            return columnCount;
        }

    public int GetRowCount(string sheetName)
        {
            OpenExcel();
             
            int rowCount = 0;
            int sheetValue = 0;
 
            if (sheets.ContainsValue(sheetName))
            {
                foreach (DictionaryEntry sheet in sheets) // Iterate over Hashtable
                {
                    if (sheet.Value.Equals(sheetName))
                    {
                        sheetValue = (int)sheet.Key;
                    }
                }
 
                // Getting particular worksheet using index/key from workbook
                xl.Worksheet worksheet = workbook.Worksheets[sheetValue] as xl.Worksheet;
                xl.Range range = worksheet.UsedRange; // Range of cells which is having content.
                rowCount = range.Rows.Count;
            }
 
            CloseExcel();
 
            return rowCount;
        }

    }
}
``` 
Main Method
``` 
static void Main(string[] args)
{
            string xlFilePath = @"d:\csharp-Excel.xls"
 
            ExcelApiTest eat = new ExcelApiTest(xlFilePath);
             
            int colCount = eat.GetColumnCount("Toranto");

            Console.Read();
}
```
### :dart:Read data from Visual Fox Pro database with C#
```
using System.Data;
using System.Data.OleDb;

public class YourClass
{
   public void GetYourData()
   {

	string connectionstring = @"Provider =VFPOLEDB.1;Data Source =C:\ARTIKEL.DBF;"; 
            string mySelectQuery = "SELECT * FROM ARTIKEL";
            OleDbConnection cnn = new OleDbConnection(connectionstring);
            OleDbCommand myCommand = new OleDbCommand(mySelectQuery, cnn);

	try
            {
                
                myCommand.Connection.Open();
                StringBuilder sb = new StringBuilder();
                IDataReader reader = myCommand.ExecuteReader();
                MessageBox.Show("Connection Open ! ");
                while (reader.Read())
                {
                    MessageBox.Show(reader[0].ToString());
                    sb.Append(string.Format("{0}, {1}", reader[0].ToString(), reader[1].ToString()) + System.Environment.NewLine);
                }
                reader.Close();                
                myCommand.Connection.Close();
            }
            catch (Exception ex)
            {
                MessageBox.Show(Convert.ToString(ex));
            }
	}
}
```
