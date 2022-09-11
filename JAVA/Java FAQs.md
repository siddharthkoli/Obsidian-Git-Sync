### **JVM, JRE and JDK**
JVM, JRE, and JDK are platform dependent because the configuration of each [OS](https://www.javatpoint.com/os-tutorial) is different from each other. However, Java is platform independent.

**JVM - Java Virtual Machine**

JVM (Java Virtual Machine) is an abstract machine. It is called a virtual machine because it doesn't physically exist. It is a specification that provides a runtime environment in which Java bytecode can be executed. It can also run those programs which are written in other languages and compiled to Java bytecode.
The JVM performs the following main tasks:

-   Loads code
-   Verifies code
-   Executes code
-   Provides runtime environment

**JRE - Java Runtime Environment**

The Java Runtime Environment is a set of software tools which are used for developing Java applications. It is used to provide the runtime environment. It is the implementation of JVM. It physically exists. It contains a set of libraries + other files that JVM uses at runtime.

**JDK**

It is an acronym for Java Development Kit. The Java Development Kit (JDK) is a software development environment which is used to develop Java applications and applets. It physically exists. It contains JRE + development tools.

JDK is an implementation of any one of the below given Java Platforms released by Oracle Corporation:

-   Standard Edition Java Platform
-   Enterprise Edition Java Platform
-   Micro Edition Java Platform

The JDK contains a private Java Virtual Machine (JVM) and a few other resources such as an interpreter/loader (java), a compiler (javac), an archiver (jar), a documentation generator (Javadoc), etc. to complete the development of a Java Application


### **Explain public static void main(String args[]) in Java.**

main() in Java is the entry point for any Java program. It is always written as **public static void main(String[] args)**.

-   **public**: Public is an access modifier, which is used to specify who can access this method. Public means that this Method will be accessible by any Class.
-   **static**: It is a keyword in java which identifies it is class-based. main() is made static in Java so that it can be accessed without creating the instance of a Class. In case, main is not made static then the compiler will throw an error as **main**() is called by the JVM before any objects are made and only static methods can be directly invoked via the class. 
-   **void**: It is the return type of the method. Void defines the method which will not return any value.
-   **main**: It is the name of the method which is searched by JVM as a starting point for an application with a particular signature only. It is the method where the main execution occurs.
-   **String args[]**: It is the parameter passed to the main method.

### **Why Java is platform independent?**

Java is called platform independent because of its byte codes which can run on any system irrespective of its underlying operating system.

### **What are wrapper classes in Java?**

Wrapper classes convert the Java primitives into the reference types (objects). Every primitive data type has a class dedicated to it. These are known as wrapper classes because they “wrap” the primitive data type into an object of that class.

### **Constructors and Types**
Block to initialise objects, same name as that of class and no return types.

Default Constructor - non parameterized constructor. It will be created when no other constructor is created by the user. Its main purpose is to initialize the variables with default values. Its main purpose is to create objects

Parameterized Constructor - the constructor which is capable of initializing the instance variables with the provided values.

Constructor chaining - Calling of one constructor from another with respect to current class

### **What is singleton class in Java and how can we make a class singleton?**

Singleton class is a class whose only one instance can be created at any given time, in one JVM. A class can be made singleton by making its constructor private.


### **Write Once and Run Anywhere**
Java's bytecode allows it to have a write once and run anywhere nature. Java compiler converts the Java programs into class file (Bytecode) which is the intermediate language between source code and machine code.

## Is Empty .java file name a valid source file name?

Yes, Java allows to save our java file by **.java** only, we need to compile it by **javac .java** and run by **java classname** Let's take a simple example:
  ```java
//save by .java only  
  class A{  
	  public static void main(String args[]){  
		  System.out.println("Hello java");  
	  }  
  }  
  //compile by javac .java  
  //run by     java A  
```

compile it by **javac .java**

run it by **java A**

### Access Modifiers

In Java, access specifiers are the keywords which are used to define the access scope of the method, class, or a variable. In Java, there are four access specifiers given below.

-   **Public** The classes, methods, or variables which are defined as public, can be accessed by any class or method.
-   **Protected** Protected members of a class are visible within the package. Therefore, we can only access within the package but can be accessed to the subclasses outside the package through the inheritance only
-   **Default** Default are accessible within the package only. By default, all the classes, methods, and variables are of default scope.
-   **Private** The private class, methods, or variables defined as private can be accessed within the class only.
![[Pasted image 20220911180053.png]]

### Non Access Modifiers
- Static :
--Static Blocks - They are called when the class is first loaded into the memory and it is called before main is called. This code is executed only once. And it is called automatically.
Static blocks can be executed without the main(). 

-- Static Variables - When a variable is declared as static, then a single copy of the variable is created and shared among all objects at the class level. Static variables are, essentially, global variables. All instances of the class share the same static variable.
Static block and static variables are executed in the order they are present in a program.

-- Static methods
When a method is declared with the _static_ keyword, it is known as the static method. The most common example of a static method is the _main( )_ method. As discussed above, Any static member can be accessed before any objects of its class are created, and without reference to any object. Methods declared as static have several restrictions: 

-   They can only directly call other static methods.
-   They can only directly access static data.
-   They cannot refer to [this](https://www.geeksforgeeks.org/this-reference-in-java/) or [super](https://www.geeksforgeeks.org/super-keyword/) in any way.

**Use Static variables for properties which are common across all objects. Use static methods to access static variables.

--Static Class : A class can be made static only if it is under some other class i.e. a nested class. Top level classes cannot be made static.
Static class cannot access non static members of a outer non static class.

- Final Keyword
Used to restrict the user. If used with a class, cannot inherit the class. If used with a method, cannot override. If used with a variable, its value cannot be changed i.e. constant.

- Abstract : Abstract is a keyword that is used with a class or a method. An abstract class or abstract method is used for further modification. If a class is declared as ‘abstract’, the class cannot be instantiated.

- Synchronized : It is used to achieve thread safeness. Only one thread can enter in a synchronized method or block at a given time.

### Super 
it is a reference variable that refers to the immediate parent class object.
When you instantiate a sub-class, the parent class constructor is automatically invoked.
The uses of the Java super Keyword are- 

1.  To refer to an immediate parent class instance variable, use super.
2.  The keyword super can be used to call the method of an immediate parent class.
3.  Super() can be used to call the constructor of the immediate parent class.

### String vs StringBuilder vs StringBuffer
String - Immutable, less efficient, constant string pool, provides thread safety
StringBuilder - Mutable, efficient, heap, no thread safety
StringBuffer - Mutable, less efficient, heap, provides thread safety

String Pool - Java String pool refers to a collection of Strings which are stored in heap memory. In this, whenever a new object is created, String pool first checks whether the object is already present in the pool or not. If it is present, then the same reference is returned to the variable else new object will be created in the String pool and the respective reference will be returned.
![[Pasted image 20220911181415.png]]

## Dynamic Method Dispatch
Call to an overridden method is resolved at run time rather than compile time. In this, a overridden method is called thorugh the reference variable of super class.

``` java
class Car{
void run()
{
 System.out.println(" in car class");
}
}
Class Audi extends Car
{
 void run()
 {
	 System.out.println("Audi");
 }
}

Class Test{
 Car c = new Audi();
 c.run();
}
```

### Java Collections:
https://www.javatpoint.com/java-collections-interview-questions
Go through below for theory:

https://www.javatpoint.com/collections-in-java