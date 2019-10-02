#Java
## Install JDK on windows
* download from http://www.oracle.com/technetwork/java/javase/downloads/index.html
* Install jdk ewe. Notice, jdk and jre directory can be customized 
* configure enviornment

 **Set JAVA_HOME**
```
setx JAVA_HOME "C:\dev\Java\jdk-13"  # set jdk home
```

**PATH** 

```
   setx PATH "%PATH%;%JAVA_HOME%\bin"
```

**CLASSPATH**: make sure class path is included

```
    setx CLASSPATH ";%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin"
 ```
    

* Sample

 ```java
 public class hello{
    public static void main(String[] args) {
    System.out.println("Hello World!");
    }
}
 ```
 
Save it as *hello.java*
```
javac hello.java
java hello
```
