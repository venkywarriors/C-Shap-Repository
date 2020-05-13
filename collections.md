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
