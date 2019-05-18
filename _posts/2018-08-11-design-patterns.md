---
title: "Design Patterns"
excerpt: "Design Patterns test..."
permalink: /posts/patterns/
layout: single
toc: true
author_profile: true
read_time: true
comments: true
share: true
related: true
search: true
categories: 
  - Patterns
last_modified_at: 2018-09-11T08:06:00-05:00
---

# Design Patterns

## About Design Patterns

Design Patterns are optimized, reusable solutions to the programming problems that we encounter every day. 
A design pattern is a description, or template, for how to solve a problem that can be used in many different situations. It's not language-specific. A good design pattern should be implementable in most if not all languages, depending on the capabilities of the language.

There are three basic kinds of design patterns:
Creational
Abstract Factory, Builder, Factory Method, Object Pool, Prototype, Singleton. 

Structural
Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy.

Behavioral
Chain of responsibility, Command, Interpreter, Iterator, Mediator, Memento, Observer, State, Strategy, Template method, Visitor.

Generally, the three groups above define how your program elements relate to each other, how they get created, and how they communicate with each other.

Why use them?
Design patterns are well-thought out solutions to programming problems. Let's draw a parallel with a real-world example.
Suppose you are standing at the base of a mountain and have been given the task of reaching its top by the end of the day. Assuming that you are unaware of the available routes to the mountain top, what will you do? Of course, you will start to climb up as per your own understanding. Your lack of knowledge about the right route makes it extremely difficult for you to decide the best possible route.
If somebody gives you a detailed map along with all possible routes, including the pros and cons of each, then you will be in a much better position to begin your journey and choose the right route.

> Simply put a design pattern is a proven solution to solve design problems

---

## Singleton Design Pattern

Singleton is a creational design pattern, which ensures that only one instance of a class is created.

Singleton may be used when: 
- you need access to a shared resource.
- access to a shared resource will be requested from multiple, separate parts of your program.
- only one object can be instantiated.

A good example is a Logger, which is used in every part of the system to log some information. For example, in a social network, every activity of a user should be logged (login, logout, comment, posts, likes).
Instead of instantiating a new Logger instance over and over again for each activity type, it would be better to have a single instance and access it when needed. In other words, it is better to use the same Logger instance to log user logins, logouts, comments, posts, and likes, when necessary.


> Singletons are intended to be used when a class must have exactly one instance, no more, no less.

---

## Factory Method Design Pattern
   
   Factory Method is a creational pattern that defines an interface for creating an object, but lets subclasses decide which class to instantiate. 
   
   The best time to use the factory method pattern is when you have multiple variations of a single entity. For example, let's consider a program that creates different shapes. For this program, we need to define a ShapeFactory that will act as a common interface for creating shapes. Using this interface, each subclass will create the specific shape by implementing the ShapeFactory's corresponding "create" method. 
   
   To better understand the Factory Method concept, consider a real-world employment agency. The agency helps clients fill positions for their company. The client provides the hiring criteria and then leaves the details of assessing candidates to the agency. The hiring agency takes care of a potential candidate’s eligibility, skill, and experience verification to ensure that the candidate matches the hiring criteria. In this case, the hiring agency acts as the factory. It allows the client to create new objects without having to know the details of how they're created.


> We create objects without exposing the creation logic to the client and refer to newly created objects using a common interface (employment agency).

The factory method pattern relies on inheritance, as object creation is delegated to subclasses that implement the factory method to create objects.

The Factory Method is usually used when creating frameworks, which standardize the architectural model for a range of applications, but allow for individual applications to define their own objects and their instantiation.


> A Factory is a creator of objects that have a common interface.

---

## Abstract Factory Design Pattern
    
   The Abstract Factory is a creational pattern, similar to the Factory Method pattern, with the key difference being that the Abstract Factory provides an interface for creating families of related or dependent objects without specifying their concrete classes.
   
   Often, designs start out using Factory Method and evolve toward Abstract Factory as more flexibility is needed.
   
   Imagine an application needs to run on different operating systems. In order to achieve this, we need to encapsulate the dependencies of our application. One approach is to have a "factory" object that has the responsibility of providing creation services for the entire platform family. Each time we need a new object for our application, we use the factory.
   This makes a class independent of how its objects are created (which concrete classes are instantiated).
   
   Consider a "factory" to create UI elements. The same factory can create buttons, textboxes, windows, and other elements for two operating systems - Windows and MacOS.
   When we want to create a new button, we do not instantiate a new button class for a particular operating system. Instead, we request the factory create a button, and the factory does so, considering the parameters of the operating system. The same applies for any other UI object. As a result, we get the object we need without getting into detail of how the objects are created.
   
   Basically, the Abstract Factory pattern provides a way to encapsulate a group of individual factories that have a common theme without specifying their concrete classes.


> Because the service provided by the factory object is so pervasive, it is routinely implemented as a Singleton.

---

