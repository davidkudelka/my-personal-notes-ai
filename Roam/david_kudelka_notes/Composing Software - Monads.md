  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Monads**
      * Functions can compose: a => b => c becomes a => c
      * Functors can compose functions with context: given F(a) and two functions, a => b => c, return F(c)
      * Monads can compose type lifting functions: a => M(b), b => M(c) becomes a => M(c)
      * ## **Explanation of Terms**
        * **Map** - means "apply a function to an 'a' and return a 'b'". Given some input, return some output. The functor map operation does that inside the context of a container called functor data type, which returns a new container with the results.
        * **Context** - is the computational detail of the monad. The functor or monad supplies some computation to be performed during the mapping process, such as iterating over a list of things, or waiting for a future value to resolve.
        * **Type Lift** - means to lift a type into a context, wrapping values inside a data type that supplies the computational context a => M(a)
        * **Flatten** - can be used to unwrap an extra layer of context that might be added by applying a type lifting function using a functor map operation. If you map a function of type a => M(b) with the functor map operation, it will return a value of type M(M(b)). Flatten unwraps the extra layer of context: M(M(b)) => M(b). Monads are not required to directly expose a flatten operation. It happens automatically inside flatMap
        * **FlatMap** - is the opretaion taht defines a monad. It combines map and flatten into a single operation used to compose type lifting functions (a => M(b))
    * ```javascript
const echo = n => x => Array.from({ length: n }).fill(x);

console.log(
	[1, 2, 3].map( echo(3) )
  	// [[1, 1, 1, 2, 2, 2, 3, 3, 3]]
);

console.log(
	[1, 2, 3].flatMap( echo(3) )
  	// [1, 1, 1, 2, 2, 2, 3, 3, 3]
);```
    *  Example of asynchronous monads
    * ```javascript
// This is compose enriched of flatMap argument to deal with
// different types of monads
const composeMonands = flatMap => (...ms) => (
	ms.reduce((f, g) => x => g(x)[flatMap](f))
);

const composePromises = composeMonads('then');

const getUserById = id => id === 3 ?
	Promise.resolve({ name: 'Kurt', role: 'Author' }) :
	undefined
;

const hasPermission = ({ role }) => (
	Promise.resolve(role === 'Author')
);

const authUser = composePromises(hasPermission, getUserById);

authUser(3).then(trace(label)); // true```
    * ## **What Monads are Made of**
      * A monad is based on a simple symmetry
        * **of** - A type lift a => M(a)
        * **map** - The application of a function a => M(b) inside the monad context, which yields M(M(b))
        * **flatten** - The unwrapping of one layer of monadic context: M(M(b)) => M(b)
      * Combine **map** with **flatten**, and you get **flatMap**
        * Function composition for monad-lifting functions, aka Kleisli composition
      * ```javascript
const Monad = value => ({
  flatMap: f => f(value),
  map (f) {
    return this.flatMap(a => Monad.of(f(a)))
  }
});
Monad.of = x => Monad(x);

Monad(21).map(x => x * 2).map(x => console.log(x))```
      * The flattening process (without the map in .flatMap()) is usually called flatten() or join(). Frequently (but not always), flatten()/join() is omitted completely, because it's built into .flatMap(). Flattening is often associated with composition so it's frequently combined with mapping. Remember, unwrapping + map are both needed to compose a => M(a) functions
      * ### **Identity monad**
        * Depending on what kind of monad you are dealing with , the unwrapping process could be extremely simple. In the case of the identity monad, .flatMap() is just like map(), except that you don't lift the resulting value back into the monad context. That has the effect of discarding one layer of wrapping
        * ```javascript
const Id = value => ({
  // Functor mapping
  // Preserve the wrapping for .map() by
  // passing the mapped value into the type
  // list:
  map: f => Id.of(f(value)),
  
  // Monad flatMap
  // Discard one level of wrapping
  // by omitting the .of() type lift:
  flatMap: f => f(value),
  
  // Just convenient way how to inspect values
 toString: () => `Id(${ value })`
})```
    * ## **Building a Kleisli Composition Function**
      * Monads can rely on values that depend on previous asynchronous or branching actions in the composition chain. In those cases, you can't get a simple value out for simple function compositions. Your monad-returning actions take the form a => Monad(b) instead of a => b
      * Example
        * ```javascript
const composePromises = (...ms) => (
	ms.reduce((f, g) => x => g(x).then(f))
);
// Step by step
// 1. b, a => [ b, a ].reduce((null, b) => x => b(x).then(null))
// 2. [b, a].reduce(x => b(x).then(null), a) 
// 				 => x => a(x).then(x => b(x).then(null))
// 3. x => a(x).then(x => b(x).then(null))


const a = n => Promise.resolve(n + 1);
const b = n => Promise.resolve(n * 2);

const h = composePromises(b, a)

// 20 => a(20).then(21 => b(21).then(x => console.log(42)))
h(20).then(x => console.log(x)) // 42
```
        * .then() is an unwrapping process that goes from Promise(b) => b. That operation is called **flatten** (aka join)
        * You can see the composePromises is good use case for higher order function, lets use **curried function** and to construct **flatMap**
          * ```javascript
const composeM = method => (...ms) => (
	ms.reduce((f, g) => x => g(x)[method](f))
);

// Now we can write the specialized implementations
const composePromises = composeM('then');
const composeMap = composeM('map');
const composeFlatMap = composeM('flatMap');```
    * ## **The Monad Laws**
      * There are 3 laws that all monads should satisfy
        * ### **Left and right identity laws**
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/pH2zKtLiNG.png]]
          * Note - of = type lift, f function
          * Left identity: of then f = f
          * Right identity: f then of = f
          * It is similar to the functors law and it is no coincidence, both obey category laws. 
          * **Definition** - A monad is a functor. A functor is a morphism between two category objects, A => B. The morphism is represented by an arrow between objects. In addition to the arrow we explicitly see between objects, each object in category also has an arrow back to itself. In other words, for every object A in a category, there exists an arrow A => A. That arrow is known as identity arrow. It's frequently drawn as an arrow that loops back to the origin object
        * ### **Associativity law**
          * ( f then g ) then h = f then (g then h)
          * of(x).flatMap(f).flatMap(g) = of(x).flatMap(x => f(x).flatMap(g))
    * ## **Conclusion**
      * **Functors** are things you can **map** over, **Monads** are things you can **flatMap** over
        * Functions can compose a => b => c becomes a => c
        * Functors can compose functions with context: given F(a) and two functions, a => b => c, return F(c)
        * Monads can compose type lifting functions: a => M(b), b => M(c) becomes a => M(c)
      * A monad is based on a simple symmetry - A way to wrap a value into a context, and a way to access the value in context
        * **Lift / Unit** - A type lift from some type into the monad context: a => M(a)
        * **Flatten / Join** - Unwrapping the type from the context: M(c) => c - is usually the result of mapping a => M(b)m so M(c) => c is usually M(M(b)) => M(b). The purpose of flatten is to discard the extra layer of wrapping
      * **Monads** are also functors. So they can map
        * **Map**: Map with context preserved: M(a) => M(b)
      * Combine **flatten** with **map** and you get **flatMap** - function composition for lifting functions, aka Kleisli composition
      * **Monads must satisfy 3 laws (axioms)**, collectively known as the monad laws
        * Left identity: unit(x).flatMap(f) ==== f(x)
        * Right identity: m.flatMap(unit) ==== m
        * Associativity: m.flatMap(f).flatMap(g) ==== m.flatMap(x => f(x).flatMap(g))
      * Examples of monads you might encounter in every day JavaScript code include promises and observables. Kleisli composition allows you to compose your data flow logic without worrying about the particulars fo the data type's API, and without worrying about the possible side-effects, conditional branching, or other details of the unwrapping computations hidden in the flatMap() operation
      * This makes monads a very powerful tool to simplify your code. You don't have to understand or worry about what's going on inside monads to reap the simplifying benefits that monads can provide, but now that you know more about what's under the hood, taking a peek under the hood isn't such a scary prospect