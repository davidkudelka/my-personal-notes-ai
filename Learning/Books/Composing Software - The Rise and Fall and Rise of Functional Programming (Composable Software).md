  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **The Rise and Fall and Rise of Functional Programming (Composable Software)**
      * There were 2 main ways **Turing machine** and **Lambda calculus** for any computation
      * [ ] Discover more about those 2 and what is actually the difference
      * There are three important points that make lambda calculus special:
        * Functions are always anonymous, the right side of const sum = ( x , y ) => x + y 
        * Function are always unary, meaning they only accept one argument at the time, when you want to provide more arguments, you have to return another function which accepts another argument, this goes on until you collect all the arguments and function can be calculated.
          * (x, y) => x + y is translated into (x) => (y) => x = y, this is called **currying**
        * Functions are first class, meaning that functions can be used as inputs to other functions and functions can return functions
        * ```javascript
const compose = (f,g) => x => f(g(x))

const double = n => n * 2
const increment = n => n + 1

const transform = compose(double, increment)

transform(3) // 8```