## Builder Design Pattern
   
   The Builder design pattern is a creational pattern that separates the construction of a complex object from its representation. By doing so, the same construction process can create different representations.
   Simply said, it builds a complex object using simple objects and a step-by-step approach.
   
   For example, let's say we need to build cars. Each car has many options. The combination of options would lead to a huge list of constructors for the Car class. To avoid this, we will create a builder class, CarBuilder. We will send each option step by step to the CarBuilder and then construct the final car with the correct options.
   This approach makes it flexible to add and remove options from the car.


> Sometimes creational patterns are complementary: Builder can use one of the other patterns to implement which components are built.

---

## Object Pool Pattern
   
   The Object Pool design pattern is useful when it is necessary to work with a large number of objects that are particularly expensive to instantiate, especially if each object is only needed for a short period of time. 
   
   Instead of creating and destroying the expensive objects, the object pool pattern suggests reusing the already created objects.
   
   When a new object is needed, it is requested from the pool. If a previously prepared object is available it is returned immediately, avoiding the instantiation cost. If no objects are present in the pool, a new item is created and returned. When the object has been used and is no longer needed, it is returned to the pool, allowing it to be used again in the future without repeating the expensive instantiation process.
   
   For example, the Object Pool design pattern is used in the .NET Framework Data Provider for SQL Server. As SQL Server database connections can be slow to create, a pool of connections is maintained. When you close a connection, the connection is held in a pool from which it can be retrieved when requesting a new connection. This substantially increases the speed of making connections.


> Object Pools are usually implemented as Singletons.

---

## Prototype Design Pattern
   
   The Prototype design pattern is a creational pattern that uses a prototype to create new objects by copying this prototype. In other words, instead of creating new objects, we clone them from the prototype.
   
   The pattern is used when object creation is resource expensive. By cloning new objects, we avoid the inherent cost of creating a new object in the standard way.
   
   Mitotic cell division, which results in two identical cells, is an example of the Prototype pattern. When a cell splits, two cells of identical genotype result. In other words, the cell clones itself.


> Prototype is unique among the other creational patterns as it doesn't require a class - only an object.

---

## Adapter Design Pattern 
   
   The Adapter pattern is a structural design pattern that allows the interface of an existing class to be used as another interface. It is often used to make existing classes work with others without modifying their source code. 
   
   For example, let's consider you have an old class that implements some functionality needed in your new project. However, the way it is written is not compatible with the philosophy and architecture of the system currently being developed. In order to use the old class without rewriting the whole functionality from scratch, we can create an adapter, also called a wrapper, that translates, or maps, the old component to the new system.
   Your program will then call the wrapper, which will redirect to the corresponding methods in the old class.

> The key idea in this pattern is to work through a separate Adapter that adapts the interface of an already existing class without changing it.

---

## Bridge Design Pattern
   
   The Bridge pattern is designed to separate the abstraction from the implementations so they can be used and changed independently.
   
   Let's look at an example to understand when this is useful and what this "confusing" definition means.
   Say you need to create a shape drawing application that should work on both Windows and MacOS.
   
   You could create a Shape interface, inherit from it the types of the shapes, like Rectangle or Circle, and then inherit from those to create the OS-specific implementations.
   The class hierarchy would look like this:
   
   
   ![alt text](/assets/images/design_patterns/20190517_122228.png "Bridge Design Pattern")
   
   
   Now, consider that you need to support more shape types and more OSes. That would lead to a significant number of classes being added - the number of types multiplied by the number of OS versions. 
   
   So, basically, to support five shape types on three different OSes, you would need to write 5*3=15 implementations.
   
   However, the Bridge pattern suggests refactoring this into two separate hierarchies - one for platform-independent abstractions (Shapes), and the other for platform-dependent implementations (OSes).
   Here is the refactored diagram:
   
   ![alt text](/assets/images/design_patterns/20190517_122126.png "Bridge Design Pattern")
   
   The relationship between Shape and ShapeImplementation is the Bridge.
   
   This pattern is used in situations where it would be best to isolate the handling of the system-dependent stuff from the handling of the system-independent stuf


> The Bridge pattern is often confused with the Adapter pattern.
  Adapter makes things work after they're designed;  
  Bridge is designed up-front to let the abstraction and the implementation vary independently. Further, Adapter is retrofitted to make unrelated classes work together.
  In other words, an adapter is a patch. A bridge is put in place on purpose.

---

## Composite Design Pattern
   
   The Composite pattern describes a group of objects that is treated the same way as a single instance of the same type of object. 
   
   Composite should be used when clients ignore the difference between compositions of objects and individual objects.
   
   For example, when dealing with tree-structured data, programmers often must discriminate between a leaf-node and a branch. This makes code more complex, and therefore, more error-prone. 
   The solution is an interface that allows treating complex and primitive objects uniformly. 
   Other examples are menus that contain menu items, each of which could be a menu. Directories that contain files, each of which could be a directory.


