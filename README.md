# **Object Oriented Programming Fundamentals**

* An Object's field is called state, its methods is called behavior
	
## **4 pillars of OOP**

1. **Abstraction** - Classes are often based on real world models, however these models often time give us more information than we need. When we abstract something, we effectively say we only want to construct parts of the model that matter to us.
2. Encapsulation - Encapsulation is a little similar to abstraction except that encapsulation focuses solely on restricting complex/private state or behavior from other resources within the program. Encapsulation is sort of an extension of abstraction, where in abstraction we specifically choose how to build an object and with encapsulation we hide complex/private behavior that is unnecessary for the rest of the program to use when working with the object that we built.
3. Inheritance - Limits code duplicity when object state or behavior is similar
4. Polymorphism - In literal terms, the definition of polymorphism means representing many forms. In code terms a superclass can have multiple subclasses where each subclass overrides a particular method in the superclass. Because of polymorphism we can assign the parent class to an instance of the subclass and when the parent invokes the overriden method the child method will be called. The parent invocation is the literal defintion of one thing representing many forms, since each invocation, even though using the same method, will produce an unique result.

## **Object Relations**

1. **Dependency** - A class depends on another class (e.g. dependency injection into the method's parameter)
2. **Association** - A class is tightly coupled with another class meaning it holds a reference to it via the class' field
3. **Aggregation** - An object can exist independently from the class which owns it, subset of association
   * The object may live on if the parent is destroyed
4. **Composition** - An object cannot exist indendently from the class which owns it, subset of association
   * The object is destroyed when its parent is destroyed

## **Design Patterns**

1. **Creational Patterns** - Involves object creation
2. **Structural Patterns** - Involves structuring objects/classes, class hiearchy
3. **Behavioral Patterns** - Handles communcation and responsibilities between objects

## **Important Design Principles**

- Encapsulate varied behavior
  - This can either be encapsulated in a class or a method
- Program to an interface
  - Removes tightly coupled object behavior. If we code to a specific object we are saying we want this exact thing to do this exact behavior. Whereas if we code to an interface we provide a generic way of defining what an object will do. This is effectively polymorphism.
- Favor Composition over Inheritance
  - Classes should only inherit a superclass if and only if the subclass has a "is-a" relationship. The "is-a" relationship defines that every method in the parent will be overriden with some behavior in the child. Additionally, the child itself will introduce new behavior. In other cases of object dependency where there isn't a "is-a" relationship, composition should be considered. With Composition we define only specific behavior which should be implemented not the entire interface. The object relationship for composition is a "has-a" relationship.
  - It's easier to create classes with a "has-a" relationship because there is less coupling compared to a "is-a" relationship.

## **Solid Principles**
1. **Single Responsibility Principle** - Classes should be encapsulated to handle one responsibility
2. **Open/Closed Principle** - Classes should be closed for modification but open to extension
3. **Liskov Substitution Principle** - Methods on the superclass and subclass can be used interchangably, link back to polymorphism. The same behavior should be consistent if I invoke a method from the parent function. For example, if I have a Rectangle parent class with setWidth and setHeight methods and a square class is inherited from the rectangle, the square will need to override the setWidth and setHeight method to maintain the square's invariant (truthiness). By overriding and changing behavior of the methods of the parent class we violate the substitution principle.
4. **Interface Segregation** - Separate large interfaces into smaller interfaces
5. **Dependency Inversion** - Low level modules should depend on high level abstractions and not the other way around. Low level code normally describes very specific functionality for a program, while high level provide high level abstractions for a business requirement. Low level code is often difficult to change, hence why high level code shouldn't depend on it. Optimally, most code should rely on abstractions.

## **Design Patterns**

  ### **Creational Design Patterns**
  Common patterns describing various ways of object creation

1. Factory Method
  - The factory method is used for object creation. It will define an interface (abstract or interface) for creating objects and any subclasses which inherit this interface will instantiate the respective objects to create. The factory method contains four elements.
    1. **Product**: An interface containing methods for the behavior of objects created by the creator, effectively like a generic interface for the type of products the program is creating. An example of what the product interface would be is simply a phone interface for phone behavior. A phone can have methods such as call() or text(), but at the same time there can be different types of phones.
    2. **Concrete Products**: Actual Implementations of the product interface. An example of concrete products would be the actual implementation of the phone interface. For example we could have
an IPhone class which implements the Phone product interface with concrete call() and text() methods for an iphone. We could also have a Samsung Phone class which does the same.
    3. **Creator**: Class which contains the factory method to produce new objects. Abstract class which has a factory method to create objects. However, the actual implementation of object creation is handled by
its subclasses. In addition, the creator class will contain methods which interact with the client. For example, in our phone example, the creator class would provide an abstract method to create phones and will call upon the product interface to execute business logic.
    4. **Concrete Creators**: Class which contains method to override the factory method in the creator to create new products. Extends the creator class and provides the actual implementation
of what type of object to create. In our phone example the concrete creators would return the different type of phone objects.


![Factory Design Pattern](https://github.com/JustinHLe/Design-Patterns/assets/25164200/a0ecb497-bcff-49c0-89e2-16e204516a97)

- Picture above is a good example. We see that the creator has a factory method called createProduct() which is used to create various types of a product. In addition it has another method called someOperation() to handle business logic. The someMethod() opeartion creates a product depending on the particular object that the creator class is instantiated to and subsequently does some operations on the newly created object via the product interface. The factory pattern is effectively like a factory which handles the creation of an object and the execution of the object's business logic; the only exception is that the factory itself is entirely decoupled from any of the objects it creates and object-related business logic.
- The factory method is utilized when we're obviously creating 

