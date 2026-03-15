  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Functional Mixins**
      * **Functional mixins** are composable factory functions which connect together in a pipeline, each function adding some properties or behaviours like workers on an assembly line.
      * **Features** of **functional mixins** 
        * Data privacy/encapsulation
        * Inheriting private state
        * Inheriting from multiple sources
        * No diamond problem (property collision ambiguity) - last in wins
        * No base-class requirement
      * ## **Motivation**
        * What **issues** **class inheritance** brings?
          * **The tight coupling problem** - Because child classes are dependent on the implementation of the parent class, class inheritance is the tightest coupling available in object oriented design
          * **The fragile base class problem** - Due to tight coupling, changes to the base class can potentially break a large number of descendant classes - potentially in code managed by third parties. The author could break code they're not aware of
          * **The inflexible hierarchy problem** - With single ancestor taxonomies, given enough time and evolution, all class taxonomies are eventually wrong for new use-cases
          * **The duplication by necessity problem** - Due to inflexible hierarchies, new use cases are often implemented by duplication, rather than extension, leading to similar classes which are unexpectedly divergent. Once duplication sets in, it's not obvious which class new classes should descent from, or why.
          * **The gorilla/banana problem** - the problem with object-oriented languages is they've got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding banana and the entire jungle
        * If an admin is an employee, how do you handle a situation where you hire an outside consultant to perform administrative duties temporarily? If you knew every requirement in advance, perhaps class inheritance could work, but I've never seen that happen. Given enough usage, applications and requirements inevitably grow and evolve over time as new problems and more efficient processes are discovered. Mixins offer a more flexible approach
      * ## **What are mixins?**
        *  **Mixins** are a form of object composition, where component features get mixed into a composite object so that properties of each mixin become properties of the composite object. Because JavaScript supports dynamic object extension and objects without classes, using object mixins is trivially easy.
        * Example
          * ```javascript
const chocolate = {
  hasChocolate: () => true
};
const caramelSwirl = {
  hasCaramelSwirl: () => true
};
const pecans = {
  hasPecans: () => true
}

const iceCream = 
      Object.assign({}, chocolate, caramelSwirl, pecans)

console.log(`
  	hasChocolate: ${ iceCream.hasChocolate() } 
	hasCaramelSwirl: ${ iceCream.hasCaramelSwirl() } 
	hasPecans: ${ iceCream.hasPecans() }
`);```
        * ### **What is functional inheritance?**
          * **Functional inheritance** is the process of inheriting features by applying an augmenting function to an object instance. The function supplies a closure scope which you can use to keep some data private. The augmenting function uses dynamic object extension to extend the object instance with new properties and methods
            * ```javascript
function base(spec) {
  var that = {};
  that.name = spec.name;
  return that;
}

function child(spec) {
  var that = base(spec);
  that.sayHello = function() {
    return 'Hello, I\'m' + that.name
  }
  return that;
}

var result = child({ name: 'a functional object' });

console.log(result.sayHello()) // 'Hello, Iam a functional object'```
            * Because child() is tightly coupled to base(), when you add grandchild(), greatGrandchild(), etc..., you'll opt into most of the common problems from class inheritance
        * ### **What is functional mixin?**
          * **Functional mixins** are composable functions which mix new properties or behaviours into existing objects. Functional mixins don't depend on or require a base factory or constructor: Simply pass any arbitrary object into mixin, and it will be extended
            * ```javascript
const flying = o => {
  let isFlying = false;
  
  return Object.assign({}, o, {
    fly () {
      isFlying = true;
      return this;
    },
    isFlying: () => isFlying,
    land () {
      isFlying = false;
      return this;
    }
  })
}
const bird = flying({});
console.log( bird.isFlying() ); // false
console.log( bird.fly().isFlying() ); // true

```
          * **Composing Functional Mixins**
            * As you can see we can compose them with usage of normal functional tools
            * ```javascript
import pipe from 'lodash/fp/flow';

const quacking = 
   	quack => o => 
		Object.assign({}, o , { quack: () => quack });

const createDuck = quack => pipe(
	flying,
  	quacking(quack)
)({})

const duck = createDuck('Quack!');

console.log(duck.fly().quack());```
      * ## **When to Use Functional Mixins**
        * You should always use the simplest possible abstraction to solve the problem you're working on. Start with pure function. If you need an object with persistent state, try a factory function. If you need to build more complex objects, try functional mixins.
        * Good use-cases for functional mixins
          * Application state management, e.g. something similar to a Redux store
          * Certain cross-cutting concerns and services, e.g. a centralized logger
          * Composable functional data types, e.g., the JavaScript Array type implements **Semigroup**, **Functor**, **Foldable**... Some algebraic structures can be derived in terms of other algebraic structures, meaning that certain derivations can be composed into a new data type without customization
      * ## **Caveats**
        * It is possible to faithfully reproduce all of the features and problems of class inheritance using functional mixins
        * You can **avoid** that, using following advice:
          * Favor pure functions -> factories -> functional mixins -> classes
          * Avoid creation of is-a relationships between objects, mixins, or data types
          * Avoid implicit dependencies between mixins - wherever possible, functional mixins should be self-contained, and have no knowledge of other mixins
          * "Functional mixins" doesn't mean "functional programming"
          * There may be side-effects when you access a property using Object.assign() or object spread syntax({...object}). You'll also skip any non-enumerable properties. ES2017 added Object.getOwnPropertyDescriptors() to get around this problem
        * ### **Classes**
          * Class inheritance is very rarely (perhaps never) the best approach in JavaScript, but that choice is sometimes made by a library or framework that you don't control. In that case, using class is sometimes practical, provided by library:
            * Does not require you to extend your own classes (i.e., does not require you to build multi-level class hierarchies)
            * Does not require you to directly use the new keyword - in other words, the framework handle instantiation for you
          * **Class performance**
            * In some browsers, classes may provide JavaScript engine optimizations that are not available otherwise. But we are talking about small tiny difference, object still have (millions of ops/sec)
            * Unless you measured a significant bottleneck that you can provably and substantially reduce using class, you should optimize for clean, flexible code instead of worrying about performance
      * ## **Functional Mixins & Functional Programming**
        * Functional mixins are commonly used in OOP and can contain side-effects.
        * When creating them always use Object.assign or {...a, ...b} spread operator so you are not mutating object passed as an argument
      * ## **Conclusion**
        * Be aware, "functional mixins" doesn't imply "functional programming" - it simply means, "mixins using functions". Functional mixins can be written using a functional programming, avoiding side-effects and preserving referential transparency, but that is not guaranteed. There may be side-effects and nondeterminism.
          * Unlike simple object mixins, functional mixins support true data privacy (encapsulation), including the ability to inherit private data.
          * Unlike single-ancestor class inheritance, functional mixins also support the ability to inherit from many ancestors, similar to class decorators, traits, or multiple inheritance
          * Unlike multiple inheritance in C++, the diamond problem is rarely problematic in JavaScript, because there is a simple rule when collisions arise: The last mixin added wins
          * Unlike class decorators, traits, or multiple inheritance, no base class required
        * Favor the simplest implementation over more complex constructions
          * Pure function -> factory functions -> functional mixins, classes 