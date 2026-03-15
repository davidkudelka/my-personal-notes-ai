  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Higher Order Functions**
      * A **higher order function** is a function that takes a function as an argument, or returns a function.
      * Example
        * ```javascript
const censor = words => {
  const filtered = [];
  for(let i = 0, { length } = words; i < length; i++) {
    const word = words[i];
    if(word.length !== 4) filtered.push(word);
  }
  return filtered;
}```
        * As you can see this function contains a lot of things that can be abstracted, and for that we will use **higher order functions**. It is especially useful because by abstraction you can get rid off obvious and keep just the important
      * Abstract Reducing
        * ```javascript
const reduce = (reducer, initial, arr) => {
  // shared stuff
  let acc = initial;
  for(let i = 0, {length} = arr; i < length; i++) {
    // unique stuff in reducer call (this is the unique condition)
    acc = reducer(acc, arr[i]);
  }
  return acc;
}```
      * Abstract Filtering
        * ```javascript
const filter = (
  // fn is predicate function (condition of filter)
  fn, arr
) => reduce(
  // in reducer take new value, apply filter function, if it is true
  // add into the array of results
  (acc, curr) => fn(curr) ? acc.concat([curr]) : acc, 
  // [] - initial value, arr - array to loop over
  [], arr
)```
      * Result
        * ```javascript
const censor = words => filter(
	word => word.length !== 4,
  	words
)```
      * JavaScript is doing some abstraction already for us, Array.prototype already contains all those important methods