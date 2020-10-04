# System.Collections
## IDictionary<TKey,TValue> Interface <br> 
Assembly: Mscorlib.dll <br> 
Namespace: System.Collections <br> 
Summary: Represents a collection of key-and-value pairs. <br> 

The IDictionary class is the base interface for collections of key-and-value pairs.
Each element is a key-and-value pair stored in a DictionaryEntry object.

Dictionary cannot include duplicate or null keys, where as values can be duplicated or set as null. Dictionary maintains insertion order of keys.
### :dart:Add Elements into Dictionary<br> 

The IDictionary type instance has one more overload for the Add() method. It accepts a KeyValuePair<TKey, TValue> struct as a parameter.
```
IDictionary<int, string> dict = new Dictionary<int, string>();

dict.Add(new KeyValuePair<int, string>(1, "One"));
dict.Add(new KeyValuePair<int, string>(2, "Two"));

//The following is also valid
dict.Add(3, "Three");
```
### :dart:Dictionary Initialization<br> 
```
IDictionary<int, string> dict = new Dictionary<int, string>()
                                            {
                                                {1,"One"},
                                                {2, "Two"},
                                                {3,"Three"}
                                            };
```
### :dart:Accessing Dictionary Elements<br> 
```
IDictionary<int, string> dict = new Dictionary<int, string>()
                                            {
                                                {1,"One"},
                                                {2, "Two"},
                                                {3,"Three"}
                                            };

foreach (KeyValuePair<int, string> item in dict)
{
    Console.WriteLine("Key: {0}, Value: {1}", item.Key, item.Value);
}

for (int i = 0; i < dict.Count; i++)
{
    Console.WriteLine("Key: {0}, Value: {1}", 
                                            dict.ElementAt(i).Key, 
                                            dict.ElementAt(i).Value);
}

Console.WriteLine(dict[1]); //returns One
Console.WriteLine(dict[2]); // returns Two
dict.ContainsKey(1); // returns true
dict.ContainsKey(4); // returns false
```
#### Output<br> 
```
Key: 1, Value: One
Key: 2, Value: Two
Key: 3, Value: Three
```
### :dart:Check for an Existing Elements<br> 
```
dict.Remove(1); // removes the item which has 1 as a key
// removes nothing because value One1 is not matching
dict.Remove(new KeyValuePair<int, string>(2, "Two1")); 
dict.ContainsKey(1); // returns true
dict.ContainsKey(4); // returns false

dict.Contains(new KeyValuePair<int,string>(1,"One")); // returns true

string result;

if(dict.TryGetValue(4, out result))
{
    Console.WriteLine(result);
}
else
{
    Console.WriteLine("Could not find the specified key.");
}

//Prints Could not find the specified key.

```
#### A difference in style: IDictionary vs Dictionary
IDictionary is an interface and Dictionary is a class.

Dictionary implements IDictionary.

That means that this is possible to refer to Dictionary instance with/by IDictionary instance and invoke most of the Dictionary methods and properties through IDictionary instance.

This is very recommended to use interfaces as many as possible, because interfaces abstracts the modules and assemblies of the applications, allows polymorphism, which is both very common and useful in many situations and cases and allows replacing one module by another without touching the other modules.

Suppose that in the present, the programmer wrote:
```
IDictionary<string> dictionary = new Dictionary<string>();
```
And now dictionary invokes the methods and properties of Dictionary<string>.
### Sorting a Dictionary in place with respect to keys
<a href="https://www.dotnetperls.com/sort-dictionary">C# Sort Dictionary: Keys and Values</a>
```
class Person
{
    public Person(string firstname, string lastname)
    {
        FirstName = firstname;
        LastName = lastname;
    }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}

static void Main(string[] args)
{
    Dictionary<Person, int> People = new Dictionary<Person, int>();

    People.Add(new Person("John", "Doe"), 1);
    People.Add(new Person("Mary", "Poe"), 2);
    People.Add(new Person("Richard", "Roe"), 3);
    People.Add(new Person("Anne", "Roe"), 4);
    People.Add(new Person("Mark", "Moe"), 5);
    People.Add(new Person("Larry", "Loe"), 6);
    People.Add(new Person("Jane", "Doe"), 7);

    foreach (KeyValuePair<Person, int> person in People.OrderBy(i => i.Key.LastName))
    {
        Debug.WriteLine(person.Key.LastName + ", " + person.Key.FirstName + " - Id: " + person.Value.ToString());
    }
}
Output:

Doe, John - Id: 1
Doe, Jane - Id: 7
Loe, Larry - Id: 6
Moe, Mark - Id: 5
Poe, Mary - Id: 2
Roe, Richard - Id: 3
Roe, Anne - Id: 4
In this example it would make sense to also use ThenBy for first names:

foreach (KeyValuePair<Person, int> person in People.OrderBy(i => i.Key.LastName).ThenBy(i => i.Key.FirstName))
Then the output is:

Doe, Jane - Id: 7
Doe, John - Id: 1
Loe, Larry - Id: 6
Moe, Mark - Id: 5
Poe, Mary - Id: 2
Roe, Anne - Id: 4
Roe, Richard - Id: 3
LINQ also has the OrderByDescending and ThenByDescending for those that need it.
```
## SortedDictionary<TKey,TValue> Class<br>
Namespace:System.Collections.Generic<br>
Assembly:System.Collections.dll<br>
Represents a collection of key/value pairs that are sorted on the key.<br>

