#Java
## Install JDK on windows
* download from http://www.oracle.com/technetwork/java/javase/downloads/index.html
* Install jdk ewe. Notice, jdk and jre directory can be customized 
* configure enviornment
  * JAVE_HOME: JDK HOME
  * PATH 
  ```
   setx PATH "%PATH%;%JAVA_HOME%\bin"
  ```
  * CLASSPATH: make sure class path is included
    * TODO
    
    public class hello{
    public static void main(String[] args) {
    System.out.println("Hello World!");
    }
* Sample
 ```java
 public class hello{
    public static void main(String[] args) {
    System.out.println("Hello World!");
    }
}
 ```
