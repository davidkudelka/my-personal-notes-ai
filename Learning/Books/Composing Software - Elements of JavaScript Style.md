  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Elements of JavaScript Style**
      * List of **elements of style**
        * Make the function the unit of composition. One job for each function
        * Omit needless code
        * Use Active Voice
        * Avoid a succession of loose statements
        * Keep related code together
        * Put statements and expressions in positive form
        * Use parallel code for parallel concepts
      * ### **1. Make the function the unit of composition. One job for each function**
        * There are 3 types of functions
          * **Communicating functions** - Functions which perform I/O
          * **Procedural functions** - A list of instructions, grouped together
          * **Mapping functions** - Given some input, return some corresponding output
        * If you function is for I/O, don't mix that I/O with mapping (calculation). If your function is for mapping, don't mix it with I/O. By definition, procedural functions violate this guideline. 
        * Procedural functions also violate another guideline: Avoid a succession of loose statements
        * The ideal function is simple, deterministic, pure function
          * Given the same input, always return the same output
          * No side-effects
      * ### **2. Omit needless code** 
        * Less code = less syntax noise = stronger signal for meaning transmission
        * ```javascript
function secret (message) {
  return function () {
    return message;
  }
};
// Can be reduced to
const secret = msg => () => msg;```
        * **Omit needless variables**
          * You should omit variables created only to name return values. **The name of your function** should provide adequate information about what the function will return. Consider following
            * ```javascript
const getFullName = ({firstName, lastName}) => {
  const fullName = firstName + ' ' + lastName;
  return fullName;
}
// vs...
const getFullName = ({firstName, lastName}) => (
	firstName + ' ' + lastName
);```
          * Another way how to reduce variables is **point-free style**
            * ```javascript
const add2 = a => b => a + b;
// Now we can define a point-free inc()
// that adds 1 to any number
const inc = add2(1);

inc(3); // 4```
          * When you compose 2 functions together, you eliminate the need to create a variable to hold the intermediary value between the two function applications
            * ```javascript
const g = n => n + 1;
const f = n => n * 2;

const incThenDoublePoints = n => {
  const incremented = g(n);
  return f(incremented)
}
incThenDoublePoints(20); // 42

// vs...
// compose2 - Take two functions and return their composition
const compose2 = (f, g) => x => f(g(x));
// Point-free
const incThenDoublePointFree = compose(f, g);
incThenDoublePointFree(20); // 42```
        *  You can do the same thing with any **functor**
          * ```javascript
const compose2 = (f, g) => x => [x].map(g).map(f).pop()

const incThenDoublePointFree = compose2(f, g);
incThenDoublePointFree(20); // 42```
        * Virtually every functional programming library has at least two versions of **compose utilities**
          * compose - right to left
          * pipe - left to right
          * ```javascript
import pipe from 'lodash/fp/flow';
pipe(g, f)(20); // 42

// or you can just use this
const pipe = 
      (...fns) => x => fns.reduce((acc, fn) => fn(acc), x);
pipe(g, f)(20); // 42```
        * **Remember**
          * If you can say the same thing with less code, without changing or obfuscating the meaning, you should
          * If you can say the same thing with fewer variables, without changing or obfuscating the meaning, you should
      * ### **3. Use Active Voice**
        * Name things as directly as possible
        * Name predicates and booleans as if they are yes or no questions
          * isActive(user) is better than getActiveStatus(user)
          * isFirstRun = false; is better than firstRun = false;
        * Name functions using verb form
          * increment() is better than plusOne()
          * unzip() is better than filesFromZip()
          * filter(isActive, array) is better than activeItemsFromArray(isActive, array)
        * **Event Handlers**
          * Event handlers and lifecycle methods are exception, they express when to do it so the naming should be "<when to act>, <verb>
            * element.onClick(handleClick) is better than element.click(handleClick)
              * In the second one, it looks like we are trying to trigger the event, instead of respond to it
        * **Lifecycle Methods**
          * component.beforeUpdate(doSomething) is better than component.beforeComponentUpdate(doSomething)
          * It is good to name **functional mixins** with adjectives
            * `const duck = comoseMixins(flying, quacking)`
      * ### **4. Avoid a Succession of loose statements**
        * Separating code into multiple events helps with easier testing and reusability
      * ### **5. Keep related code together**
        * When you group files together by feature, you avoid scrolling up and down in your file list to find all the files you need to edit to get a single feature working
        * Colocate files related by feature
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/lZub_TZ4Vf.png]]
      * ### **6. Put Statements and expressions in positive form**
        * **isFlying** is better than **isNotFlying**
        * **late** is better than **notOnTime**
        * **If statements**
          * ```javascript
if (err) return reject(err)

// do something

// IS BETTER THAN

if(!err) {
  // ... do something
} else {
  return reject(err)
}```
        * **Ternaries**
          * ```javascript
{
  [Symbol.iterator]: iterator ? iterator : defaultIterator
}

// is better than

{
  [Symbol.iterator]: (!iterator) ? defaultIterator : iterator
}```
        * **Prefer strong negative statements**
          * Sometimes we only care about a variable if it's missing
          * Using positive name would force us to negate it with the ! operator
          * In those cases prefer a strong negative form
            * **if ( missingValue )** is better than **if ( !hasValue )**
            * **if ( anonymous )** is better than **if ( !user )**
            * **if ( isEmpty(thing) )** is better than **if (notDefined(thing))**
        * **Avoid null and undefined arguments in function calls**
          * ```javascript
const createEvent = ({
  title = 'Untitled',
  timeStamp = Date.now(),
  description = ''
}) => ({ title, description, timeStamp });

// later

const birthdayParty = createEvent({
  title: 'Birthday party',
  description: 'Best pary ever!'
})

// IS BETTER THAN

const createEvent = (
  title = 'Untitled',
  timeStamp = Date.now(),
  description = ''
) => ({ title, description, timeStamp });

const birthdayParty = createEvent(
  'Birthday party',
  undefined // This was avoidable
  'Best pary ever!'
)```
      * ### **7. Use parallel code for parallel concepts**
        * There are few problems in applications that have not been solved before. We end up doing the same things over and over again. When that happens, it's an opportunity for abstraction. Identify the parts that are the same, and build an abstraction that allows you to supply only the parts that are different. This is exactly what frameworks do for us
        * For those familiar with components, it's pretty easy to see how each component works; There is some declarative markup expressing the UI elements, event handlers for hooking up behaviours, and lifecycle hooks for attaching callbacks that will run when we need them to
        * When we repeat similar pattern for similar problems, anybody familiar with the pattern should be able to quickly learn what the code does
      * ### **Conclusion**
        *  Given that concise code is
          * Less bug prone
          * Easier to debug
        * And given that bugs
          * Are extremely expensive to fix
          * Tend to cause more bugs
          * Interrupt the flow of normal feature development
        * And given that concise code is also
          * Easier to write
          * Easier to read
          * Easier to maintain
        * It is **worth investing** in fluency with concise syntax, currying & composition
        * Code should be **simple** not **simplistic**