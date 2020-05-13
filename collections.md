## System.Collections
### :dart:IDictionary<TKey,TValue> Interface <br> 
Assembly: Mscorlib.dll <br> 
Namespace: System.Collections <br> 
Summary: Represents a collection of key-and-value pairs. <br> 

The IDictionary class is the base interface for collections of key-and-value pairs.
Each element is a key-and-value pair stored in a DictionaryEntry object.

Each association must have a unique key that is not null, but the value of an association can be any object reference, including a null reference. The IDictionary interface allows the contained keys and values to be enumerated, but it does not imply any particular sort order.
```
@Test
public void navigation() throws Exception{

  MyScreenRecorder.startRecording("Navigation_recording");
  
  /*
                       your code goes here
                */
               MyScreenRecorder.stopRecording();

}
```
#### A difference in style: IDictionary vs Dictionary
IDictionary is an interface and Dictionary is a class.

Dictionary implements IDictionary.

That means that this is possible to refer to Dictionary instance with/by IDictionary instance and invoke most of the Dictionary methods and properties through IDictionary instance.

This is very recommended to use interfaces as many as possible, because interfaces abstracts the modules and assemblies of the applications, allows polymorphism, which is both very common and useful in many situations and cases and allows replacing one module by another without touching the other modules.

Suppose that in the present, the programmer wrote:

IDictionary<string> dictionary = new Dictionary<string>();

And now dictionary invokes the methods and properties of Dictionary<string>.
