### :dart:Record your Test Execution in Selenium : <br> 
Monte Screen Recorder, a Java library that can assist you in creating videos of your Selenium tests. Add Screen Recorder
Maven Dependencies

How to Implement in our project :

We have one Java File of Recording screen functionality written and have attached as java file name as 'MyScreenRecorder.java' file

This <a href="https://github.com/venkywarriors619/Generic-functions-Selenium-java/blob/master/MyScreenRecorder.java">'MyScreenRecorder.java'</a> file is the base function and we can use the method as 'MyScreenRecorder.startRecording("yourtestcase_recording")' in our own test case file.

For Example : Your Java file has the navigation function and if you want to record some scenarios, then we can use the method as 'MyscreenRecorder.startRecording' to start record and 'MyScreenRecorder.stopRecording' to stop the record.
Reference Link: http://www.randelshofer.ch/monte/
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
