  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Curry and Function Composition**
      * ### **What is a curried function?**
        * A **curried function** is a function that take multiple arguments one at a time.
        * ```javascript
const add = a => b => a + b

const result = add(2)(3); // => 5```
        * To get result we must apply **both functions** with double parentheses invocation
        * The add function takes one argument, and then returns a **partial application** of itself with a variable **fixed** in the closure scope. A **closure** is a function bundled with its lexical scope. Closures are created at runtime during function creation. **Fixed** means that the variables are assigned values in the closure's bundled scope
      * ### **What is partial application?**
        * A partial application is a function which has been applied to some, but not yet all of its arguments.
        * In other words, it's a function which has some arguments fixed inside it's closure
      * ### **What's the Difference partial (application vs curried function)?**
        * **Partial Applications** can take as many or as few arguments at a time, but **curried functions** always return **unary function**: a function which takes one argument
        * The **unary requirement** for curried functions is an important feature
      * ### **What is point-free style?**
        * **Point-free style** is a style of programming where function definitions do not make reference to the function's arguments
        * ```javascript
const add = a => b => a + b

const inc = add(1);

inc(3)```
        * You are assigning function without defining function, you can't use function keyword as well as const foo = () => {} and etc. (You can't reference arguments)
      * ### **Why do we curry?**
        * Curried functions are particularly useful in the context of **function composition**
        * Example of compose function
          * ```javascript
const compose = 
      (...fns) => x => fns.reduceRight((y, f) => f(y), x)

const g = n => n + 1;
const f = n => n * 2;

const h = compose(f, g);

h(20);```
        * We use currying to define function that abstracts the iteration over the arguments and passing the value down the stream
      * ### **Trace**
        * The point-free style creates very concise, readable code, but it can come at the cost of easy debugging, that's why trace function comes really handy.
        * ```javascript
const trace = label => value => {
  console.log(`${ label }: ${ value }`);
  return value;
}```
      * ### **Curry and Function Composition, Together**
        * The key is that curried function takes **one argument at a time**. The reason that curried functions are so convenient for function composition is that key transform functions which expect multiple parameters into functions which can take a single argument, **allowing them to fit in a function composition pipeline.** Take the trace() function as an example
        * You also need to ensure that the function is expecting parameters in the correct order to specialise them
        * **Data last** - which means that you should take the specialised parameters first, and take the data the function will act on last. 