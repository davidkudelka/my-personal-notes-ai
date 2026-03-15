  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Abstraction & Composition**
      * Abstraction let us run on autopilot, safely. All software is automation. Given enough time, anything you do on a computer, you could do with paper, ink, and carrier pigeons. Software just takes care of all the little details that would be too time consuming to do manually
      * ## **Abstraction is simplification**
        * "Simplicity is about substracting the obvious and adding the meaningful" - [[John Maeda]] #quote
        * ### **2 main components**
          * **Generalisation** - is the process of finding similarities (the obvious) in repeated patterns, and hiding the similarities behind an abstraction
          *  **Specialisation** - is the process of using the abstraction, supplying only what is different (the meaningful) for each use case
        * ### **Abstraction in Software**
          * Abstractions in software?
            * Algorithms
            * Data structures
            * Modules
            * Classes
            * Frameworks
          * Functions make great abstractions because they possess the properties that are essential for a good abstraction
            * **Identity** - The ability to assign a name to it and reuse it in different contexts
            * **Composable** - The ability to compose simple functions to form more complex functions
        * ### **Abstraction through composition**
          * In math, a function given the same inputs will always return the same output
            * f: A -> B
            * Given some inout A, a function f will produce B as output. You could say that f defines a relationship between A and B
          * Example
            * f: A -> B
            * g: B -> C
            * h: A -> C
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/lmY2zzAow6.png]]
          * Good abstractions simplify by hiding structure, the same way h reduces A -> B -> C down to A -> C 
        * ### **How to Do More with Less Code**
          * Abstraction is the key to doing more with less code.
          * When you create abstractions, you should be deliberate about it, and you should be aware of the good abstractions that have already been made available to you (such as the always useful map, filter, and reduce)
          * **Characteristics of good abstractions**
            * Composable
            * Reusable
            * Independent
            * Concise
            * Simple
        * ### **Reduce**
          * **Reduce** (aka: fold, accumulate) utility commonly used in functional programming that lets you iterate over a list, applying a function to an accumulated value and the next item in the list, until the iteration is complete and the accumulated value gets returned.
          * Many useful things can be implemented with reduce. Frequently, it's the most elegant way to do any non-trivial processing on a collection of items
          * **Reduce is Versatile**
            * You can use to create map, filter and etc.
            * But mainly you can use reduce to implement **compose** for you functions
              * ```javascript
const compose = (...fns) => 
	x => fns.reduceRight((v, f) => f(v), x)```
            * and as well pipe, which is better for sequence of events
              * ```javascript
const pipe = (...fns) =>
	fns.reduce((v, f) => f(v), x)```
          * Reduce is the most versatile and useful tool you will in JavaScript