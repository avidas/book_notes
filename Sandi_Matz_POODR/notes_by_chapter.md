### Chapter 1
### Chapter 2
### Chapter 3
### Chapter 4
* Think OOD as messages that need to pass between objects
* Notice domain objects but focus on messages that need to pass between them
* Public interfaces should reveal primary responsibility, describe what not how, take hash as options parameter
* UML diagrams switch attention from objects to messages to concentrate on building application with public interfaces
* UML sequence diagrams should be experimental and will be discarded, they create intention that is the starting point of the design
* By reducing how much object needs to know about other objects, we lower context and easier to reuse
* Sender of the message should trust the receiver to behave appropriately without knowing context
* _ to denote private might be preferable as they supply information about method stability without imposing visibility restrictions
* LOD prohibits routing message to third object via a second object of different type, only talk to immediate neighbors

### Chapter 5
* Duck typing detaches public interfaces from specific classes, creating vitual types that are defined by what they do (i.e. what messages they accept) rather than what they are, reveals underlying abstractions.
* Polymorphism in OOP refers to ability of many different objects to respond to the same message. Receivers of message supply their own specific version of behavior
* When observer patterns such as kind, is_a, responds_to focus on the code's expectations and use it to find duck type. 
* When classes being changed are stable e.g. framework/stdlib, 
* Static: compile time error checking, type checks documented, compiled code faster
* Dynamic: Interpreted and dynamically loaded code, no compile/make cycle; easier metaprogramming

### Ch 6:  Acquiring Behavior Through Inheritance

* Inheritance provides automatic message delegation from subclasses to superclasses

* When your problem is one of needing numerous specializations of a stable, common abstraction, inheritance can be an extremely low-cost solution.

* Inheritance solves the problem of highly related types that share common behavior but differ along some dimension

* Creating empty superclass and pushing abstract bits of code up to it can be done carefully without fear of leaving concrete artifacts

* The general rule for refactoring into a new inheritance hierarchy is to arrange code so that you can promote abstractions rather than demote concretions.

* This technique of defining a basic structure in the superclass and sending messages to acquire subclass-specific contributions is known as the template method pattern. Always document template method requirements by implementing matching methods that raise useful errors.

* When a subclass sends super it’s effectively declaring that it knows the algorithm;it depends on this knowledge. If the algorithm changes, then the subclasses may break even if their own specializations are not otherwise affected.

* Abstract superclasses use hook methods to allow inheritors to contribute specializations without being forced to send super, i.e. subclasses don’t have to know the abstract algorithm

* Don't underestimate value of sb who really wants to do



### Ch 7: Sharing Role Behavior with Modules

* When objects that play a common role need to share behavior, they do so via a Ruby module. The code defined in a module can be added to any object, be it an instance of a class, a class itself, or another module.

* Inheritance falls short when subclass requires combining the qualities of two existing superclasses

* Modules in Ruby provides a way to define a named group of methods that are independent of class and can be mixed in to any object, allowing objects of different classes to play a common role using a single set of code

* With modules as well as classical inheritance, if a module sends a message it must provide an implementation, even if to just raise an error indicating users of this module must implement the method

* Inheritance is is-a, modules is behaves-like-a

* The methods of the last included module are encountered first in the lookup path

* First, an object that uses a variable with a name like type or category to determine what message to send to self contains two highly related but slightly different types. Second, when a sending object checks the class of a receiving object to determine what message to send, you have overlooked a duck type.

* Avoid writing code that requires its inheritors to send super; instead use hook messages to allow subclasses to participate while absolving them of responsibility for knowing the abstract algorithm.

* Deep hierarchies of classes introduce long search path for message resolution and large set of built-in dependencies. 

* Liskov Substitution Principle, which in mathematical terms says that a subtype should be substitutable for its super type



### CH 8: Combining Objects with Composition

* In composition, the larger object is connected to its parts via a has-a relationship. It communicates with them via an interface.
* Factory is an object that manufactures other objects. It can isolate all the knowledge required to create a valid object instead of being dispersed throughout the application
* OpenStruct is convenient way to bundle a number of attributes into an object. It can be used to bundle attributes to play a certain Role
* Aggregation is similar to composition except the contained object has an independent life
* Inheritance: For the cost of arranging objects in a hierarchy, you get message delegation for free. Classical inheritance is a code arrangement technique. Behavior is dispersed among objects and these objects are organized into class relationships such that automatic delegation of messages invokes the correct behavior
* Composition: Objects stand alone and as a result must explicitly know about and delegate messages
to one another. Composition allows objects to have structural independence, but at the cost of explicit message delegation. Composition contains far fewer built-in dependencies than inheritance; it is very often the best choice.
* Use of inheritance results in code that can be described as open–closed; hierarchies
are open for extension while remaining closed for modification. Hierarchies are therefore exemplary; by
their nature they provide guidance for writing the code to extend them.
* Inheritance may create situation when no way to ad new behavior or make future users tolerate the dependencies inheritance demands
* Avoid writing frameworks that require users of your code to subclass your objects in order to gain your behavior. Their application’s objects may already be arranged in a hierarchy; inheriting from your framework may not be possible
* Composition results in applications built of simple, pluggable objects that are easy to extend and have a high tolerance for change, since it is more transparent. Because composed objects deal with their parts via an interface, adding a new kind of part is a simple matter of plugging in a new object that honors the interface.
* Composition is excellent at prescribing rules for assembling an object made of parts but doesn’t provide as much help for the problem of arranging code for a collection of parts that are very nearly
identical.
* Use Duck Types for behaves-like-a Relationships: Playing the role is not Objects main responsibility, many otherwise unrelated objects share a desire to play the same role
* For every problem, assess the costs and benefits of alternative design techniques and use your judgment and experience to make the best choice.

### CH 9: Designing Cost-Effective Tests

* Tests help with 
    1. Finding Bugs 
    2. Supplying Documentation
    3. Deferring Design Decisions
    4. Supporting Abstractions
    5. Exposing Design Flaws

* The true purpose of testing, just like the true purpose of design, is to reduce costs.
* Incoming messages should be tested for the state they return. Outgoing command messages should be tested to ensure they get sent. Outgoing query messages should not be tested.
* When your intention is to defer a design decision, do the simplest thing that solves today’s problem.
* From the point of view of the object under test, every other object is a role and dealing with objects as if they are representatives of the roles they play loosens coupling and increases flexibility, both in your application and in your tests.
* If you leverage Liskov and create new subclasses that are used exclusively for testing, consider requiring these subclasses to pass your subclass responsibility test to ensure they don’t accidentally become obsolete.