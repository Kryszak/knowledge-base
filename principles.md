# Programming principles

## KISS - Keep It Simple, Stupid
It means you should be writing code as simple as possible. 
Don't get caught up in trying to be overly clever or showing off with a paragraph of advanced code.
If you can write a script in one line, write it in one line.

## DRY - Don't Repeat Yourself
When writing code, avoid duplication of data or logic. If you've ever copied and pasted code within your program, it's not DRY code.

## Composition Over Inheritance
If you write code using object-oriented programming you're going to find this useful. 
The composition over inheritance principle states: objects with complex behaviors should contain instances of objects with individual behaviors. 
They should not inherit a class and add new behaviors.
Composition programming is a lot cleaner to write, easier to maintain and allows flexibility defining behaviors. 
Each individual behavior is its own class. You can create complex behaviors by combining individual behaviors.

## Separation of Concerns
The separation of concerns principle is an abstract version of the single responsibility principle. 
This idea states that a program should be designed with different containers, and these containers should not have access to each other.
A well-known example of this is the model-view-controller (MVC) design. MVC separates a program into three distinct areas: the data (model), the logic (controller), and what the page displays (view). 
Variations of MVC are common in today's most popular web frameworks.
For example, the code that handles the database doesn't need to know how to render the data in the browser. 
The rendering code takes input from the user, but the logic code handles the processing. Each piece of code is completely independent.
The result is code that is easy to debug. If you ever need to rewrite the rendering code, you can do so without worrying about how the data gets saved or the logic gets processed.

## YAGNI - You Aren't Going to Need It
This principle means you should never code for functionality on the chance that you may need in the future. 
Don't try and solve a problem that doesn't exist.
In an effort to write DRY code, programmers can violate this principle. Often inexperienced programmers try to write the most abstract and generic code they can. 
Too much abstraction causes bloated code that is impossible to maintain.
Only apply the DRY principle only when you need to. If you notice chunks of code written over and over, then abstract them.
Don't think too far out at the expense of your current code batch.

## SOLID
### The Single Responsibility Principle
The Single Responsibility Principle states that a class should do one thing and therefore it should have only a single reason to change.

### Open-Closed Principle
The Open-Closed Principle requires that classes should be open for extension and closed to modification

### Liskov Substitution Principle
The Liskov Substitution Principle states that subclasses should be substitutable for their base classes.
This means that, given that class B is a subclass of class A, we should be able to pass an object of class B to any method that expects an object of class A and the method should not give any weird output in that case.

### Interface Segregation Principle
Segregation means keeping things separated, and the Interface Segregation Principle is about separating the interfaces.
The principle states that many client-specific interfaces are better than one general-purpose interface. Clients should not be forced to implement a function they do no need.

### Dependency Inversion Principle
The Dependency Inversion principle states that our classes should depend upon interfaces or abstract classes instead of concrete classes and functions.
