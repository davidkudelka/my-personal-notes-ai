  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Pure Functions**
      * **What is a Function?**
        * It is a process that takes some input and produces some output
        * **Purposes of function**:
          * **Mapping** - produce some output based on given inputs. A function maps input values to output values
          * **Procedures** - A function may be called to perform a sequence of steps. The sequence is known as a procedure, and programming in this style is known as procedural programming
          * **I/O** - Some functions exist to communicate with other parts of the system, such as the screen, storage, system logs, or network
        * **Pure functions** are all about the mapping, they map input arguments and return values, meaning that for each set of inputs, there exist an output.
        * Pure functions are same as functions in algebra
          * f(x) = 2x
          * This is definition of function in algebra
          * f(2) in this case means the same as I would write 4, this is called **referential transparency** (notice that there are no side effects, so it doesn't matter if I write f(2) or 4)
          * The same thing is in JavaScript, the function just can't contain any side-effects (writing to disk, logging, and so on), because then **referential transparency** is not valid, because you can't exchange the function call for value without changing the meaning
        * ## **Pure Functions**
          * Pure function is function which?
            * Given the same input, will always return the same output
            * Produces no side effects
          * They are the very essential building blocks of functional programming, (KISS - Keep It Simple, Stupid)
          * The fact that they are immune from shared state and mutations they are very easily to move, refactor and they can make your code more flexible and adaptable to future changes
          * **The trouble with Shared State**
            * Imagine auto suggestion input that every time user types something, it calls API for auto suggestions based on user's input.
            * Because different request can take different times, it can happen that bugs occur (past request is slower than newer and it updates shared state so, you have for newer input past request values)
            * "Non-determinism = paralel processing + mutable state" - [[Martin Odersky]]
          * **Same Input, Same Output**
            * Function is only pure if given the same input, it will always produce the same output.
            * A pure function must not rely on any external mutable state, because it would no longer be deterministic or referentially transparent
          * **No Side Effects**
            * A pure function produces no side effects, which means that it can't alter any external state
            * **Immutability**
              * One of the key aspects of the pure functions, so you avoid mutation of the shared state
              * One of the problem can be passing object as arguments, then adjusting properties of the object and returning the same object.
      * **Conclusion**
        * **Pure functions are the simplest kind of function**. You should prefer them whenever they are practical. They are deterministic, which makes them easy to understand, debug, and test. Determinism also makes them immune to entire classes of bugs dealing with shared mutable state, side-effects, race conditions, and so on.
        * An expression is **referentially transparent** if you can replace the expression with its corresponding value without changing the meaning of the program
        * **Pure functions** can be used to optimise software performance. For instance, rendering a view is often an expensive operation, which can be skipped if the data underlying the view has not changed. When pure functions are used for view state updates, you can check to see whether or not a view should be re-rendered by comparing the previous state to the new state.