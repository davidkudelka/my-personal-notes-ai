  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Why Learn Functional Programming in JavaScript**
      * JavaScript has the most important features needed for functional programming
        * **First class functions** - function is a value, you can pass it as arguments or return it, allows for higher order functions, currying and composition
        * **Anonymous functions and concise lambda syntax** - makes it easier to work with higher order functions
        * **Closures** - closure are created at function creation time, when a function is defined inside another function, it has access to the variable bindings in the outer function, even after the outer function exits
      * What JavaScript is Missing?
        * JavaScript is a multi-paradigm language (it supports imperative, object-oriented, and functional programming). The disadvantage is that almost everything needs to be mutable
        * **Mutation** is a change to data structure that happens in-place
          * ```javascript
cosnt foo = {
  bar: 'baz'
}

foo.bar = 'qux' // mutation```
        * Features that JavaScript is Missing
          * **Purity** - You have to program using just pure functions, side-effects are not allowed. In some FP languages, purity is enforced
          * **Immutability** - Some FP languages disable mutations. Instead of mutating, you are creating new array or object. (This might sounds inefficient, but most of them are using trie data structures under the hood, which feature structural sharing, meaning that old object and new object share references to the data that is the same)
            * Immutable.js and Mori - good libraries for enforcing immutability in JavaScript
            * We have const in JavaScript, but you can still change values in object
            * We have freeze() to freeze object values, but you can still change properties in nested objects
          * **Recursion** - it is the ability for a function to reference itself for purpose of iteration, you can do this in JavaScript, but it does not fully support **proper tail calls** (a feature that allows recursive functions to reuse stack frames for recursive calls ), for long recursions you get a stack overflow error
        * The true strength of JavaScript is **diversity of thought and users** in the ecosystem