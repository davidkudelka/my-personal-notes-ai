  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Factory Functions**
      * A **factory function** is any function which is not a **class** or **constructor** that returns (presumably new) object. In JavaScript, any function can return an object. When it does so without the new keyword, it's a factory function.
      * Handy facts about object in JavaScript
        * ```javascript
const user = {
  userName: 'echo',
  avatar: 'echo.png'
}

// Accessing by key
const key = 'avatar';
console.log( user[key] ) // "echo.png"

const userName = 'echo';
const avatar = 'echo.png';

// Omiting keys
const user = {
  userName,
  avatar
}
console.log(user) // { "avatar": "echo.png", "userName": "echo" }

const userName = 'echo';
const avatar = 'echo.png';

const user = {
  userName,
  avatar,
  setUserName (userName) {
    this.userName = userName;
    return this;
  }
}

console.log(user.setUserName('Foo').userName); // "Foo"```
        * You can access objects properties by 'this', if it is called by method inside the object
      * ## **Factory Function for User Objects**
        * ```javascript
const createUser = ({userName, avatar}) => ({
  userName,
  avatar,
  setUserName (userName) {
    this.userName = userName;
    return this;
  }
})```
        * ### **Destructuring**
          * `const createUser = ({userName, avatar}) => ({`
          * Function takes object as an argument, but we are destructuring those 2 values from input object
          * We can destructure even **arrays**
            * `const swap = ([first, second]) => [second, first];`
            * You can use there as well **rest operator** to collect all other values
              * `const rotate = ([first, ...rest]) => [...rest, first];`
        * ### **Computed Property Keys**
          * ```javascript
const arrToObj = ([key, value]) => ({ [key]: value });
console.log(arrToObj(['foo', 'bar'])); // {"foo": "bar"}```
        * ### **Default Parameters**
          * Benefits of default parameters
            * Users are able to omit parameters with suitable defaults
            * The function is more self-documenting because default values supply examples of expected input
            * IDE's and static analysis tools can use default values to infer the type expected for the parameter. For example, a default value of 1 implies that the parameter can take a member of the Number type
          * ```javascript
const createUser = ({
  userName = 'Anonymous',
  avatar = 'anon.png'
} = {}) => ({
  userName,
  avatar
});```
          * What's very **important** there is = { } after destructuring, this allow us to call createUser() with no arguments. If we wouldn't supply = { } with no argument when calling the function it would throw error (it would try to destructure undefined)
      * ## **Type Inference**
        * What is it?
          * Type interference is the process of inferring types based on the context in which they are used. In JavaScript, it is a very good alternative to type annotations
          * Visual Studio Code with Typescript does this automatically, so it is basically those hints from figuring out what types of things you code with are
            * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/UlyBSbwFoX.png]]
        * It **doesn't always** make sense to restrict a parameter to a fixed type (that would make generic functions and higher order functions difficult), but when it does make sense, default parameters are often the best way to do it, even if you're using TypeScript or Flow
    * ## **Conclusion**
      * Start with the simplest implementation, and move to more complex implementations only as required