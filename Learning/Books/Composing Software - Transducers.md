  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Transducers**
      * A **transducer** is a composable **higher order reducer**. It takes a reducer as input, and returns another reducer.
      * **Transducers** are
        * Composable using simple function composition
        * Efficient for large collections of infinite streams: Only enumerates over the signal once, regardless of the number of operations in the pipeline
        * Able to transduce over any enumerable source (e.g. arrays, trees, streams, graphs, etc...)
        * Usable for either lazy or eager evaluation with no changes to the transducer pipeline
      * ### What is the difference between **transducers** and **reducers** ?
        * **Reducers** fold multiple inputs into single outputs, where "fold" can be replaced with virtually any binary operation that produces single output, such as
          * ```javascript
// Sums: (1, 2) = 3
const add = (a, c) => a + c;```
        * **Transducers** do much the same thing. but unlike ordinary reducers, transducers are composable using normal function composition
        * Normal reducers can't compose, because they expect two arguments, and only return a single output value, so you can't simply connect the output to the input of the next reducer in series
        * **Transducers** accept reducer and return reducer
      * ## **Why Transducers**
        * Example
          * ```javascript
const friends = [
	{ id: 1, name: 'Sting', nearMe: true },
	{ id: 2, name: 'Radiohead', nearMe: true },
	{ id: 3, name: 'NIN', nearMe: false },
	{ id: 4, name: 'Echo', nearMe: true },
	{ id: 5, name: 'Zeppelin', nearMe: false }
];

const isNearMe = ({ nearMe }) => nearMe;
const getName = ({ name }) => name;

const results = friends
	.filter(isNearMe)
	.map(getName)```
          * There are potential problems in this implementation
            * This only works for arrays. What about potentially infinite streams of data coming in form a network subscription, or a social graph with friends-of-friends
            * Each time you use the dot chaining syntax on an array, JavaScript builds up a whole new intermediate array before moving onto the next operation in the chain. If you have a list of 2,000,000 "friends" to wade through, that could slow down things down by an order of magnitude or two. With transducers you can stream each friend through the complete pipeline without building up intermediate collections between them, saving lots of time and memory churn
            * With dot chaining, you have to build different implementations of standard operations, like .filter(), .map(), .reduce(), .concat(), and so on. The array methods are built into JavaScript, but what if you want to build a custom data type and support a bunch of standard operations without writing them all from scratch? Transducers can potentially work with any transport data type: Write an operator once, use it anywhere that supports transduers
      * ## **Background and Etymology**
        * Transducers are basically transformations of transformation
        * They were critical in data flow processing, we started thinking about data in terms of stream instead of processing arrays of array
      * ## **A Musical Analogy for Transducers**
        * When you are recording music the signal flow might looks something like this. Imagine the arrows are wires between transducers
          * [Source] -> [Mic] -> [Filter] -> [Mixer] -> [Recording]
        * In more general terms, you could express it
          * [Enumerator] -> [Transducer] -> [Transducer] -> [Accumulator]
        * If you want to work with data in an **array**, the downside of it is that you have to enumerate through the whole array each step to complete this
          * ```javascript
const result = arr.
	.filter(isEven)
	.map(double)
// is equal to
const tempResult = arr.filter(isEven);
const result = tempResult.map(double);```
        * The alternative is to flow a value directly from the filtered output to the mapping transformation without creating and iterating over a new, temporary array in between. Flowing the values through one at a time removes the need to iterate over the same collection for each stage in the transducing process,, and transducers can signal stop at any time, meaning you don't need to enumerate each stage deeper over the collection than required to produce desired values
          * There are 2 ways to do that
            * **Pull** - lazy evaluation
            * **Push** - eager evaluation
        * **Transducers** don't care whether you pull or push. Transducers have no awareness of the data structure they are acting on. They simply call the reducer you pass into them to accumulate new values
        * **Transducers** are **higher-order reducers**: Reducer functions that take a reducer and return a new reducer. Rick Hickey describes transducers as **process transformation**, meaning that as opposed to simply changing the values flowing through transducers, transducers change the processes that act on those values
        * The signature looks like this
          * `reducer = (accumulator, current) => accumulator`
          * `transducer = reducer => reducer`
          * Or to spell it out
            * ```javascript
transducer = ((accumulator. current) => accumulator) 
  	=> ((accumulator, current) => accumulator) ```
          * Generally speaking though, most transducers will need to be partially applied to some arguments to specialise them. For example, a map transducer might look like this
            * `map = transform => reducer => reducer`
            * Or more specifically
            * `map = (a => b) => step => reducer`
            * In other words, a map transducer takes a mapping function (called transform) and reducer(called the step function), and returns a new reducer. The step function is a reducer to call when we've produced a new value to add to the accumulator in the next step
        * Some **naive** examples
          * ```javascript
const compose = (...fns) => x => fns.reduceRight(
	(y, f) => f(y), x);

const map = f => step =>
	(a, c) => step(a, f(c));

const filter = predicate => step =>
	(a, c) => predicate(c) ? step(a, c) : a;

const isEven = n => n % 2 === 0;
const double = n => n * 2;

const doubleEvens = compose(
	filter(isEven),
  	map(double)
);

const arrayConcat = (a, c) => a.concat([c]);

const xform = doubleEvens(arrayConcat);

[map(double), filter(isEven)].reduceRight(y, f) => f(y), x);

[map(double)].reduceRight(
	(y = (a, c) => a.concat([c]), f = filter(isEven)) 
  		=> filter(isEven)((a, c) => a.concat([c])), x)
)

[].reduceRight(
	(y = filter(isEven)((a, c) => a.concat([c])), f = map(double))
  	=> map(dobule)(filter(isEven)((a, c) => a.concat([c]))), x)
)

xform = map(double)(filter(isEven)(a ,c) => a.concat([c])))

const result = [1,2,3,4,5,6].reduce(xform, []) // [4, 8, 12]```
        * It basically compose the function in the reducer one after each other, so instead of first filtering the whole array it takes the values one by one a completes the whole flow before taking another one
        * If this seems like a lot of work, keep in mind there are already functional programming libraries that supply common transducers along with utilities such as compose, which handle function composition, and into, which transduces a value into the given empty value
          * ```javascript
const xform = compose(
	map(inc),
  	filter(isEven)
);
into([], xform, [1,2,3,4]) // [2, 4]

// Notice that it compose top to bottom even when it is compose
// function. Explanation in next bullet point```
      * ## **Transducers compose top-to-bottom**
        * Transducers wrap around other transducers under composition. In other words, a transducer says: "I'm going to do my thing, and then call the next transducer in the pipeline", which has the effect of turning the execution stack inside out
        * It is wrapped in reducer basically, so reducer is called first and then inside the function call is happening
      * ## **Transducer Rules**
        * The example above is naive, because it ignores rules that transducers must follow
        * ### Rules
          * **Initialization**
            * Remember this rule: When called with no arguments, a reducer should always return a valid initial (empty) value for the reduction. It's generally a good idea to obey this rule for any reducer function, including reducers for React or Redux
            * ```javascript
const map = f => step => (a = step(), c) => (
	step(a, f(c))
);```
            * It calls next reducer in chain to ask about initial value if there is none provided
          * **Early Termination**
            * There must be a way how to send a message to all reducers to stop enumerating over values. They way how to do it is to send special type called reduced
              * ```javascript
const reduced = v => ({
  get isReduced () {
    return true;
  }
  valueOf: () => v,
  toString: () => `Reduced(${ JSON.stringify(v) })`
})```
              * The only parts that are strictly required are
                * **The type lift** - A way to get the value inside the type (reduced function)
                * **Type identification** - A way to test the value to see if it is a value of reduced (isReduced getter)
                * **Value extraction** - A way to get value back out of the type (e.g. valueOf())
              * toString() is just for debugging purposes
          * **Completion**
            * If you have more state to flush after the previous function has signaled that it's finished reducing, the completion step is the time to handle it.
            * At this stage you can optionally
              * Send one more value (flush your pending state)
              * Discard your pending state
              * Perform any required state cleanup
      * ## **Transducing**
        * ```javascript
const transduce = 
	curry((step, initial, xform, foldable) => 
  		foldable.reduce(xform(step), initial)         
)```
        * Transduce function takes following arguments
          * **Step** - function that is the final step in the transducer pipeline
          * **Initial** - initial value for the accumulator
          * **Xform** - transducer
          * **Foldable** - foldable is any object that supplies a .reduce() method
        * First we need **Step** defined, we can easily create function that transduces to an array. First we need a reducer that reduces to an array
          * `const concatArray = (a, c) => a.concat([c]);`
        * Next step provide **Initial** value and curry
          * `const toArray = transduce(concatArray, [])`
        * With **toArray()** we can replace two lines of code with one, and reuse it in a lot of other situations, besides
          * ```javascript
const result2 = toArray(doubleEvens, [1,2,3,4,5,6]);
console.log(result2); // [4,8,12]```
      * ## **The Transducer Protocol**
        * Transducers are really made of 3 different functions
        * In JavaScript transducer is an function that consist of 3 functions
          * **init** - Return a valid initial value for the accumulator (usually, just call the next step())
          * **step** - Apply the transform, e.g. for map(f): step(accumulator, f(current))
          * **result** - If a transducer is called without a new value, it should handle its completion step (usually step(a), unless the transducer is stateful)
        * Here is less naive implementation of the map transducer
          * ```javascript
const map = f => next => transducer({
  init: () => next.init(),
  result: a => next.result(a),
  step: (a, c) => next.step(a, f(c))
})```
          * Additionally, the special reduced object uses there properties in the transducer protocol
            * **reduced** - A boolean value that is always true for reduced values
            * **value** - The reduced value
      * ## **Conclusion**
        * Transducers are not always faster than built-in array methods. The performance benefits tend to kick in when the data set is very large (hundreds of thousands of items), or pipelines are quite large (adding significantly to the number of iterations required using method chains). If you are after the performance benefits, remember to profile
  * Action Points:
    * [ ] Look into this book about history of computer science from functional programming perspective - https://www.amazon.com/Structure-Interpretation-Computer-Programs-Engineering/dp/0262510871/ref=as_li_ss_tl?ie=UTF8&qid=1507159222&sr=8-1&keywords=sicp&linkCode=ll1&tag=eejs-20&linkId=44b40411506b45f32abf1b70b44574d2