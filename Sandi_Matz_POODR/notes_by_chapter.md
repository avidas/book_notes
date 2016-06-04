### Chapter 1
### Chapter 2
### Chapter 3
### Chapter 4
-- Think OOD as messages that need to pass between objects
-- Notice domain objects but focus on messages that need to pass between them
-- Public interfaces should reveal primary responsibility, describe what not how, take hash as options parameter
-- UML diagrams switch attention from objects to messages to concentrate on building application with public interfaces
-- UML sequence diagrams should be experimental and will be discarded, they create intention that is the starting point of the design
-- By reducing how much object needs to know about other objects, we lower context and easier to reuse
-- Sender of the message should trust the receiver to behave appropriately without knowing context
-- _ to denote private might be preferable as they supply information about method stability without imposing visibility restrictions
-- LOD prohibits routing message to third object via a second object of different type, only talk to immediate neighbors

### Chapter 5
-- Duck typing detaches public interfaces from specific classes, creating vitual types that are defined by what they do (i.e. what messages they accept) rather than what they are, reveals underlying abstractions.
-- Polymorphism in OOP refers to ability of many different objects to respond to the same message. Receivers of message supply their own specific version of behavior
-- When observer patterns such as kind, is_a, responds_to focus on the code's expectations and use it to find duck type. 
-- When classes being changed are stable e.g. framework/stdlib, 
-- Static: compile time error checking, type checks documented, compiled code faster
-- Dynamic: Interpreted and dynamically loaded code, no compile/make cycle; easier metaprogramming

### Ch 6:  Acquiring Behavior Through Inheritance

-- Inheritance provides automatic message delegation from subclasses to superclasses

— When your problem is one of needing numerous specializations of a stable, common abstraction, inheritance can be an extremely low-cost solution.

— Inheritance solves the problem of highly related types that share common behavior but differ along some dimension

— Creating empty superclass and pushing abstract bits of code up to it can be done carefully without fear of leaving concrete artifacts

— The general rule for refactoring into a new inheritance hierarchy is to arrange code so that you can promote abstractions rather than demote concretions.

— This technique of defining a basic structure in the superclass and sending messages to acquire subclass-specific contributions is known as the template method pattern. Always document template method requirements by implementing matching methods that raise useful errors.

— When a subclass sends super it’s effectively declaring that it knows the algorithm;it depends on this knowledge. If the algorithm changes, then the subclasses may break even if their own specializations are not otherwise affected.

— Abstract superclasses use hook methods to allow inheritors to contribute specializations without being forced to send super, i.e. subclasses don’t have to know the abstract algorithm

— Don't underestimate value of sb who really wants to do



### Ch 7: Sharing Role Behavior with Modules

— When objects that play a common role need to share behavior, they do so via a Ruby module. The code defined in a module can be added to any object, be it an instance of a class, a class itself, or another module.

— Inheritance falls short when subclass requires combining the qualities of two existing superclasses

— Modules in Ruby provides a way to define a named group of methods that are independent of class and can be mixed in to any object, allowing objects of different classes to play a common role using a single set of code

— With modules as well as classical inheritance, if a module sends a message it must provide an implementation, even if to just raise an error indicating users of this module must implement the method

— Inheritance is is-a, modules is behaves-like-a

— The methods of the last included module are encountered first in the lookup path

— First, an object that uses a variable with a name like type or category to determine what message to send to self contains two highly related but slightly different types. Second, when a sending object checks the class of a receiving object to determine what message to send, you have overlooked a duck type.

— Avoid writing code that requires its inheritors to send super; instead use hook messages to allow subclasses to participate while absolving them of responsibility for knowing the abstract algorithm.

— Deep hierarchies of classes introduce long search path for message resolution and large set of built-in dependencies. 

— Liskov Substitution Principle, which in mathematical terms says that a subtype should be substitutable for its super type



### CH 8: Combining Objects with Composition

— In composition, the larger object is connected to its parts via a has-a relationship.

