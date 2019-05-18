---
title: "Solid Principles"
excerpt: "Solid Principles test..."
permalink: /posts/solid-principles/
layout: single
toc: true
author_profile: true
read_time: true
comments: true
share: true
related: true
search: true
categories: 
  - Solid
last_modified_at: 2018-07-11T08:06:00-05:00
---

# Solid Principles

SOLID is one of the most popular sets of design principles when doing OOD (Object Oriented Design). 
SOLID principles can also form a core philosophy for methodologies such as agile development or adaptive software development.

The intention of these principles is to make software designs more understandable, easier to maintain and easier to extend.


It’s a mnemonic acronym for the following five design principles:

- Single Responsibility Principle
- Open/Closed Principle
- Liskov Substitution Principle
- Interface Segregation Principle
- Dependency Inversion

These 5 principles were introduced by Robert C. Martin (Uncle Bob), in his 2000 paper [Design Principles and Design Patterns](https://web.archive.org/web/20150906155800/http://www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf).


## S — Single Responsibility Principle(S.R.P)

> "A class should have one, and only one, reason to change."
Martin, Robert C. (2003). Agile Software Development, Principles, Patterns, and Practices. Prentice Hall. p. 95. ISBN 978-0135974445.


-------
### Benefits
It makes your software easier to implement and prevents unexpected side-effects of future changes.

### Concepts

A module, class, or function should have responsibility over a single part of the functionality provided by the software, and that responsibility should be entirely encapsulated by the class.


### Examples

We have a class named Book.
We use a method called formatJson() to return the book as a JSON string.

```php
class Book {
  protected $title;
 
  public getBook($title) {
    return $this->title;
  }
 
  public function formatJson() {
    return json_encode($this->getTitle());
  }
}
```

If we want to change the output of the JSON string, or add another type of output to the class, we would need to alter the class to either add another method or change an existing method to suit.

How can we solve it so that it complies with the Single Responsibility Principle?.

We create a secondary class called JsonPageFormatter that is used to format the Page objects into JSON.

```php
class Book {
  protected $title;
 
  public getBook($title){
    return $this->title;
  }
}
 
class JsonPageFormatter {
    public function format(Book $book) {
        return json_encode($book->getTitle());
    }
}
```

Doing this means that if we wanted to create an XML format we could just add a class called XmlPageFormatter and write some simple code to output XML.


> It is one of the basic principles most developers apply to build robust and maintainable software. You can not only apply it to classes, but also to software components and microservices.




## O — Open-Closed Principle

> "Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification"
Meyer, Bertrand (1988). Object-Oriented Software Construction. Prentice Hall. ISBN 0-13-629049-3.

### Benefits

It promotes the use of interfaces to enable you to adapt the functionality of your application without changing the existing code.

If we could follow this principle strongly enough, it is possible to then modify the behavior of our code without ever touching a piece of original code.

### Concepts

We can make sure that our code is compliant with the open/closed principle by utilizing inheritance and/or implementing interfaces that enable classes to polymorphically substitute for each other.

This simply means that a class should be easily extendable without modifying the class itself. 

We should always try to add new code instead of changing existing code.

### Example

We have two different books and handle them with a switch case. 
Based on the type variable in the array we load in the correct book class to then echo the correct visual name. 

```php
class ScienceBook 
{
    public $type = 'Science';
    private $bookTitle;
    private $bookDescription;
    public function __construct($book) { ... }
    public function getbookTitle() 
    {
        return $this->bookTitle;
    }
    public function getBookDescription() 
    {
        return $this->bookDescription;
    }
}

class FictionBook 
{
    public $type = 'Fiction';
    private $authorName;
    public function __construct($book) { ... }
    public function getAuthorName() {
        return $this->authorName;
    }
}

class AllBooks
{
    public function show($books) {
        foreach ($books as $book) {
            switch ($book->type) {
                case 'Science':
                    echo $book->getFirstName().' '.$book->getLastName();
                    break;
                case 'Fiction':
                    echo $book->getAuthorName();
                    break;
            }
        }
    }
}
```

If we add a third book type then we would also need to change the existing switch case and thus break this principle.

How can we solve it so that it complies with the Open-Closed Principle?.

We created an interface which we use to extend each of the Book types. If we now add a third type, then we have no reason to change any existing code. We just add new code to add new functionality.

```php
interface Book {
    public function getName();
}

class ScienceBook implements Book {
    private bookTitle;
    private bookDescription;
    
    public function __construct($book) { ... }
    public function getName() {
        return $this->bookTitle.' '.$this->bookDescription;
    }
}

class FictionBook implements Book
{
    private $authorName;
    
    public function __construct($book) { ... }
    public function getName() 
    {
        return $this->authorName;
    }
}

class AllBooks 
{
    public function show($books) 
    {
        foreach ($books as $book) {
            echo $book->getName();
        }
    }
}
```


## L — Liskov Substitution Principle

> Let Φ(x) be a property provable about objects x of type T. Then Φ(y) should be true for objects y of type S where S is a subtype of T.

> Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.

### Benefits

The behavior of your classes becomes more important than its structure.

### Concepts

The Liskov Substitution principle was introduced by [Barbara Liskov](https://en.wikipedia.org/wiki/Barbara_Liskov) in her conference keynote [Data abstraction and hierarchy](https://doi.org/10.1145%2F62139.62141) in 1987.

Liskov Substitution Principle extends the Open/Closed Principle by focusing on the behavior of a superclass and its subtypes.

The principle defines that objects of a superclass shall be replaceable with objects of its subclasses without breaking the application. That requires the objects of your subclasses to behave in the same way as the objects of your superclass.

An overridden method of a subclass needs to accept the same input parameter values as the method of the superclass. That means you can implement less restrictive validation rules, but you are not allowed to enforce stricter ones in your subclass.

### Examples

In this example we extend Square from Rectangle. The difference between a square and rectangle is that a square its sides are always the same size. So if we set height or width we need to change both height and width.

```php
class Rectangle
{
    protected $height;
    protected $width;

    public function setHeight(int $height)
    {
        $this->height = $height;
    }
    
    public function setWidth(int $width)
    {
        $this->width = $width;
    }
}

class Square extends Rectangle
{
    public function setHeight(int $height)
    {
        $this->height = $height;
        $this->width = $height;
    }
    
    public function setWidth(int $width)
    {
        $this->height = $width;
        $this->width = $width;
    }
}
```

A solution to this example is to have an Abstract class where both will have different setters to calculate the sides and we have one general function which calculates the area.

```php
abstract class AbstractShape
{
    abstract public function Area() : int;
}

class Rectangle extends AbstractShape
{
    private $height;
    private $width;
    
    public function setHeight(int $height)
    {
        $this->height = $height;
    }
    
    public function setWidth(int $width)
    {
        $this->width = $width;
    }
    
    public function Area() : int
    {
        return $this->height * $this->width;
    }
}

class Square extends AbstractShape
{
    private $sideLength;
    
    public function setSideLength(int $sideLength)
    {
        $this->sideLength = $sideLength;
    }
    
    public function Area() : int
    {
        return $this->sideLength * $this->sideLength;
    }
}
```


## I — Interface Segregation Principle

> Clients should not be forced to depend upon interfaces that they do not use.

### Benefits

You can apply these principles also to microservices.

### Concepts

The goal of the Interface Segregation Principle is to reduce the side effects and frequency of required changes by splitting the software into multiple, independent parts.

### Examples

We have an interface Book. We implement an Paper class. Then we have a problem, because an Paper is a book, but it can’t be download.

```php
interface Book 
{
    public function read();
    public function download();
}

class Ebook implements Book
{
    public function read() { ... }
    public function download() { ... }
}

class Paper implements Book
{
    public function read() { ... }
    public function download() { /* exception */ }
}
```

We should solve this by creating a separate interface for digital books and paper books.

```php
interface Book
{
    public function read();
}

interface DigitalBook
{
    public function download();
}

interface PaperBook
{
    public function buy();
}

class Ebook implements Book, DigitalBook
{
    public function read() { ... }
    public function download() { ... }
}

class Paper implements Book, PaperBook 
{
    public function read() { ... }
    public function buy() { ... }
}
```


## D — Dependency Inversion Principle

> High-level modules should not depend on low-level modules. Both should depend on abstractions.
> Abstractions should not depend on details. Details should depend on abstractions.

### Benefits

Decouple your code from its direct dependencies.

### Concepts

We have high level modules and low level modules. In simplest terms the high level modules are the ones we call directly and do all the high level business logic. Low level modules are classes that help our high level modules, this can be inserting data to a database or printing a date in the correct format.

High-level modules, which provide complex logic, should be easily reusable and unaffected by changes in low-level modules, which provide utility features. To achieve that, you need to introduce an abstraction that decouples the high-level and low-level modules from each other.

An important detail of this definition is, that high-level and low-level modules depend on the abstraction.

### Examples

```php
interface Adapter
{
    public function getData();
}

class Mysql implements Adapter
{
    public function getData()
    {
        return 'data from database';
    }
}

class Controller
{
    private $adapter;
    public function __construct(Mysql $mysql)
    {
        $this->adapter = $mysql;
    }
    function getData()
    {
        $this->adapter->getData();
    }
}
```

In this example we can only pass an object of the database type.


```php
interface Adapter
{
    public function getData();
}

class Mysql implements Adapter
{
    public function getData()
    {
        return 'data from database';
    }
}

class Controller
{
    private $adapter;
    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }
    function getData()
    {
        $this->adapter->getData();
    }
}
```

Now we can pass whatever implementation we want based on our Adapter interface.


## References

- [SOLID](https://en.wikipedia.org/wiki/SOLID)
- [Single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)
- [Open-closed principle](https://en.wikipedia.org/wiki/Open-closed_principle)
- [Liskov_substitution_principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle)
- Robert C. Martin, [The Liskov Substitution Principle](https://web.archive.org/web/20151128004108/http://www.objectmentor.com/resources/articles/lsp.pdf), C++ Report, March 1996
- [Interface segregation principle](https://en.wikipedia.org/wiki/Interface_segregation_principle)
- [Dependency inversion principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle)
