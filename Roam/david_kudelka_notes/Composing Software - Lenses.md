  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Lenses**
      * **A lens** is a composable pair of pure getter and setter functions which focus on a particular field inside an object, and obey a set of axioms known as **the lens law**. Think of the object as the whole and the field as the part. 
        * **The getter** takes a whole and returns the part of the object that the lens is focused on
        *  **The setter** takes a whole, and a value to set the part to, and returns a new whole with the part updated. Unlike a function which simply sets a value into an object's member field, Lens setters are pure functions
      * Simple examples
        * **Getters**
          * ```javascript
const getX = ([x]) => x;
const getY = ([x, y]) => y;
const getZ = ([x, y, z]) => z;

console.log(
	getZ(10, 10, 100) // 100
)```
        * **Setters**
          * ```javascript
const setY = ([x, _, z]) => y => ([x, y, z])

console.log(
	setY([10, 10, 10])(900) // [10, 900, 10]
)```
      * ## **Why Lenses?**
        * State shape dependencies are a common source of coupling in software. Many components may depend on the shape of some shared state, so if you need to later change the shape of that state, you have to change logic in multiple places
        * If you later need to change the state shape, you can do so in the lens m and none of the code that depends on the lens will need to change
        * This follows the principle that a small change in requirements should require only a small change in the system
      * ## **Lens Laws**
        * The **lens laws** are **algebraic axioms** which ensure that the lens is well behaved
          * view(lens, set(lens, value, store)) = value
            * If you set a value into the store, and immediately view the value through the lens, you get the value that was set.
          * set(lens, b, set(lens, a, store)) = set(lens, b, store)
            * If you set a lens value to 'a' and then immediately set the lens value to 'b', it's the same as if you'd just set the value to 'b'
          * set(lens, view(lens, store), store) = store
            * If you get the lens value from the store, and then immediately set that value back into the store, the value unchanged
        * Those examples are just naive solutions, on production you should always use well tested library like **Rambda**
          * ```javascript
// Functions to view and set, which can be used with
// any lens: 
const view = (lens, store) => lens.view(store)
const set = (lens, value, store) => lens.set(value, store)

// A function which takes a prop, and returns naive
// lens accessors for that prop
const lensProp = prop => ({
  view: store => store[prop],
  // This is very naive, because it only works for objects
  set: (value, store) => ({
    ...store,
    [prop]: value
  })
})

// An example store object. An object you access with a lens
// is often called the "store" object
const fooStore = {
  a: 'foo',
  b: 'bar'
}
const aLens = lensProp('a');
const bLens = lensProp('b');
// Desctructure the 'a' and 'b' props from the lens using
// the view() function
const a = view(aLens, fooStore) // a = 'foo'
const b = view(bLens, fooStore) // b = 'bar'```
      * ## **Composing Lenses**
        * Lenses are composable. When you compose lenses, the resulting lens will dive deep into the object, traversing the full object path. Let's import the more full-featured lensProp form Ramda to demonstrate
        * ```javascript
import {compose, lensProp, view} from 'ramda';

const lensProp = [
  'foo',
  'bar',
  1
];

const lenses = lensProps.map(lensProp);

const truth = compose(...lenses);

const obj = {
  foo: {
    bar: [false, true]
  }
}

console.log(
	view(truth, obj)
);```
        * ### **Over**
          * We can apply a function to the value of focus in lens. The lens map operation is commonly called **"over"** in JavaScript libraries
          * We can create it like this:
            * ```javascript
// over = (lens, f: a => a, store) => store
const over = (lens, f, store) =>
	set(lens, f(view(lens, store)), store);
const uppercase = x => x.toUpperCase();

console.log(
	over(aLens, uppercase, store) // { a: 'FOO', b: 'bar' }
)```
          * Setters mirror the **functor laws**. If you map the identity function over a lens, the store is unchanged
          * Lenses obey as well functor **composition law**. For composition example, we are going to use an autocurried version of over
          * ```javascript
import { curry } from 'ramda'

const over = curry(
	(lens, f, store) => set(lens, f(view(lens, store)), store)
)

const lens = aLens;

const store = {
  a: 20
};

const g = n => n + 1;
const f = n => n * 2;

const a = compose(
	over(lens, f)
  	over(lens, g)
)

const b = over(lens, compose(f, g));

console.log(
	a(store) // {a: '42'}
  	b(store) // {a: '42'}
)```
      * ## **Action Points**
        * [ ] Edward Kmett has spoken a lot on the topic