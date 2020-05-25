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
