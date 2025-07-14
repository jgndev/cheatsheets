---
id: 13
date: 2025-07-14T00:00:00Z
title: Java Cheatsheet
author: Jeremy Novak
summary: Java programming language cheatsheet
slug: java-cheatsheet
tags:
  - java
published: true
---

# Java Cheatsheet

---

## Setup & Environment

- Install Java (macOS)
```bash
brew install openjdk
```

- Install Java (Linux)
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install default-jdk

# CentOS/RHEL
sudo yum install java-11-openjdk-devel
```

- Install Java (Windows)
1. Download JDK from [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html) or [OpenJDK](https://openjdk.org/)
2. Run the installer and follow the prompts
3. Set JAVA_HOME environment variable

- Check Java version
```bash
java -version
javac -version
```

- Set up Java environment variables (add to ~/.bashrc or ~/.zshrc)
```bash
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk
export PATH=$PATH:$JAVA_HOME/bin
```

---

## Building & Running

- Compile a Java file
```bash
javac HelloWorld.java
```

- Run a Java program
```bash
java HelloWorld
```

- Compile and run with classpath
```bash
javac -cp "lib/*" MyApp.java
java -cp ".:lib/*" MyApp
```

- Create a JAR file
```bash
jar cvf myapp.jar *.class
```

- Run a JAR file
```bash
java -jar myapp.jar
```

---

## Maven

- Create a new Maven project
```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=myapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

- Compile project
```bash
mvn compile
```

- Run tests
```bash
mvn test
```

- Package project
```bash
mvn package
```

- Clean project
```bash
mvn clean
```

- Install to local repository
```bash
mvn install
```

---

## Gradle

- Create a new Gradle project
```bash
gradle init --type java-application
```

- Build project
```bash
./gradlew build
```

- Run tests
```bash
./gradlew test
```

- Run application
```bash
./gradlew run
```

- Clean project
```bash
./gradlew clean
```

---

## Basic Java Structure

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

---

## Variables and Data Types

- Primitive types
```java
int number = 42;
double decimal = 3.14;
boolean flag = true;
char letter = 'A';
byte smallNumber = 127;
short mediumNumber = 32767;
long largeNumber = 123456789L;
float floatNumber = 2.5f;
```

- Strings
```java
String text = "Hello";
String name = new String("World");
```

- Arrays
```java
int[] numbers = {1, 2, 3, 4, 5};
String[] names = new String[3];
names[0] = "Alice";
```

- Constants
```java
final int MAX_SIZE = 100;
static final String CONSTANT = "VALUE";
```

---

## Control Flow

- If/else statement
```java
if (x > 0) {
    System.out.println("Positive");
} else if (x < 0) {
    System.out.println("Negative");
} else {
    System.out.println("Zero");
}
```

- Switch statement
```java
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    default:
        System.out.println("Other day");
}
```

- For loop
```java
for (int i = 0; i < 10; i++) {
    System.out.println(i);
}
```

- Enhanced for loop
```java
int[] array = {1, 2, 3, 4, 5};
for (int num : array) {
    System.out.println(num);
}
```

- While loop
```java
int i = 0;
while (i < 10) {
    System.out.println(i);
    i++;
}
```

- Do-while loop
```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 10);
```

---

## Classes and Objects

- Define a class
```java
public class Person {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public int getAge() {
        return age;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
}
```

- Create and use objects
```java
Person person = new Person("Alice", 30);
System.out.println(person.getName());
person.setAge(31);
```

---

## Inheritance

- Extend a class
```java
public class Student extends Person {
    private String studentId;
    
    public Student(String name, int age, String studentId) {
        super(name, age);
        this.studentId = studentId;
    }
    
    public String getStudentId() {
        return studentId;
    }
}
```

- Override methods
```java
@Override
public String toString() {
    return "Student{" +
           "name='" + getName() + '\'' +
           ", age=" + getAge() +
           ", studentId='" + studentId + '\'' +
           '}';
}
```

---

## Interfaces

