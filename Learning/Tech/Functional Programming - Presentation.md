  * # What is functional programming?
    * Functional programming (often abbreviated FP) is a programming paradigm where applications are composed using pure functions, avoiding shared mutable state and side-effects.
    * Functional programming is usually more declarative than imperative, meaning that we express what to do rather than how to do it.
    * ## What is software composition?
      * Software composition is the way we compose software together and we can do it either consciously or not
        * Just because you don’t know about software composition you are not avoiding it, you are just doing it badly
      * You have 2 basic ways how to write your code and it is either imperative or declarative
        * **Imperative** - **HOW** programs spend lines of code describing the specific steps used to achieve results - the flow control - how to do things
          * TOP to BOTTOM, it is way how you think
          * Typical example of imperative style is for loop
          * Usually utilise **statements**
            * for, if, switch, throw, etc...
        * **Declarative** - **WHAT** program abstract the flow control process (the how gets abstracted away), and instead spend lines of code describing the dat a flow (what to do)
          * Avoid using word abstraction

          * What is important to notice is that by doing this you are separating writing logic and composition of this logic to from each other, giving you more room to actually better think about composition of your programs
          * Usually utilise expressions
            * 2*2, doubleMap([2,3,4]), Math.max(4,3,2)
        * **Functional Programming**
          * **Functional programming** is a programming paradigm where applications are composed using pure functions, avoiding shared mutable state and side-effects. Functional programming is usually more declarative than imperative, meaning that we express what to do rather than how to do it
          * Most important features for functional programming
            * **First class functions** - function is a value, you can pass it as arguments or return it, allows for higher order functions, currying and composition
            * **Anonymous functions and concise lambda syntax** - makes it easier to work with higher order functions
            * **Closures** - closure are created at function creation time, when a function is defined inside another function, it has access to the variable bindings in the outer function, even after the outer function exits
            * What is JavaScript missing from functional programming features

          * Core parts of functional programming
            * Pure functions
              * Given the same inputs, always returns the same output
              * Has no side-effects
              * Referential transparency
            * Function composition
              * The process of combining two or more functions in order to produce a new function or perform some computation
            * Shared state
              * The problem with shared state is that in order to understand the effects of a function, you have to know the entire history of every shared variable that the function uses or affects
              * As well the order of functions that are called upon this state matters as well
