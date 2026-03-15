  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Functors & Categories**
      * A **functor data type** is something you can map over
      * The JavaScript array .map() method is a good example of a functor, but many other kinds of objects can be mapped over as well, including promises, streams, trees, objects, etc.
      * ## **Why Functors**
        * The details of the underlying data structure implementation are abstracted away. It doesn't matter how the map is working under the hood, we can just use it
        * Functors hide the types of the data they act on. Instead you pass function that deals with them
        * Functors allow you to easily compose functions over the data inside
      * With functors you have to write less code, less code = less surface for bugs = less bugs
      * ## **Functor Laws**
        * There are 2 main laws
          * **Identity**
            * For all objects 'A' in category 'C', there must be an identity arrow that maps back to the same object, represented as 'idA', or '1a'
            * If you pass the identity function (x => x) into a .map(), where 'a' is any functor type, the result should be equivalent to 'a' 
            * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/uIAsOsab6h.png]]
          * **Composition**
            * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/9DKOc2DxdE.png]]
            * ```javascript
const g = n => n + 1;
const f = n => n * 2;
const mappable = [20];

const a = mappable.map(g).map(f);
const b = mappable.map(x => f(g(x)));

console.log(a.toString() === b.toString()) // true```
            * Functors must obey the composition law a.map(g).map(f) is equivalent to a.map(x => f(g(x)))
      * ### **Category Theory**
        * A **category** is a collection of objects and arrows between objects (where "object" can mean just about anything). Objects are like types in programming, meaning that they usually represent sets of things with one or more elements
        * Arrows are known as **morphism**. Morphisms map between two objects 'A' and 'B', connecting them with arrow 'f'. They're often represented in diagrams as 'A' -> 'B' (where -> is 'f')
        * All objects must have identity arrows, which are arrows pointing back to the same object, e.g. A -> A (where -> is 'idA'). The identity arrow can also be represented as 'idA': A -> A or '1a': A -> A
        * For any group of connected objects, A -> B -> C, there must be a composition which goes directly from A -> C
        * All morphism are equivalent to compositions, e.g. given objects 'A','B' and an arrow 'f' between them 'idB' o f = f = f o 'idA'
        * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/AaE2jGxflX.png]]
      * ### **Build Your Own Functor**
        * Example
          * ```javascript
const Identity = value => ({
  map: fn => Identity(fn(value))
});```
          * Identity satisfies the functor laws, lets look at proof
            * ```javascript
// trace() is a utility to let you easily inspect
// the contents

const trace = x => {
  console.log(x);
  return x
}

const u = Identity(2);

// Identity law
const r1 = u; 				// Identity(2)
const r2 = u.map(x => x); 	// Identity(2)
r1.map(trace); // 2
r2.map(trace); // 2

const f = n => n + 1;
const g = n => n * 2;

// Composition law
const r3 = u.map(x => f(g(x)));	// Identity(5)
const r4 = u.map(g).map(f);		// Identity(5)
r3.map(trace) // 5
r4.map(trace) // 5```
      * ### **Curried Map**
        * ```javascript
const Identity = value => ({
  map: fn => Identity(fn(value))
});

const map = curry((fn, mappable) => mappable.map(fn));
const log = x => console.log(x);

const double = n => n * 2;
const mdouble = map(double);

mdouble(Identity(4)).map(log); 	// 8
mdouble([4]).map(log);			// 8```
    * ## **Conclusion**
      * **Functor data types are data types you can map over.** You can think of them as containers which can apply functions to the contents inside, which will return a new container with results.
      * In category theory, **a functor is a structure preserving map from category to category**, where "structure preserving" means that the relationships between objects and morphisms are retained.
      * A **category** is a collection of objects and arrows between objects. Arrows represent morphisms, which we can roughly think of as functions inside code. Each object in a category has an identity morphism A -> A (where -> is 'idA'). For any chain of objects A -> B -> C there exists a composition A -> C
      * Functors are great higher-order abstractions that allow you compose functions over the contents of a container without coupling those functions to the strucutre or implementation details of the functor data type. Functors form the foundation of other very useful algebraic structures, such as monads. 