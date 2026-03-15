  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Object Composition**
      * One of the most common mistakes in software development is the tendency to overuse class inheritance. Because it forms **is-a relations**. The tightest coupling
        * The fragile base class problem
        * The gorilla / banana problem
        * The duplication by necessity problem
      * ## **What is Object Composition?**
        * "In computer science, a composite data type or compound data type is any data type which can be constructed in a program using the programming languages primitive data types and other composite types"
        * Favor object composition over class inheritance
        * The big difference between object composition and class inheritance is in relations, some programmers without knowing create system where everything is dependent on each other and program becomes a dense mass that's hard to learn, port, and maintain
      * ## **Three Different Forms of Object Composition**
        * There are 3 fundamental techniques of object composition
          * ### **Aggregation**
            * When an object is formed from an enumerable collection of sub-objects. In other words, an object which contains other objects. Each sub-object retains its own reference identity, such that it could be destructured from the aggregation without information loss
            * **Examples**
              * Arrays
              * Maps
              * Sets
              * Graphs
              * Trees (DOM nodes, UI Components)
            * **When to use**
              * Whenever there are collections of objects which need to share common operations, such as iterables, stacks, queues
            * **Consideration**
              * Aggregations are great for applying universal abstractions, such as applying a function to each member of an aggregate (e.g. array.map(fn)). If there are potentially hundreds of thousands or millions of sub-objects, however, stream processing or delegation may be more efficient
            * **In code**
              * ```javascript
const objs = [
  { a: 'a', b: 'ab' },
  { b: 'b' },
  { c: 'c', b: 'cb' }
]

const collection = (a, b) => a.concat([b])

const a = objs.reduce(collection, []);```
          * ### **Concatenation**
            * When an object is formed by adding new properties to an existing objects, e.g. JQuery plugins are created by concatenating new methods to the jQuery delegate prototype, jQuery.fn.
            * **Examples**
              * Plugins are added to jQuery.fn via concatenation
              * State reducers (e.g. Redux)
              * Functional mixins
            * **When to use**
              * Any time it would be useful to progressively assemble data structures at runtime e.g. merging JSON objects, hydrating application state from multiple sources, creating updates to immutable state (by merging previous state with new data) etc...
            * **Considerations**
              * Be careful mutating existing objects. Shared mutable state is a recipe for many bugs.
              * It's possible to mimic class hierarchies and **is-a relations** with concatenation. The same problems apply. Think in terms of composing small, independent objects, rather than inheritance
              * Beware of implicit inter-component dependencies
              * Property name collisions are resolved by concatenation order: last-in wins. This is useful for defaults/overrides behaviour, but can be problematic if the order shouldn't matter
            * **In code**
              * ```javascript
const concatenate = (a, o) => ({...a, ...o});

const c = objs,reduce(concatenate, {});```
          * ### **Delegation**
            * **Delegation** is when an object forwards or delegates to another object
            * **Examples**
              * JavaScripts built-in types use delegation to forward built-in method calls up the prototype chain e.g., [].map() delegates to Array.prototype.map(), obj.hasOwnProperty() delegates to Object.prototype.hasOwnProperty() and so on
              * Photoshop uses delegates called 'smart objects' to refer to images and resources defined in separate files. Changes to the object that smart objects refer to are reflected in all instances of the smart object
            * **When to use**
              * **Converse memory** - Any time there may be potentially many instances of an object and it would be useful to share identical properties or methods among each instance which would otherwise require allocating more memory
              * **Dynamically update many instances** - Any time many instances of an object need to share identical state which may need to be updated dynamically and changes instantaneously reflected in every instance, e.g., Sketchpad's "masters" or Photoshop's 'smart objects'
            * **Considerations**
              * Delegation can be used to exactly mimic the behaviour and limitations of class inheritance. In fact, class inheritance in JavaScript is built on top of static delegates via the prototype delegation chain. Avoid **is-a** thinking

            * **In Code**
              * ```javascript
const delegate = (a, b) 
	=> Object.assign(Object.create(a), b);

const d = objs.reduceRight(delegate, {});```
    * # **Conclusion**
      * These are not the only three kinds of object composition. It's also possible to form loose, dynamic relationships between objets through acquaintance/association relationships where objects are passed as parameters to other objects (dependency injection), and so on.
      * Look for ways to compose where a small change to program requirements would require only a small change to the code implementation. Express your intention clearly and concisely, and remember: If you think you need class inheritance, chances are very good that there's a better way to do it.