### :dart:Sample Program<br> 
```
using System;
using System.Collections.Generic;

public class Example
{
    public static void Main()
    {
        // Create a new sorted dictionary of strings, with string
        // keys.
        SortedDictionary<string, string> openWith =
            new SortedDictionary<string, string>();

        // Add some elements to the dictionary. There are no
        // duplicate keys, but some of the values are duplicates.
        openWith.Add("txt", "notepad.exe");
        openWith.Add("bmp", "paint.exe");
        openWith.Add("dib", "paint.exe");
        openWith.Add("rtf", "wordpad.exe");

        // The Add method throws an exception if the new key is
        // already in the dictionary.
        try
        {
            openWith.Add("txt", "winword.exe");
        }
        catch (ArgumentException)
        {
            Console.WriteLine("An element with Key = \"txt\" already exists.");
        }

        // The Item property is another name for the indexer, so you
        // can omit its name when accessing elements.
        Console.WriteLine("For key = \"rtf\", value = {0}.",
            openWith["rtf"]);

        // The indexer can be used to change the value associated
        // with a key.
        openWith["rtf"] = "winword.exe";
        Console.WriteLine("For key = \"rtf\", value = {0}.",
            openWith["rtf"]);

        // If a key does not exist, setting the indexer for that key
        // adds a new key/value pair.
        openWith["doc"] = "winword.exe";

        // The indexer throws an exception if the requested key is
        // not in the dictionary.
        try
        {
            Console.WriteLine("For key = \"tif\", value = {0}.",
                openWith["tif"]);
        }
        catch (KeyNotFoundException)
        {
            Console.WriteLine("Key = \"tif\" is not found.");
        }

        // When a program often has to try keys that turn out not to
        // be in the dictionary, TryGetValue can be a more efficient
        // way to retrieve values.
        string value = "";
        if (openWith.TryGetValue("tif", out value))
        {
            Console.WriteLine("For key = \"tif\", value = {0}.", value);
        }
        else
        {
            Console.WriteLine("Key = \"tif\" is not found.");
        }

        // ContainsKey can be used to test keys before inserting
        // them.
        if (!openWith.ContainsKey("ht"))
        {
            openWith.Add("ht", "hypertrm.exe");
            Console.WriteLine("Value added for key = \"ht\": {0}",
                openWith["ht"]);
        }

        // When you use foreach to enumerate dictionary elements,
        // the elements are retrieved as KeyValuePair objects.
        Console.WriteLine();
        foreach( KeyValuePair<string, string> kvp in openWith )
        {
            Console.WriteLine("Key = {0}, Value = {1}",
                kvp.Key, kvp.Value);
        }

        // To get the values alone, use the Values property.
        SortedDictionary<string, string>.ValueCollection valueColl =
            openWith.Values;

        // The elements of the ValueCollection are strongly typed
        // with the type that was specified for dictionary values.
        Console.WriteLine();
        foreach( string s in valueColl )
        {
            Console.WriteLine("Value = {0}", s);
        }

        // To get the keys alone, use the Keys property.
        SortedDictionary<string, string>.KeyCollection keyColl =
            openWith.Keys;

        // The elements of the KeyCollection are strongly typed
        // with the type that was specified for dictionary keys.
        Console.WriteLine();
        foreach( string s in keyColl )
        {
            Console.WriteLine("Key = {0}", s);
        }

        // Use the Remove method to remove a key/value pair.
        Console.WriteLine("\nRemove(\"doc\")");
        openWith.Remove("doc");

        if (!openWith.ContainsKey("doc"))
        {
            Console.WriteLine("Key \"doc\" is not found.");
        }
    }
}
```
Output:
```
An element with Key = "txt" already exists.
For key = "rtf", value = wordpad.exe.
For key = "rtf", value = winword.exe.
Key = "tif" is not found.
Key = "tif" is not found.
Value added for key = "ht": hypertrm.exe

Key = bmp, Value = paint.exe
Key = dib, Value = paint.exe
Key = doc, Value = winword.exe
Key = ht, Value = hypertrm.exe
Key = rtf, Value = winword.exe
Key = txt, Value = notepad.exe

Value = paint.exe
Value = paint.exe
Value = winword.exe
Value = hypertrm.exe
Value = winword.exe
Value = notepad.exe

Key = bmp
Key = dib
Key = doc
Key = ht
Key = rtf
Key = txt

Remove("doc")
Key "doc" is not found.
```
