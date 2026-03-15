  * tags: #fundamentals #testing #javascript #javascript
  * Author: [[Kent C. Dodds]]
  * Notes
    * # **Fundamentals of Testing in JavaScript**
      * It is really important for people to understand their abstractions to use them effectively
      * We gonna build our own small Jest library
      * ## Throw an Error with a Simple Test in JavaScript
        * An automated test in JavaScript is code that throws an error when things are unexpected
        * ```javascript
const result = sum(3, 7)
const expected = 10
if (result !== expected){
    throw new Error(`${result} is not equal to ${expected}`)
}```
        * The goal of an error message is to be as useful as possible, so we can easily identify the error and fix it as fast as possible
      * ## Abstract Test Assertions into a JavaScript Assertion Library
        * ```javascript
function expect(actual) {
  return {
    toBe(expected) {
      if (actual !== expected) {
        throw new Error(`${actual} is not equal to ${expected}`)
      }
    }
  }
}

let result = sum(3, 7)
let expected = 10
expect(result).toBe(expected)```
        * This function is like an assertion library it takes an value and compare it to the expected, we can as well add to expect function different props to the object like toEqual, toBeGreaterThan
      * ## Encapsulate and Isolate Tests by building a JavaScript Testing Framework
        * ```javascript
test('sum adds numbers', () => {
  const result = sum(3, 7)
  const expected = 8
  expect(result).toBe(expected)
})
 function test(title, callback) {
   try {
    callback()
    console.log(`${title}`)
   } catch (e) {
    console.error(`${title}`)
    console.error(e)
   }
 }

 function expect(actual) {
  return {
      toBe(expected) {
          if (actual !== expected) {
              throw new Error(`${actual} is not equal to ${expected}`)
          }
      }
  }
}```
        * We basically encapsulate the test in it's own function which runs in try catch and if it fails it returns different output with error message, so it is easily distinguishable between passed and error test
      * ## Support Async Tests with JavaScripts Promises through async await 
        * ```javascript
test('subtractAsync subtracts numbers asynchronously', async () => {
  const result = await subtractAsync(7, 3)
  const expected = 4
  expect(result).toBe(expected)
})

async function test(title, callback) {
  try {
   await callback()
   console.log(`good - ${title}`)
  } catch (e) {
   console.error(`bad -${title}`)
   console.error(e)
  }
}

function expect(actual) {
 return {
     toBe(expected) {
         if (actual !== expected) {
             throw new Error(`${actual} is not equal to ${expected}`)
         }
     }
 }
}```
        * To support async code we have transform our test function into async and add await before callback
      * ## Provide Testing Helper Functions as Globals in JavaScript
        * ```javascript
async function test(title, callback) {
    try {
     await callback()
     console.log(`good - ${title}`)
    } catch (e) {
     console.error(`bad -${title}`)
     console.error(e)
    }
  }
  
  function expect(actual) {
   return {
       toBe(expected) {
           if (actual !== expected) {
               throw new Error(`${actual} is not equal to ${expected}`)
           }
       }
   }
  }

global.test = test
global.expect = expect```
        * This sets **test** and **expect** as global variables
        * We just need to call
          * `node --require ./setup-globals.js lessons/globals.js`
          * to expose them in the testing file
      * ## Verify Custom JavaScript Tests with Jest
        * Our testing functions looks very similar to Jest now, we can as well run jest on the test we have in repo
          * `npx jest`
            * It will automatically detect jest file in the repository and run the tests for us, what makes jest such great tool is it's stats and styling of error messages to make them super clear