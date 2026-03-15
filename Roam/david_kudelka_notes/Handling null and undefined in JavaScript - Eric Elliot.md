  * tags: #engineering #articles #[[Unit Tests]] 
  * Author: [[Eric Elliot]]
  * Rating: 
  * Finished: [[2020-10-15]]
  * Notes:
    * **Sources of null or undefined values**
      * User input
      * Database / Network records
      * Uninitialised state
      * Functions which could return nothing
    * **User Input**
      * Validation is good thing to avoid those
    * **Hydrating Records from Input**
      * Every time it is good to use default values for arguments of function (if the function expect async data)
      * So it never happens to you that for example if you are displaying balance, you do not display 0 value before the data loads
    * **Avoid creating null and undefined values**
      * Never create null value on your own, state machines are usually better
      * You can use chaining to avoid erros
      * **Nullish Coalescing Operator**
        * It is an expresion that if the value on the left is null or undefined use value on the right
        * `baz ?? 'default baz'`
      * **Asynchronous Either with Promises**
        * If function may not return with a value, it might be a good idea to wrap it in an Either. It is something that split return into 2 possible results. It is basically Promise in javascript 
        * ```javascript
const exists = x => x != null;
const ifExists = value => exists(value) ?
  Promise.resolve(value) :
  Promise.reject(`Invalid value: ${ value }`);

// Invalid value: null
ifExists(null).then(log).catch(log); 
// hello
ifExists('hello').then(log).catch(log); ```
      *  **Arrays for Maybes**
        * Basically if you are using native JavaScripts map it doesn't run on empty array and you can take advantage of this
        * There is as well example of Maybe function which basically encapsulates optional value and if the value is null or undefined it uses the optional value