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
  - Composition, in a code sense, is when an object's fields are objects themselves.

## **Solid Principles**
1. **Single Responsibility Principle** - Classes should be encapsulated to handle one responsibility
2. **Open/Closed Principle** - Classes should be closed for modification but open to extension
3. **Liskov Substitution Principle** - Methods on the superclass and subclass can be used interchangably, link back to polymorphism. The same behavior should be consistent if I invoke a method from the parent function. For example, if I have a Rectangle parent class with setWidth and setHeight methods and a square class is inherited from the rectangle, the square will need to override the setWidth and setHeight method to maintain the square's invariant (truthiness). By overriding and changing behavior of the methods of the parent class we violate the substitution principle.
4. **Interface Segregation** - Separate large interfaces into smaller interfaces
5. **Dependency Inversion** - Low level modules should depend on high level abstractions and not the other way around. Low level code normally describes very specific functionality for a program, while high level provide high level abstractions for a business requirement. Low level code is often difficult to change, hence why high level code shouldn't depend on it. Optimally, most code should rely on abstractions.

## **Design Patterns**

  ## **Creational Design Patterns**
  Common patterns describing various ways of object creation

### 1. Factory Method
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
- The factory method is utilized when
  - Constructing an object consist of various dependencies and is a complicated process
  - A single constructor is not expressive enough

### 2. Abstract Factory Method
   - An abstract factory is used when we need to create several different types of related objects. For example, in our previous example our factory could only create one type of product: phones, if we were to introduce a new product, the factory pattern would not be scalable. Imagine we would need to have a switch statement for whatever product we are going to create. The abstract factory pattern is similar to the factory pattern in the sense it is used to create objects, but varies since the abstract factory pattern is scalable when creating multiple products.
   - The abstract factory design pattern will consist of:
     1. **Abstract Products**: An interface which contains abstracted methods for the type of proudcts we are creating. In our abstract factory we will be handling multiple products. As an example we could have a phone product and computer product. The abstract product will declare interfaces containing methods for the phone and computer. The phone interface could have an abstract call() and text() methods, while the computer interface could have 
 abstracted methods for program() and storeData().
     2. **Concrete Products**: Actual implementation of the abstract products. Basically, the concrete products are implementations of the abstract products. For example, our concrete products for the phone interface and computer interface could be iPhone and Google Pixel and Mac and Chromebook respectively. In our example, the concrete product effectively gives "specialization" to a generic abstraction.
     3. **Abstract Factory**: An interface which contains methods for creating abstract products. In our example we would have a HardwareFactory with abstracted methods such as createComputer() and createPhone().
     4. **Concrete Factories**: Implements the abstract factory to return the concrete products. Continuing with our example, we would have two concrete factory classes: 1. GoogleFactory and 2. AppleFactory. The GoogleFactory would create methods for instantiating a new Google Pixel and ChromeBook, the AppleFactory would do the same for apple products. 
  - Note: The return type for all factories (Abstract and Concrete) should be the abstract products in order to prevent the factory from being coupled to any specific product variant.

  - With abstract factories there is typically a client application class. The client application contains fields for the abstract products, a constructor which accepts the abstracy factory and subsequently creates the variants for the type of concrete product, and performs business logic on the newly created products.
    
