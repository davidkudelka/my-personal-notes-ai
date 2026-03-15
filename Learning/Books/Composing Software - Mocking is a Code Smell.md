  * tags:
  * book: [[Composing Software - Eric Elliot]]
  * notes:
    * # **Mocking is a Code Smell**
      * ### **TDD should lead to better design**
        * By any means try to avoid dependency injection
        * TDD should require fewer lines of code and more readable, flexible, maintainable constructions
        * You should remember two things
          * You can write decoupled code without dependency injection
          * Maximizing code coverage brings diminishing returns - the closer you get to 100% coverage, the more you have to complicate your application code to get even closer, which can subvert the important goal of reducing bugs in your application
        * More complex code means
          * More clutter leads to more convenient places for bugs to hide, which leads to more bug
          * It's easier to find what you are looking for when there is less clutter to get lost in
      * ### **What is a code smell?**
        * "A **code smell** is a surface indication that usually corresponds to a deeper problem in the system - [[Martin Fowler]] #quote
        * A code smell does not mean that something is definitely wrong,, or that something must be fixed right away. It is a rule of thumb that should alert you to a possible opportunity to improve something
      * ### **What is a mock?**
        * A **mock** is a test double that stands in for real implementation code during the unit testing process
        * Avoiding mocking can simplify tests, because you won't have to construct those mocks
      * ### **What is a unit test?**
        * **Unit tests** test individual units (modules, functions, classes) in isolation from the rest of the program
        * Unit tests usually use black box testing
        * Avoid white box testing = leads to wasted work
      * ### **What is test coverage?**
        * Code coverage refers to amount of code covered by test cases
        * There are 2 main kinds of coverage
          * **Code coverage** - how much of the code is exercised
          * **Case coverage** - how many of the use-cases are covered by the test suites
        * Unit tests by definition test units in isolation, **not in integration**, meaning that a test suite containing only unit tests will always have close to 0% case coverage for **integration** and **functional** use-case scenarios
          * 100% code coverage does not guarantee 100% case coverage
          * Developers targeting 100% code coverage are chasing the wrong metric
      * ### **What is tight coupling?**
        * **Coupling** is the degree to which a unit of code (module, function, class, etc...) depends upon other units of code. 
        * **Tight coupling**, or a high degree of coupling, refers to how likely a unit is to break when changes are made to its dependencies. In other words, the tighter the coupling, the harder it is to maintain or extend the application.
        * **Loose coupling** reduces the complexity of fixing bugs nad adapting the application to new use-cases
        * Coupling takes different forms:
          * **Subclass coupling** - subclass is dependent on parent class implementation - the tightest form of coupling available in OO design
          * **Control dependencies** - code that controls its dependencies by telling them what to do
          * **Mutable state dependencies** - code that shares mutable state with other code
          * **State shape dependencies** - code that shares data structures with other code, and only uses a subset of the structure. If the shape of the shared structure changes, it could brake the dependent code
          * **Event/message coupling** - code that communicates with other units via message passing, events, etc...
      * ### **What causes tight coupling?**
        * Tight coupling has many causes
          * **Mutation** vs immutability
          * **Side-effects** vs purity/isolated side-effects
          * **Responsibility overload** vs Do One Thing (DOT)
          * **Procedural instructions** vs describing structure
          * **Imperative composition** vs declarative compostion
        * Doing functional programming doesn't mean your code is immune to tight coupling, it is just easier to avoid it because basic building blocks are pure functions
        * How **pure function** reduce coupling?
          * **Immutability** - no mutation of existing values, they return new ones
          * **No side effects** - only thing we can observe is output, so all other things are very hard to test
          * **Do One Thing (DOT)** - it is very easy do define what this building block should do
          * **Structure, not instructions** - pure functions describe structural relationships between data, not instructions for the computer to follow, so two different sets of conflicting instructions running at the same time can't step on each other's toes and cause problems
      * ### **What does composition have to do with mocking?**
        *  The essence of all software development is the process of breaking a large problem down into smaller, independent pieces (decomposition) and composing the solutions together to form an application that solves the large problem (composition)
          * Mocking is required when our decomposition strategy has failed
          * Mocking is required when our supposed atomic units of composition are not really atomic, they are not independent
        * When **decomposition succeeds** it is possible to use generic composition utility, to compose pieces back together
          * Function composition (e.g. pipe, compose)
          * Component composition (e.g. higher order components with function composition)
          * State store / model composition (e.g. Redux combineReducers)
          * Object or factory composition (e.g. mixins or functional mixins )
          * Process composition (e.g. transducers)
          * Promise or monadic composition (e.g. asyncPipe, Kleisli composition with composeM(), composeK(), etc...)
        * If you are using generic composition utilities, each element can be unit tested in isolation without mocking others. Utilities are 3rd party libraries with their own tests, so only thing meaningful here is to integration test
        * You can compose functions manually (**imperatively**) or automatically (**declaratively**)
      * ## **How do we remove coupling?**
        * Causes of **tight coupling**
          * Class inheritance
          * Global variables
          * Other mutable global state (browser DOM, shared storage, network, etc...)
          * Module imports with side-effects
          * Implicit dependencies from composition
          * Dependency injection containers
          * Dependency injection parameters
          * Control parameters (an outside unit is controlling the subject unit by telling it what to do)
          * Mutable parameters
        * **Loose coupling**
          * Module imports without side-effects (in black box testing, not all imports need isolating)
          * Message passing / pubsub
          * Immutable parameters (can still cause shared dependencies on state shape)
        * What to do to **prevent tight coupling** from happening?
          * Use **pure functions**
          * **Isolate side-effects** - do not mix logic with I/O
          * **Remove dependent logic** - from imperative composition so that they can become declarative
        * ### **Use Pure Functions**
          * avoid mutation, you don't have to worry about performance and if that is an issue there are other solutions like memoized versions of the object
          * consider using Mori or Immutable.js libraries
      * ## **Isolate side-effects from the rest of your program logic**
        * There are 3 ways how you can achieve this
          * ### **Use pub/sub**
            * In the publish/subscribe pattern, unit don't directly call each other. Instead they publish messages (publishers) that other units (subscribers) can listen to
            * This is mainly used in DOM, and was commonly used in JQuery
          * ### **Isolate logic from I/O**
            * In order to make this kind of composition work, we need to ensure 2 things
              * haveWriteAccess - will reject if the user doesn't have write access. That moves the conditional logic into the promise context so we don't have to unit test it or worry about it at all (promises have their own tests baked into the JS engine code)
              * Each of these functions takes and resolves with the same data type. We could create a pipelineData type for this composition which is just an object containing the following keys: { user, folder, files, dbUser?, folderInfo? }. This creates a structure sharing dependency between the components, but you can use more generic versions of these functions in other places and specialise them for this pipeline with thin wrapping function
            * With those conditions met, it's trivial to test each of these functions in isolation from each other without mocking the other functions. Since we've extracted all of the logic out of the pipeline, there's nothing meaningful left to unit test in this file. All that's left to test are the integrations
          * ### **Use Objects that represent future computations**
            * It's similar idea as having monads, you return data with type and payload
            * ```javascript
const handleResponse = response => ({
  type: 'RECEIVED_RESPONSE',
  payload: response
})```
      * ## **"Code smells" are warnings, not laws. Mocks are not evil**
        * ```javascript
const express = required('express');
const app = express();

app.get('/', function (req, res) {
  res.send('Hello world!')
})

app.listen(3000, function () {
  console.log('Example app listening on port 3000!')
})```
        * Example above doesn't really make sense to unit test, if you want to unit test something here that would be the hello world response and we can separate the logic there and test that
        * ```javascript
const hello = (req, res) => res.send('Hello World!')

{
  const expected = 'Hello World!';
  const msg = 'should call .send() with ' + expected
  
  const res = {
    send: (actual) => {
      if(actual !== expected) {
      	throw new Error('NOT OK' + msg)	
      }
      console.log('OK: ' + msg)
    }
  }
  
  hello({}, res)
}```
        * You still need some integration tests, but adding more unit tests doesn't make much sense
      * ## **Mocking is great for integration tests**
        * Because integration tests test collaborative integrations between units, it's perfectly OK tot fake servers, network protocols, networks messages, and so on in order to reproduce all the various conditions you will encounter during communication with other units, potentially distributed across clusters of CPU's or separate machines on a network
        * There are a lot of useful integration testing tools that throttle network bandwidth, introduce network lag, produce network errors, and otherwise test  lots of other conditions that are impossible to test using unit tests which mock away the communication layer
        * It's impossible to achieve 100% case coverage without integration tests. Don't skip them even if you manage to achieve 100% unit test coverage. Sometimes 100% is not 100%