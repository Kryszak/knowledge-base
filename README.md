# Baza wiedzy pod rekrutacje

## Programming principles

### KISS - Keep It Simple, Stupid
It means you should be writing code as simple as possible. 
Don't get caught up in trying to be overly clever or showing off with a paragraph of advanced code.
If you can write a script in one line, write it in one line.

### DRY - Don't Repeat Yourself
When writing code, avoid duplication of data or logic. If you've ever copied and pasted code within your program, it's not DRY code.

### Composition Over Inheritance
If you write code using object-oriented programming you're going to find this useful. 
The composition over inheritance principle states: objects with complex behaviors should contain instances of objects with individual behaviors. 
They should not inherit a class and add new behaviors.
Composition programming is a lot cleaner to write, easier to maintain and allows flexibility defining behaviors. 
Each individual behavior is its own class. You can create complex behaviors by combining individual behaviors.

### Separation of Concerns
The separation of concerns principle is an abstract version of the single responsibility principle. 
This idea states that a program should be designed with different containers, and these containers should not have access to each other.
A well-known example of this is the model-view-controller (MVC) design. MVC separates a program into three distinct areas: the data (model), the logic (controller), and what the page displays (view). 
Variations of MVC are common in today's most popular web frameworks.
For example, the code that handles the database doesn't need to know how to render the data in the browser. 
The rendering code takes input from the user, but the logic code handles the processing. Each piece of code is completely independent.
The result is code that is easy to debug. If you ever need to rewrite the rendering code, you can do so without worrying about how the data gets saved or the logic gets processed.

### YAGNI - You Aren't Going to Need It
This principle means you should never code for functionality on the chance that you may need in the future. 
Don't try and solve a problem that doesn't exist.
In an effort to write DRY code, programmers can violate this principle. Often inexperienced programmers try to write the most abstract and generic code they can. 
Too much abstraction causes bloated code that is impossible to maintain.
Only apply the DRY principle only when you need to. If you notice chunks of code written over and over, then abstract them.
Don't think too far out at the expense of your current code batch.

### SOLID
#### The Single Responsibility Principle
The Single Responsibility Principle states that a class should do one thing and therefore it should have only a single reason to change.

#### Open-Closed Principle
The Open-Closed Principle requires that classes should be open for extension and closed to modification

#### Liskov Substitution Principle
The Liskov Substitution Principle states that subclasses should be substitutable for their base classes.
This means that, given that class B is a subclass of class A, we should be able to pass an object of class B to any method that expects an object of class A and the method should not give any weird output in that case.

#### Interface Segregation Principle
Segregation means keeping things separated, and the Interface Segregation Principle is about separating the interfaces.
The principle states that many client-specific interfaces are better than one general-purpose interface. Clients should not be forced to implement a function they do no need.

#### Dependency Inversion Principle
The Dependency Inversion principle states that our classes should depend upon interfaces or abstract classes instead of concrete classes and functions.

## Recruitment

### JEE transactions
http://www.javaexpress.pl/article/show/Transakcje_w_systemach_Java_Enterprise_Wprowadzenie

### JEE vs Spring vs Spring Boot
https://www.quora.com/What-are-the-differences-between-Java-EE-and-Spring
https://www.quora.com/What-is-the-difference-between-Spring-Boot-and-the-Spring-framework

### DB isolation levels
https://en.wikipedia.org/wiki/Isolation_(database_systems)

### CI/CD
CI: https://en.wikipedia.org/wiki/Continuous_integration
CD: https://en.wikipedia.org/wiki/Continuous_delivery

### JPA
https://en.wikipedia.org/wiki/Java_Persistence_API

### Kafka vs JMS
http://cloudurable.com/blog/kafka-vs-jms/index.html

### ACID
https://en.wikipedia.org/wiki/ACID_(computer_science)

### BASE
https://www.lifewire.com/abandoning-acid-in-favor-of-base-1019674

### PostgreSQL - block removing row with relation
https://stackoverflow.com/questions/17976689/do-i-need-to-specify-on-delete-no-action-on-my-foreign-key

### Fat jar, war
fat jar - jar with all dependency
war - contains web app

### Checked vs unchecked exceptions
https://www.geeksforgeeks.org/checked-vs-unchecked-exceptions-in-java/

### Inner vs Outer JOIN SQL
https://www.diffen.com/difference/Inner_Join_vs_Outer_Join

### Design patterns
https://sourcemaking.com/design_patterns

### Java 7 vs 8 vs 9/10
https://howtodoinjava.com/java-version-wise-features-history/
https://softwareengineering.stackexchange.com/questions/193630/summary-of-differences-between-java-versions

### ForkJoinPool
https://www.baeldung.com/java-fork-join

### Conditional CDI
https://stackoverflow.com/questions/19225115/how-to-do-conditional-auto-wiring-in-spring

### Spring Profile vs Maven profile
https://dzone.com/articles/spring-profiles-or-maven

### Java Garbage Collector
https://www.baeldung.com/jvm-garbage-collectors

### JVM memory types
https://dzone.com/articles/java-memory-management

### Java - pass by reference of value
Java is always pass by value
https://www.javaworld.com/article/2077424/learn-java/learn-java-does-java-pass-by-reference-or-pass-by-value.html

### ArrayList implementation, LinkedList
https://beginnersbook.com/2013/12/difference-between-arraylist-and-linkedlist-in-java/

### HashMap implementation
https://www.geeksforgeeks.org/internal-working-of-hashmap-java/

### Queues
http://tutorials.jenkov.com/java-collections/queue.html

### Java reference types
https://dzone.com/articles/java-different-types-of-references

### Spring data fetch collection (lazy)
https://stackoverflow.com/questions/34833350/spring-data-jpa-lazy-fetching-with-collections

### Java in docker
https://developers.redhat.com/blog/2017/03/14/java-inside-docker/

### CDI - constructor vs setter vs field injection
https://www.baeldung.com/inversion-control-and-dependency-injection-in-spring

### Type erasure
https://www.baeldung.com/java-type-erasure

### Last element from Java stream
https://www.baeldung.com/java-stream-last-element

### String concatenation
https://stackoverflow.com/a/7817989


## Java gimmics
```
(int) (Integer) null
///NullPointerException
```

```
class Scratch {
    public static void main(String[] args) {
        Integer first = 100;
        Integer second = 100;

        System.out.println("First == second " + (first == second)); // true

        Integer third = 5000;
        Integer fourth = 5000;

        System.out.println("First == second " + (third == fourth)); // false
    }
}
```
