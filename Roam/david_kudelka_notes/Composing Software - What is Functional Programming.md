  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **What is Functional Programming**
      * **Functional programming** is a programming paradigm where applications are composed using pure functions, avoiding shared mutable state and side-effects. Functional programming is usually more declarative than imperative, meaning that we express what to do rather than how to do it
      * Before you start, we need to understand those core concepts
        * **Pure Functions**
          * Given the same inputs, always returns the same output
          * Has no side-effects
          * Referential transparency
        * **Function Composition**
          * The process of combining two or more functions in order to produce a new function or perform some computation
        * **Shared State**
          * The problem with a shared state is that in order to understand the effects of a function, you have to know the entire history of every shared variable that the function uses or affects
          * As well the order of functions that are called upon this state matters as well
            * ```javascript
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
        * **Immutability**
          * Immutability is a central concept of functional programming because without it, the data flow in your program is lossy. State history is abandoned, and strange bugs can creep into your software
          * const doesn't mean immutable, object properties can still be changes
          * Object.freeze({}) doesn't mean immutable, because if there is nested object, that object can still be changed
          * Functional programming languages uses data structures called Tries, which has structural sharing, which leads to sharing the same unchanged state between 2 objects
          * Check out - Immutable.js and Mori libraries
        * **Side Effects**
          * It includes
            * Modifying any external variable or object property(e.g. global variable, or a variable in the parent function scope chain)
            * Logging to the console
            * Writing to the screen
            * Writing to a file
            * Writing to the network
            * Triggering any external process
            * Calling any other functions with side-effects
        * **Reusability Through Higher Order Functions**
          * A **higher order function** is any function which takes a function as an argument, returns function, or both. Higher order functions are often used to:
            * Abstract or isolate actions, effects, or async flow control using callback functions, promises, monads, etc.
            * Create utilities which can act on a wide variety of data types
            * Partially apply a function to its arguments or create a curried function for the purpose of reuse or function composition
            * Take a list of functions and return some composition of those input functions
        * **Containers, Functors, Lists, and Streams**
          * A **functor data structure** is a data structure that can be mapped over. In other words, it's a container which has an interface which can be used to apply a function to the values inside it. When you see the word functor, you should think "mappable"
          * The same functor function can be applied to data streams, because "A list expressed over time is a stream"
        * **Declarative vs Imperative**
          * **Imperative** - programs spend lines of code describing the specific steps used to achieve the desired results - the flow control: How to do things
            * ```javascript
const doubleMap = mumbers => {
  const double = [];
  for (let i = 0; i < numbers.length; i++) {
    double.push(numbers[i] * 2);
  }
  return double;
}```
          * **Declarative** - programs abstract the flow control process (the how gets abstracted away), and instead spend lines of code describing the data flow: What to do
            * ```javascript
const doubleMap = numbers => numbers.map(n => n * 2);```
          * Imperative code frequently utilizes **statements**
            * for, if, switch, throw, etc.
          * Declarative code relies more on **expression**
            * 2 * 2, doubleMap([2,3,4]), Math.max(4,3,2), 'a' + 'b' + 'c', {...a, ...b, ...c}
      * ## **Conclusion**
        * **Pure functions** over shared state and side effects
        * **Immutability** over mutable data
        * **Function composition** over imperative flow control
        * **Generic** utilities that act on many data types over object methods that only operate on their colocated data
        * **Declarative** over imperative code (what to do, rather than how to do it)
        * **Expressions** over statements