> The key concept is that you can manipulate a single instance of the object just as you would manipulate a group of them.

---

## Decorator Design Pattern
   
   The Decorator design pattern allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class.
   
   This is achieved by designing a new Decorator class that wraps the original class. This pattern is designed so that multiple decorators can be stacked on top of each other, each adding a new functionality.
   
   The goal is to make it so that the extended behavior can be applied to one specific instance, and, at the same time, still be able to create an original instance that doesn't have the new behavior.
   
   This pattern is an alternative to subclassing, which refers to creating a class that inherits functionality from a parent class. As opposed to subclassing, which adds the behavior at compile time, "decorating" allows you to add new behavior during runtime, if the situation calls for it.
   
   For example, consider a window in a windowing system. Assume windows are represented by instances of the Window class, and assume this class has no functionality for adding scrollbars. 
   We could create a subclass ScrollingWindow that provides them, or create a ScrollingWindowDecorator that adds this functionality to existing Window objects. At this point, either solution would be fine.
   
   Now, assume one also desires the ability to add borders to windows. If we had used subclassing, then we have a problem, as we will need to create separate subclasses with the borders functionality for all possible types of windows.
   With the decorator solution, we simply create a new BorderedWindowDecorator and decorate any window we need during runtime. 
   
   So, using decorator, we have the ability to add scrollbars and/or borders to any of our Windows objects.
   
   Notice that if the functionality needs to be added to all Windows, you could modify the base class and that will do. However, sometimes (e.g., when using external frameworks) it is not possible, legal, or convenient to modify the base class.


> The I/O Streams implementations of both Java and the .NET Framework follow the decorator pattern by extending the base subclass to add features to the stream classes.

---

## Facade
   
   The Facade design pattern provides a unified interface to a set of interfaces in a subsystem, thus making a complex subsystem easier to use.
   
   A facade is an object that provides a simplified interface to a larger body of code, such as a class library.
    A facade can:
    - make a software library easier to use, understand, and test, since the facade has convenient methods for common tasks,
    - make the library more readable,
    - wrap a poorly designed collection of APIs with a single well-designed API.
   
   The Facade design pattern is often used when a system is very complex or difficult to understand because the system has a large number of interdependent classes or its source code is unavailable. This pattern hides the complexities of the larger system and provides a simpler interface to the client. It typically involves a single wrapper class that contains a set of members required by the client. These members access the system on behalf of the facade client and hide the implementation details.
   
   The $ in jQuery, which provides a simple interface to common operations, is an example of the Facade design pattern.


> Adapter and Facade are both wrappers, but they are different kinds of wrappers. The intent of Facade is to produce a simpler interface, and the intent of Adapter is to design to an existing interface.

---

## Flyweight Design Pattern 
   
   The Flyweight design pattern efficiently supports a large number of objects.
   A flyweight is an object that minimizes memory usage by sharing as much data as possible with other similar objects; it is a way to use objects in large numbers when a simple repeated representation would use an unacceptable amount of memory. 
   
   For example, when representing large text documents, creating an object for each character in the document would result in a huge number of objects that couldn't be processed efficiently. Instead, for every character there might be a reference to a flyweight glyph object shared by every instance of the same character in the document; only the position of each character in the document would need to be stored internally.
   
   As another example, modern web browsers use this technique to prevent loading the same images twice. When a browser loads a web page, it traverses through all images on that page. The browser loads all new images and places them in the internal cache. For already loaded images, a flyweight object is created, which has some unique data-like position within the page, but the image itself is referenced from the cache.


> To enable safe sharing between clients and threads, Flyweight objects must be immutable. 
  Flyweight objects are by definition value objects. The identity of the object instance is of no consequence; therefore, two Flyweight instances of the same value are considered equal.

---

## Proxy Design Pattern
    
   The Proxy design pattern provides a placeholder for another object to control access to it.
   
   A proxy is a class functioning as an interface to something else, such as a network connection, a large object in memory, a file, or some other resource that is expensive or impossible to duplicate.
   A proxy acts as a wrapper object that is being called by the client to access the real serving object behind the scenes. For the client, usage of a proxy object is similar to using the real object, because both implement the same interface.
   
   Possible Usage Scenarios
   Remote Proxy
   In distributed object communication, a local object represents a remote object. The local object is a proxy for the remote object, and method invocation on the local object results in remote method invocation on the remote object. An example would be an ATM implementation, where the ATM might hold proxy objects for bank information that exists in the remote server.
   
   Virtual Proxy
   In place of a complex or heavy object, a skeleton representation may be advantageous in some cases. When an underlying image is huge in size, it may be represented using a virtual proxy object, loading the real object on demand.
   
   Protection Proxy
   A protection proxy might be used to control access to a resource based on access rights.


> A proxy can:
   - hide information about the real object from the client.
   - perform optimization like on-demand loading.
   - do additional housekeeping jobs like audit tasks.



