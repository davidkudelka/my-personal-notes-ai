  * tags:
  * Book: [[Composing Software - Eric Elliot]]
  * Notes:
    * # **Composing Software: An Introduction**
      * Just because you don't know about software composition you are not avoiding it, you are just doing it badly
      * The process of software development is breaking down large problems into smaller problems, building components that solve those smaller problems, then composing those components together to form a complete application
      * **Function composition** - is the process of applying a function to the output of another function
        * Basically all we do is composing software and if we do it intentionally, we will do it better
        * **Advantages** - with composing functions you gonna get rid of intermediary variables, that's called point free style (return of one function is argument of another function) - [[Composing Software - functional x imperative]]
          * **Working memory** - idea of less variables means less things to remember, so we code is then much more readable
          * **Signal to Noise Ratio** - more concise code expression leads to enhanced comprehension
          * **Surface Area for Bugs** - extra code means extra surface for bugs
      * ## **Composing Obejcts**
        * "Favor object composition over class inheritance" - [[The Gang of Four]]
        * There are 2 general types of data
          * **Primitive Types** - int, string, boolean ...
          * **Composite Types** - data composed from primitive data types, this can be object in JavaScript
        * Any time you are building any non-primitive data structure, you are performing some kind of object composition
        * 3 types of composition: delegation, aggregation, acquaintance
        * Problems of class inheritance
          * **The tight coupling problem** - Because child classes are dependent on the implementation of the parent class, class inheritance is the tightest coupling available in object oriented design
          * **The fragile base class problem** - Due to tight coupling, changes to the base class can potentially break a large number of descendant classes - potentially in code managed by third parties. The author could break code they are not aware of
          * **The inflexible hierarchy problem** - With single ancestor taxonomies, given enough time and evolution, all class taxonomies are eventually wrong for new use-casses
          * **The Duplication by necessity problem** - Due to inflexible hierarchies, new use cases are often implemented by duplication, after this it is hard to tell from which class new things should be created, since you have very similar classes
          * **The gorilla/banana problem** - it just brings all the other things that are not really necessary for your use case, you want gorilla, but you will get gorilla with banana and the whole jungle
        * The most common form of object composition is **object concatenation** aka **mixin composition**
          * ```javascript
const a = {
  a: 'a'
};

const b = {
  b: 'b'
};

const c = { ...a, ...b } // {a: 'a', b: 'b'}```
        * What should you know ?
          * There is more than one way to do object composition
          * Some ways are better than others
          * Tou want to select the simplest, most flexible solution for the task at hand