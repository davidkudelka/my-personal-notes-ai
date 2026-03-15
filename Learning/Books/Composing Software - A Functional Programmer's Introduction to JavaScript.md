  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **A Functional Programmer's Introduction to JavaScript**
      * **Expressions and Values**
        * An **expression** is a chunk of code that evaluates to a value
        * The value of an expression can be given a name
        * Examples:
          * ```javascript
7;

7 + 1; // 8

7 * 2; // 14

'Hello'; // Hello

const hello = 'Hello';
hello; // Hello```
      * **var, let, and const**
        *  **const** - set value at declaration time, it helps you fully understand what the name means right away, without needing to read the whole function or block scope
        * var, let, and const - more strict declaration is better
      * **Types**
        * There are as well booleans, objects and arrays
        * **Objects** - you can use **object spread operator** for better object composition
          * ```javascript
const a = {
  a: 'a'
}
const b = {
  b: 'b'
}
const c = {
  ...a,
  ...b,
} // { a: 'a', b: 'b' }```
        * **Destructuring** -  both arrays and object supports this
          * ```javascript
const [t, u] = ['a', 'b']
t; // 'a'
u; // 'b'
const blep = {
  blop: 'blop'
}
cosnt {blop} = blep;
blop; // 'blop'```
        * **Default Parameter Values**
          * ```javascript
const orZero = (n = 0) => n```
          * It helps with documentation
        * **Named Arguments**
          * ```javascript
const createUser = ({
  name = 'Anonymous',
  avatarThumbnail = '/avatars/anonymous.png'
}) => ({
  name,
  avatarThumbnail
})```
        * **Rest and Spread**
          * ```javascript
// Rest operator
const aTail = (head, ...tail) => tail

// Spread opreator
const array = [1,2,3]
const newArray = [...array, 4] // [1,2,3,4]```
        * **Currying**
          * A **curried function** is a function that take multiple parameters one at a time
          * ```javascript
const gte = cutoff => n => n >= cutoff```
          * Lodash has autocurry function
        * **Arrrays**
          * Arrays have some built-in methods. A **method** is a function associated with an object: usually a property of the associated object
          * ```javascript
const arr = [1,2,3]
arr.map(double) // [2,4,6]

// Note that the original arr value is unchanged
arr; // [1,2,3]```
        * **Method Chaining**
          * You can call method on the returned value without needing to refer to the return value by name
          * ```javascript
const arr = [1,2,3]
arr.map(double).map(double); // [4,8,12]

const gte = cutoff => n => n  >= cutoff
[2,4,6].filter(gte(4)); // [8,12]```
          * gte is a **predicate** function. Function that returns a boolean value