```javascript
// Shared state
const x = {
  val: 2
}

// Mutates shared state
const x1 = () => x.val += 1;

// Mutates shared state
const x2 = () => x.val *= 2;

x1()
x2()

console.log(x.val) // 6

x.val = 2 // Reseting back to 2

x2()
x1()

console.log(x.val) // 5```
              * When you avoid shared state, the timing and order of functions calls don't change the result of calling the function. With pure functions, given the same input, you'll always get same output. This makes function calls completely independent of other function calls, which can radically simplify changes and refactoring. A change in one function, or the timing of a function call won't ripple out and break other parts of the program
              * Remove function call timing dependency, and you eliminate an entire class of potential bugs
            * Immutability
              * Immutability is a central concept of functional programming because without it, the data flow in your program is lossy. State history is abandoned, and strange bugs can creep into your software
              * const doesn't mean immutable, object properties can still be changes
              * Object.freeze({}) doesn't mean immutable, because if there is nested object, that object can still be changed
              * Functional programming languages uses data structures called Tries, which has structural sharing, which leads to sharing the same unchanged state between 2 objects
              * Check out - Immutable.js and Mori libraries
            * Side effects
              * It includes
                * Modifying any external variable or object property(e.g. global variable, or a variable in the parent function scope chain)
                * Logging to the console
                * Writing to the screen
                * Writing to a file
                * Writing to the network
                * Triggering any external process
                * Calling any other functions with side-effects
            * Reusability through higher order functions
              * A **higher order function** is any function which takes a function as an argument, returns function, or both. Higher order functions are often used to:
                * Abstract or isolate actions, effects, or async flow control using callback functions, promises, monads, etc.
                * Create utilities which can act on a wide variety of data types
                * Partially apply a function to its arguments or create a curried function for the purpose of reuse or function composition
                * Take a list of functions and return some composition of those input functions
            * Containers, functors, lists and streams
              * A **functor data structure** is a data structure that can be mapped over. In other words, it's a container which has an interface which can be used to apply a function to the values inside it. When you see the word functor, you should think "mappable"
              * The same functor function can be applied to data streams, because "A list expressed over time is a stream"
  * # Why is it important?
    * Functional programming and therefore declarative paradigm strives for reusability - less code = less surface for bugs
    * **Advantages**
      * **Working memory** - idea of less variables means less things to remember, so we code is then much more readable
      * **Signal to Noise Ratio** - more concise code expression leads to enhanced comprehension
      * **Surface Area for Bugs** - extra code means extra surface for bugs
      * **Small change in requirements = small change in code** - no tight coupling, nothing inherits from each other and we are able to adjust more things without worrying about changing functionality of other parts of code
      * **Much easier to achieve test coverage**
        * You are separating easy logic from hard logic (easy = code, hard = side effects)
        * You can as well test those from each other, good thing is that we most of the time use other libraries to create side effects so most of the time testing is not even necessary
      * **Helps you to better think about composition**
        * Support declarative style of programming, which separates composition from logic
        * We separate side effects and pure functions, but most of the time side effects are the most important part of our application and this allows us to pay more attention to them
    * Why is functional programming important for start-ups?
      * Most of the time we face situations where we are not 100% sure what the final product is going to be and we need to be prepared for pivots
      * Other developers need to work on the same code we wrote, declarative code is much more concise and it is easier to grasp flow of the data
      * Allow us to test just certain parts of the code so we don’t have to care about 100% test coverage, instead we can focus more on testing core functionality of our business
  * # Object oriented programming
    * What is essential to it
      *  **Encapsulating state** - by isolating other objects from local state changes. The only way to affect another object's state is to ask (not command) that object to change it by sending a message. State changes are controlled at a local, cellular level rather than exposed to shared access
      * **Decoupling objects from each other** - the message sender is only loosely coupled to the message receiver, through the messaging API
      * **Runtime adaptability** - via late binding. Runtime adaptability provides many great benefits that [[Alan Kay]] considered essential to OOP
      * Features
        * Classes
        * Class inheritance
        * Special treatment for objects/functions/data
        * The new keyword
        * Polymorphism
        * Static Types
        * Recognizing a class as a "type"
    * Problems of class inheritance
      * **The tight coupling problem** - Because child classes are dependent on the implementation of the parent class, class inheritance is the tightest coupling available in object oriented design
      * **The fragile base class problem** - Due to tight coupling, changes to the base class can potentially break a large number of descendant classes - potentially in code managed by third parties. The author could break code they are not aware of
      * **The inflexible hierarchy problem** - With single ancestor taxonomies, given enough time and evolution, all class taxonomies are eventually wrong for new use-casses
      * **The Duplication by necessity problem** - Due to inflexible hierarchies, new use cases are often implemented by duplication, after this it is hard to tell from which class new things should be created, since you have very similar classes
      * **The gorilla/banana problem** - it just brings all the other things that are not really necessary for your use case, you want gorilla, but you will get gorilla with banana and the whole jungle
  * # Why isn’t functional programming the norm?
    * Reasons
      * **Other popularity factors**
        * Job market - we have this big project in object oriented language and you have to work with it
        * Community - support by community
      * **Quick upgrade**
        * Benefits
        * Familiarity
        * Learning Curve - (I don't know what category theory is, what is monad ? this is the difficulties we face)
        * Code migrations effort - Typescript - it is basically javascript plus something, it is easy to start
          * You can just take javascript file rename it to .ts and that's it, you can slowly start and making it better slowly
      * Platform exclusivity
        * **Object C and Swift** - it is build for iOS and for this reason it doesn't matter how good they are
        * **JavaScript** - the same thing, just the platform makes it popular and not really the programming language itself
        * **C#** - Windows exclusivity
      * No Killer apps for FP languages
        * rails for ruby
        * drupal for wordpress
        * systems programming for C
    * ## Answer why isn't a norm
      * No sufficient large "killer apps"
      * No exclusivity on large platforms
      * Can't be a quick upgrade if substantially different
      * No epic marketing budgets
      * Slow & steady growth takes decades
    * ## We can see larger and larger support of FP 
      * Kotlin has both OO and FP, you can use both
      * Swift included functional programming patterns
      * JavaScript has some support of functional patterns as well
      * And those supports are growing
      * Maybe JavaScript, Swift, Kotlin being hybrid and this is just transition between those 2 styles, but who knows how soon this can happen
  * Feedback
    * [ ] Start with question
    * [ ] Ask more questions during presentation
    * [ ] More examples