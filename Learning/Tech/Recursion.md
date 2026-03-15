  * notes:
    * ## What is recursion?
      * It's different way how to think about problem
      * A **process** (a function in our case) that **calls itself**
    * ## Why Use Recursion?
      * it's everywhere - JSON.parse / JSON.stringify
      * document.getElementById and DOM traversal algorithms
      * Object traversal
      * Even more complex data structures are using it
      * It's sometimes a cleaner alternative to iteration
    * ## The call stack
      * Any time a function is invoked it is placed (pushed) on the top of the call stack
        * When JavaScript sees the **return** keyword or when the function **ends**, the compiler will remove function from there (pop)
    * ## The base case
      * The condition of recursion function to determine when the recursion ends
      * This is the most important concept to understand
      * ```javascript
function countDown(num) {
  if(num <= 0) {
    console.log('All done!')
    return;
  }
  console.log(num)
  num--;
  countDown(num);
}

// SUM RANGE

function sumRange(num) {
  if(num === 1) return 1;
  return num + sumRange(num - 1)
}

// FACTORIAL

function factorial(num) {
  if(num === 1) return 1
  
  return num * factorial(num - 1)
}```
    * ## Common pitfalls
      * You don't have good base case, so it will get stack in the loop until the call stack is full and it throws error
      * Forgetting to return or returning the wrong thing
    * ## Helper method recursion
      * ```javascript
function collectOddValues(arr) {
  let result = [];
  
  function helper(helperInput) {
    if(helper.length === 0) {
      return;
    }
    if(helperInput[0] % 2 !== 0) {
      result.push(helperInput[0])
    }
    helper(helperInput.slice(1))
  }
  
  helper(arr)
  
  return result
}```
      * ### Pure recursion
        * ```javascript
function collectOddValues(arr) {
  let newArr = [];
  
  if(arr.length === 0) {
    return newArr
  }
  
  if(arr[0] % 2 !== 0) {
    newArr.push(arr[0]);
  }
  
  newArr = newArr.concat(collectOddValues(arr.slice(1)));
  return newArr;
}```
        * Tips
          * For arrays, use methods like **slice, the spread operator, and concat** that make copies of arrays so you do not mutate them
          * Remember that strings are immutable so you will need to use methods like **slice, substr, or substring** to make copies of strings
          * To make copies of objects use **Object.assign, or the spread operator**
