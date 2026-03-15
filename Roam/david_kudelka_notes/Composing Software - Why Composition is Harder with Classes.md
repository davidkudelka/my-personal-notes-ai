  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Why Composition is Harder with Classes**
      * What does **new** keyword actually do?
        * Creates a new object and binds this to it in constructor function
        * Implicitly returns this, unless you explicitly return another object
        * Sets the instance [[Prototype]], instance.*proto* to Constructor.prototype, so that Object.getPrototypeOf(instance) === Constructor.prototype and instance.*proto* === Constructor.prototype
        * Sets the instance.constructor === Constructor
      * ## **The Delegate Prototype**
        * Delegating prototype link is good for memory optimization , but if you do not need to optimize
        * istanceof can lie to you
          * ```javascript
class User {
  constructor ({userName, avatar}) {
    this.userName = userName;
    this.avatar = avatar;
  }
}

const currentUser = new User({
  userName: 'Foo',
  avatar: 'foo.png'
})

User.prototype = {}

console.log(
	currentUser instanceof User, // <-- false -- Oops!
  	// But it clearly has the correct shape:
  	// { avatar: 'foo.png', userName: 'Foo' }
  	currentUser
)```
          * This behaviour is forbidden in V8 Chrome but Babel will accept altering prototype link, which is the **worse** because it is **inconsistent**
          * More common problem is that JavaScript has multiple execution contexts, called realms - memory sandboxes where the same code will access different physical memory locations.  If you have constructor in parent frame and one iframe they will point to different location in memory and instanceof will fail again
          * Another problem is its nominal type check rather than a structural type check, which means that if you start with a class and later switch a factory, all the calling code using instanceof won't understand new implementations even if they satisfy the same interface contract.
          * Don't use instanceof and it won't lie to you
      * ## **The .constructor Property**
        * In theory **.constructor** could be useful to make generic functions which are capable of returning a new instance of whatever object you pass in
        * There is an issue with constructor, lets imagine creating new instance of data type
          * ```javascript
const empty = ({ constructor } = {}) => constructor ?
      	new constructor() :
		undefined;

const foo = [10];
console.log(empty(foo)) // [] - here it works fine

// But lets try promise
const prom = Promise.resolve(10);

console.log(empty(prom)) 
// [TypeError: Promise resolver undefined is not a function]```
          * We can see that issue here is in a **new** keyword
          * What is JavaScript missing is a united way how to do this, there exist in JavaScript static method on any factory or constructor called **.of()**, but **.off()** is not supported by most of the data types (strings, numbers, objects, maps, weak maps or sets)
          * Adding support for **.constructor** and **.of()** to a factory
            * ```javascript
const createUser = ({
  userName = 'Anonymous',
  avatar = 'anon.png'
} = {}) => ({
  userName,
  avatar,
  constructor: createUser
});
createUser.of = createUser;

// You can make .constructor non-enumerable by adding to
// the delegate prototype

const createUser = ({
  userName = 'Anonymous',
  avatar = 'anon.png'
} = {}) => ({
  *proto*: {
    constructor: createUser
  },
  userName,
  avatar
})```
      * ## **Class to Factory is a Breaking Change**
        * Factories allow increased flexibility because they
          * Decouple instantiation details from calling code
          * Allow you to return arbitrary objects - for instance, to use an object pool to tame the garbage collector
          * Don't pretend to provide any type guarantees, so callers are less tempted to use intanceof and other unreliable type checking measures, which might break code across execution contexts, or if you witch to an abstract factory
          * Can dynamically swap implementations for abstract factories. e.g., a media player that swaps out the .play() method for different media types
          * Adding capability with composition is easier with factories
        * While it's possible to accomplish most of these goals using classes, it's easier to do so with factories. There are fewer potential bug pitfalls, less complexity to juggle, and a lot less code
        * Due to the fact that **new** changes the behaviour of a function being called, changing from a class or constructor to a factory function is a potentially breaking change.
          * Refactoring from a class to an arrow function factory might seem to work with a compiler, but if the code compiles the factory to a native arrow function, your app will break, because you can't use **new** with arrow functions
          * What can exactly cause the breaking changes
            * Absence of the **[[Prototype]]** link from factory instances will break caller intanceof checks
            * Absence of the **.constructor** property from factory instances could break code that relies on it
            * Callers using **new** could begin to throw errors or experience unexpected behaviour after switching to a factory
      * ## **Code that Required new Violates the Open/Closed Principle**
        * Our APIs should be **open** to extension, but **closed** to breaking changes. Since a common extension to a class is to turn it into a more flexible factory, but that refactor is a breaking change, code that requires the **new**   keyword is **closed** to extension and **open** to breaking changes. That's the opposite what we want
          * Export a **factory** instead of class
      * ## **The class Keyword and extends**
        *   The class keyword is supposed to be a nicer syntax for object creation patterns in JavaScript, but it falls short in several ways
          * ### **Friendly Syntax**
            * The primary purpose of class was to provide a friendly syntax to mimic class from other languages in JavaScript
            * **The question we should ask ourselves though is, does JavaScript really need to mimic class from other languages?**
            * Start with object literals, if you need to create more instances of it use factories as next step
            * Comparison
              * ```javascript
class User {
  constructor ({userName, avatar}) {
    this.userName = userName;
    this.avatar = avatar;
  }
}

const currentUsr = new User({
  userName: 'Foo',
  avatar: 'foo.png'
})

// Versus

const createUser = ({ userName, avatar }) => ({
  userName,
  avatar
})

const currentUser = createUser({
  userName: 'Foo',
  avatar: 'foo.png'
})```
          * ### **Performance and Memory**
            * class offers two kinds of performance optimizations: shared memory for properties stored on the delegate prototype, and property lookup optimizations
              * You can have delegate even on factories
              * property lookup optimizations are microoptimizations
            * In the context of applications, we should avoid premature optimization, and focus our efforts only where they will make a large impact, For most applications,  that means our network calls and payloads, animations, asset caching strategies, etc.
            * Instead, you should optimize code for maintenance and flexibility
          * ### **Type Checking**
            * Classes in JavaScript are dynamic, and instanceof checks don't work across execution contexts, so type checking based on class is a non-starter. It's unreliable. It's likely to cause bugs and make your application unnecessarily rigid
          * ### **Class Inheritance with extends**
            * extends introduces well-known issues
              * Tight coupling
              * Inflexible hierarchies
              * Gorilla/Banana problem
              * Duplication by necessity
        * ## **Classes are OK if You're Careful**
          * Recommendations
            * **Avoid instanceof** - it lies because JavaScript is dynamic and has multiple execution contexts, and instanceof fails in both situations. It can also cause problems if you switch to an abstract factory down the road
            * **Avoid extends** - don't extend a single hierarchy more than once. "Favor object composition over class inheritance"
            * **Avoid exporting your class** - Use class internally for performance gains, but export a factory that creates instances in order to discourage users from extending your class and avoid forcing callers to use new
            * **Avoid new** - Try to avoid using it directly whenever it makes sense, and don't force your callers to use it. (Export a factory, instead)
          * It is ok to use class if
            * **You are building UI components for a framework like React or Angular** - Both frameworks wrap your component classes into factories and manage instantiation for you, so you don't have to use new in your own code
            * **You never inherit from your own classes or components** - Instead, try object composition, function composition, higher order functions, or modules - all of them are better code reuse patterns than class inheritance
            * **You need to optimize performance** - Just remember to export a factory so callers don't have to use new and don't get lured into the extends trap
          * In most other situations, factories gonna serve you better