![Abstract Factory DP](https://github.com/JustinHLe/Design-Patterns/assets/25164200/8f71981c-04b0-454f-bc00-fd48da4be44e)

- The picture above is best read from right to left. We have a client application which has a constructor that accepts a GUIFactory, the parameter will most likely be a class which implements the GUIFactory. When the constructor is invoked the button field will be initialized by the respective concrete factory to produce a concrete product. Finally, the business logic methods such as createUI() and paint() can be invoked. To avoid coupling the field button will be used in the business rule methods. Everything in the client application must use the abstracted code.
- The abstract factory method is used when
  - Handling multiple related products that require loose coupling
  - The main difference between the factory design pattern and abstract design pattern is that the factory pattern is established by inheritance, while the abstract factory is established by composition. The factory pattern defines an abstraction for creating objects but delegates implementation of the abstraction to the subclasses. In addition, the interface will refer to the newly created objects through a common interface. The abstract factory pattern instantiates and refers to its objects through composition (the application's fields are most likely abstract products). The instantiation process for an abstract factory will depend on what type of factory is required as part of business rules. Remember that abstract factory pattern is more or less a super factory which produces factories. These factories in turn produce the products. The abstract factory patterns helps us produce variants of the same products.
  - The main similarities between the factory design pattern and the abstract design pattern is that both are creational design patterns which abstract object creation. In addition, both have a notion of a certain product  to create as well as defining behavior for said products.

### 3. Builder Pattern
  - The builder pattern allows an object to be created step-by-step and with the minimal requirements necessary.
  - The builder pattern is useful when we want to create variants of an object without having to create an overly complicated constructor or having to create a subclass for each object variant
  - The builder pattern will consist of:
    1. **Builder Interface**: An interface which declares product construction steps. For example, if we are creating a PC we could have a builder interface with methods such as withGPU(), withMotherBoard(), withCPU().
    2. **Concrete Builders**: Actual implementation of the builder interface which inevitably creates a new product. The products created from the concrete builders don't have to be related to the common builder interface. For example, we could have a PCBuilder which implements the methods from the builder interface and we could have a GamingConsoleBuilder which implements the same methods from the interface. Notice that a PC is not inherently related to a gaming console.
    3. **Products**: The actual product object created by the concrete builders. In our example we would have a PC and GamingConsole object and their respective classes which contains behavioral methods. The classes will typically contain getters and business logic.
    4. **Director**: An optional class which defines an order for step creation. The director allows for different objects to be constructed by interacting with the common builder interface. The different types of objects constructed will be dictated by which concrete builder is passed to the director. For example, we could have a director class called HardwareStore. The hardware store has no notion of what builder is being utilized, it is only aware of how to build something. For example, the client will typically invoke the director and pass a concrete builder into its constructor. The director object then can invoke any of its builder methods constructing whatever object is required from the concrete builder. In our example, we could invoke the director class with an instance of our PCBuilder. From there the director can call a method called constructPC() which utilizes the polymorphic builder interface to create a PC object. Alternatively, we could invoke the director class with an instance of our GamingConsoleBuilder and do the same.
   
       
![Builder Design Pattern](https://github.com/JustinHLe/Design-Patterns/assets/25164200/8aa3105f-9847-4a30-85d8-017d4ffc7b22)

- The picture above visualizes the design pattern. The entry point is the client which invokes one of the director's methods with an instance of the CarBuilder(). The director is told by the client to make a sportsCar using the carBuilder. By following its commands, the director utilizes the builder interface to construct the sports car. The director is able to call upon the generic builder interface since the car builder implements the interface. The fact that the builder works with a generic interface allows us to create different objects such as a Car or Car Manual. Once the builder finishes construction, we can create a new product object by invoking the concrete builder's (in our case the Car Builder) result() method which returns a new Car instance.
- The builder object is typically used when we want to construct an object with many fields, but don't want a bloated constructor. 

Example Code: 
```
public class Pizza {
  private int size;
  private boolean cheese;
  private boolean pepperoni;
  private boolean bacon;

  public static class Builder {
    //required
    private final int size;

    //optional
    private boolean cheese = false;
    private boolean pepperoni = false;
    private boolean bacon = false;

    public Builder(int size) {
      this.size = size;
    }

    public Builder cheese(boolean value) {
      cheese = value;
      return this;
    }

    public Builder pepperoni(boolean value) {
      pepperoni = value;
      return this;
    }

    public Builder bacon(boolean value) {
      bacon = value;
      return this;
    }

    public Pizza build() {
      return new Pizza(this);
    }
  }

  private Pizza(Builder builder) {
    size = builder.size;
    cheese = builder.cheese;
    pepperoni = builder.pepperoni;
    bacon = builder.bacon;
  }
}

```

### 4. Prototype
  - The prototype design pattern allows an object to be cloned without creating any code dependency on the class of the object being cloned. The important thing to remember here is that cloning does not refer to creating another instance which points to the same object in memory, rather a new object is created from a base object which contains the base's fields. A common interface which contains a clone method is typically utilized to decouple an object from its class when cloning. The interface will be used to invoke the clone method and depending on which object the interface type is instantiated to will invoke the clone method respectively. 
  - The prototype design pattern is coined by the fact that an initial object acts as a prototype containing all the data required to create duplicates of itself.
  - A shallow copy does not create a new object but rather references the same object as the cloners'. A deepy copy will prodce a new object and will not reference the same object as the cloners'. 
  - The prototype design pattern will consist of:
    1. **A prototype interface**: The interface is typically an abstract class which defines a clone() method.
    2. **Concrete Prototype**: A class which extends the prototype interface and implements the clone method. Any objects which extend the prototype interface are objects suitable for cloning.
    3. **Client**: The client will typically accept any concrete prototype and invoke the clone method. The client is the thing which allows us to decouple our object from the class. This is due to the fact that the client will only interact with the concrete prototype through their interface type.
    4. **Prototype Registry**: A prototype registry is sort of like a cache. It is typically a java class that stores prototypes which are made available for cloning. The prototype registry class will typically contain a map and whenever a key is retrieved a clone of the key's value will be returned.
    
![Prototype DP](https://github.com/JustinHLe/Design-Patterns/assets/25164200/b18a63f9-89a8-43c2-846e-f2cc38b79118)

- The above image demonstrates the clone design pattern. The shape is our prototype interface which contains an abstracted method called clone. The concrete prototypes, rectangle and circle, implement the shape interface and clone method. Typically, most clone methods will invoke `return new Object(this)` (e.g. `new Circle(this`); the constructor will typically invoke the super constructor while passing in `this` to clone any fields from the parent if any. In our case, rectangle/circle will invoke the super class constructor in `Shape`.
- The prototype design pattern is typically used in cases where an object with the same data needs to be created. For example, if a network request returns the same JSON, instead of initializing a new object on every request we can simply create a prototype and return it instead of having to make a network call. The prototype pattern can also be used as a substitute for object creation. For example, if we want to create multiple objects with slight differences from the same class we can either create a subclass for each unique object or create a prototype of each object and provide a clone of the object itself when required. Finally, the prototype interface allows some form of abstraction, instead of depending on a concrete class to clone (which is typically the case during runtime) we can invoke `clone` on a common interface which allows us decouple our relationship with concrete classes.

### 5. Singleton
  - The singleton design pattern allows a class to produce only instance for itself throughout the entire application. 
  - See code example below for design:
```
// Class declared as final to prevent extension
public final class MySingleton {
    private static MySingleton INSTANCE = new MySingleton();

    private MySingleton() { // private constructor cannot instantiate new object outside of this class    
    }
    
    // global access to singleton
    // 
    // 
    public static MySingleton getInstance() { 
      return INSTANCE;
    }
}

public class MyMainClass() {
   public static void main(String[] args) {
        // MySingleton class loaded in JVM, class loading occurs when information about a class is required
        // 
 	MySingleton mySingleton = MySingleton.getInstance(); 
   }
}
```


