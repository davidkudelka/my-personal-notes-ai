  * notes:
    * ## Frequency counter pattern
      * if we need to count something
      * ```javascript
function same(arr1, arr2) {
  if(arr1.length !== arr2.length) {
    return false
  }
  let frequencyCounter1 = {}
  let frequencyCounter2 = {}
  
  for(let val of arr1) {
    frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1
  }
  for(let val of arr2) {
    frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1
  }
  for(let key in frequencyCounter1) {
    if(!(key ** 2 in frequencyCounter2)) {
      return false
    }
    if(frequencyCounter2[key ** 2] !== frequencyCounter1[key]) {
      return false
    }
  }
  return true
}```
      * this is always better than nesting loops
    * ## Multiple pointers
      * This is only useful for **sorted arrays**
      * Creating pointers or values that correspond to an index or position and move towards the beginning, end or middle based on a certain condition
      * Very efficient for solving problems with minimal space complexity as well
      * ```javascript
function sumZero(arr) {
  let left = 0;
  let right = arr.length - 1;
  while(left < right) {
    let sum = arr[left] + arr[right];
    if(sum === 0) {
      return [arr[left], arr[right]];
    } else if(sum > 0) {
      right--;
    } else {
      left++;
    }
  }
}```
    * ## Sliding window
      * This pattern involves creating a **window** which can either be an array or number from one position to another
      * Depending on a certain condition, the window either increases or closes (and a new window is created)
      * Very useful for keeping track of a subset of data in an array/string etc.
        * ```javascript
function maxSubarraySum(arr, num) {
  let maxSum = 0;
  let tempSum = 0;
  if(arr.length < num) return null;
  for(let i = 0; i < num; i++) {
    maxSum += arr[i]
  }
  tempSum = maxSum;
  for(let i = num; i < arr.length; i++) {
    tempSum = tempSum - arr[i - num] + arr[i];
    maxSum = Math.max(maxSum, tempSum)
  }
  return maxSum
}```
    * ## Divide and Conquer Pattern
      * This pattern involves dividing a data set into smaller chunks and then repeating a process with a subset of data
      * This pattern can tremendously **decrease time complexity**
      * This is basically binary search
        * ```javascript
function binarySearch(array, val) {
  let min = 0;
  let max = array.length - 1;
  
  while(min <= max) {
    let middle = Math.floor((min + max) / 2);
    let currentElement = array[middle];
    
    if(array[middle] < val) {
      min = middle + 1;
    } else if(array[middle] > val) {
      max = middle - 1;
    } else {
      return middle
    }
  }
  return -1
}```