- Define an interface
```java
public interface Drawable {
    void draw();
    default void print() {
        System.out.println("Printing...");
    }
}
```

- Implement an interface
```java
public class Circle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}
```

---

## Exception Handling

- Try-catch block
```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    System.out.println("This always executes");
}
```

- Throw an exception
```java
public void checkAge(int age) throws IllegalArgumentException {
    if (age < 0) {
        throw new IllegalArgumentException("Age cannot be negative");
    }
}
```

---

## Collections

- ArrayList
```java
import java.util.ArrayList;
import java.util.List;

List<String> names = new ArrayList<>();
names.add("Alice");
names.add("Bob");
names.remove("Alice");
```

- HashMap
```java
import java.util.HashMap;
import java.util.Map;

Map<String, Integer> ages = new HashMap<>();
ages.put("Alice", 30);
ages.put("Bob", 25);
int aliceAge = ages.get("Alice");
```

- HashSet
```java
import java.util.HashSet;
import java.util.Set;

Set<String> uniqueNames = new HashSet<>();
uniqueNames.add("Alice");
uniqueNames.add("Bob");
uniqueNames.add("Alice"); // Duplicate, won't be added
```

---

## File I/O

- Read file
```java
import java.io.*;
import java.util.Scanner;

try (Scanner scanner = new Scanner(new File("file.txt"))) {
    while (scanner.hasNextLine()) {
        String line = scanner.nextLine();
        System.out.println(line);
    }
} catch (FileNotFoundException e) {
    System.out.println("File not found: " + e.getMessage());
}
```

- Write file
```java
import java.io.*;

try (PrintWriter writer = new PrintWriter("output.txt")) {
    writer.println("Hello, World!");
    writer.println("Writing to file");
} catch (FileNotFoundException e) {
    System.out.println("Error writing file: " + e.getMessage());
}
```

---

## Useful Methods

- String methods
```java
String text = "Hello World";
int length = text.length();
String upper = text.toUpperCase();
String lower = text.toLowerCase();
boolean contains = text.contains("World");
String[] parts = text.split(" ");
String trimmed = text.trim();
```

- Math methods
```java
int max = Math.max(10, 20);
int min = Math.min(10, 20);
double sqrt = Math.sqrt(16);
double random = Math.random(); // 0.0 to 1.0
int randomInt = (int) (Math.random() * 100); // 0 to 99
```

- Array methods
```java
import java.util.Arrays;

int[] numbers = {3, 1, 4, 1, 5};
Arrays.sort(numbers);
String arrayString = Arrays.toString(numbers);
```

---

## Common Patterns

- Singleton pattern
```java
public class Singleton {
    private static Singleton instance;
    
    private Singleton() {}
    
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

- Builder pattern
```java
public class User {
    private String name;
    private int age;
    private String email;
    
    private User(Builder builder) {
        this.name = builder.name;
        this.age = builder.age;
        this.email = builder.email;
    }
    
    public static class Builder {
        private String name;
        private int age;
        private String email;
        
        public Builder setName(String name) {
            this.name = name;
            return this;
        }
        
        public Builder setAge(int age) {
            this.age = age;
            return this;
        }
        
        public Builder setEmail(String email) {
            this.email = email;
            return this;
        }
        
        public User build() {
            return new User(this);
        }
    }
}

// Usage
User user = new User.Builder()
    .setName("Alice")
    .setAge(30)
    .setEmail("alice@example.com")
    .build();
```

---

## Useful Packages

- "java.util" — Collections, utilities
- "java.io" — Input/output
- "java.nio" — New I/O API
- "java.lang" — Core language features
- "java.time" — Date and time API
- "java.util.stream" — Stream API
- "java.util.concurrent" — Concurrency utilities

---

## Resources

- [Oracle Java Documentation](https://docs.oracle.com/en/java/)
- [Java Tutorials](https://docs.oracle.com/javase/tutorial/)
- [OpenJDK](https://openjdk.org/)
- [Maven Documentation](https://maven.apache.org/guides/)
- [Gradle Documentation](https://docs.gradle.org/)
