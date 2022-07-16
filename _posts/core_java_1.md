<b>Title:</b> Core Java - Part 1
<b>Author:</b> Anurag Sharma

<b>Track Category:</b> Development
<b>Subcategory:</b> Programming
<b>Tags:</b> Java, Language, Tools and Libraries

<b>Read Time:</b>  10 min

[Banner Image](https://www.dropbox.com/s/622zq50qi1h6rcl/markus-spiske-qjnAnF0jIGk-unsplash.jpg?dl=0)

# Content

Welcome to the first part of Core Java tutorials. In this series, we'll discuss the basics of Core Java with practical examples. So let's get started.

Java is an Object-Oriented Programming Language(OOPS). Sun Microsystems developed it in 1995, which was later acquired by Oracle. It is secure and platform-independent, which means its compiled programs can be run on any operating system. We can run our Java programs on a wide variety of computers using a range of OS(macOS, Windows, Linux, etc.). This is possible because our Java program doesn't execute directly on our computers. It runs on a standardized hypothetical computer known as Java Virtual Machine(JVM). This JVM is implemented in our computer by a program called Java interpreter. Don't get confused by the terminology. We will discuss everything in detail. Let's start with these terms.

1. Java Virtual Machine(JVM) - It provides a runtime environment in which Java byte code can be executed.
2. Java Compiler - It compiles the .java file into bytecode. Bytecodes are binary instructions for Java interpreter.
3. Java Interpreter - It reads the bytecode and converts it into machine code.

*NOTE* - Java is platform-independent, but JVM is not. According to the OS, you need to install it into your machine.

### Compiling a Java Program - 

The below command is used to compile a java program -

`javac test.java`

`javac` is the compiler that compiles our program and creates a file with the extension `.class` The class file contains bytecodes that are binary instructions for Java interpreter.

### To run application program - 

Below command is used to run a java program - 

`java test`

- A Java program is a collection of one or more classes. There is at least one class in every program. 
- A Java program file must be saved with the `.java` extension. 
- We must save the program file with the same name as that of the class defined within it.
- We must put the code for each public class in a separate file.(There can be only one public class in a file)

We will discuss what a class is and what is public in this series's later parts.

### Variables

A variable is known as a named value holder in primary memory. When a variable is declared, the compiler is able to check that it is not being used in a manner or context that is inappropriate to its type(Type checking).

example - `int x = 10;` Here x is a variable of integer type. We'll discuss different data types later.

### Variables Names 

The name we choose for a variable is called an identifier, and an identifier can be of any length, although it must begin with an alphabet and uppercase. The rest of the identifier can include digits also. Operators and spaces are not allowed in identifiers. Java variables are case sensitive, which means `name` and `NAME` are two different identifiers.

We can't use Java keywords as a name for something. Keywords are an essential part of the language and are meant for specific purposes.

Below are some examples of valid identifiers - 

```
max, Max, MAX
ab$123
$ab_123
_abcd
```
Below are some examples of invalid identifiers - 

```
ab+cd
ab-cd
ab@cd
ab cd
123abcd
while
final
```

The last two `while and final` are reserved keywords.

In general, we follow camel case notation for variables, class, or method names in Java. Below is the example - 

HelloWorld, calculateTotal, findMyAge().

That's all for now for this part. We'll continue in the next part with DataTypes, Type conversion, and more. Till then, happy coding :)