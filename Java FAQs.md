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

### **What is singleton class in Java and how can we make a class singleton?**

Singleton class is a class whose only one instance can be created at any given time, in one JVM. A class can be made singleton by making its constructor private.


### **Write Once and Run Anywhere**
Java's bytecode allows it to have a write once and run anywhere nature. Java compiler converts the Java programs into class file (Bytecode) which is the intermediate language between source code and machine code.

### **### Is Empty .java file name a valid source file name?**

Yes, Java allows to save our java file by **.java** only, we need to compile it by **javac .java** and run by **java classname** Let's take a simple example:
1.  //save by .java only  
2.  class A{  
3.  public static void main(String args[]){  
4.  System.out.println("Hello java");  
5.  }  
6.  }  
7.  //compile by javac .java  
8.  //run by     java A  

compile it by **javac .java**

run it by **java A**
