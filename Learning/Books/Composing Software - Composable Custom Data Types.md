  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Composable Custom Data Type**
      * In JavaScript, the easiest way to compose is function composition, and function is just an object you can add methods to. In other words, you can do this:
        * ```javascript
const t = value => {
  const fn = () => value;
  
  fn.toString = () => `t(${ value })`;
  
  return fn
}

const someValue = t(3);

console.log(
	someValue.toString() // "t(2)"
)```
      * We can compose functions of the same type, lets do it in 3 simple steps
        * Change the fn function into an add function that returns t(value + n) where n is the passed argument
        * Add a valueOf() method to the t type so that the new add() function can take instances of t() as arguments. The + operator will use the result of n.valueOf() as the second operand.
        * Assign the methods to the add() function with Object.assign()
      * When you put it together it looks like this
        * ```javascript
const t = value => {
  const add = n => t(value + n);
  
  return Object.assign(add, {
    toString: () => `t(${ value })`,
    valueOf: () => value
  })
}```
        * This fulfil the **Identity law** and **Associativity law**
      * Now you can compose values 
        * ```javascript
const pipe = (...fns) => x => fns.reduce((y, f) => f(y), x);

const add = (...fns) => pipe(...fns)(t(0))

const sum = add(
	t(2),
  	t(4),
  	t(-1)
);

console.log(sum.toString()) // t(5)```
      * ## **You can do this with any type**
        * It doesn't matter what shape your data takes, as long as there is some composition operation that makes sense. For strings or lists, it could be concatenation
        * The question is, which operation best represents the concept of composition ? In other words, which operation would benefit most expressed like this?
        * ### **Composable Currency**
          * Moneysafe is an open source library that implements this style of composable functional datatypes. JavaScript's Number type can't accurately represent certain fractions of dollars
            * `.1 + .2 = .3 // false`
          * Examples
            * ```javascript
import { $ } from 'moneysafe';

$(.1) + $(.2) === $(.3).cents; // true

// The ledger syntax takes advantage of the fact that
// Moneysafe lifts values into composable functions.
// It exposes a simple function composition utility called
// ledger

import { $ } from 'moneysafe'
import { 
  $$, 
  subtractPercent, 
  addPercent 
} from 'moneysafe/ledger'

$$(
	$(40),
	$(60),
  	subtractPercent(20),
  	addPercent(10)
).$ // 88```
            * The returned value is a value of the lifted money type. It exposes the convenient .$ getter which converts the internal floating-points cents value into dollars, rounded to the nearest cent
            * The result is an intuitive interface for performing ledger-style money calculations