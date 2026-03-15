  * notes:
    * # What is Big O Notation
      * to determine how good algorithm is
        * it categorise algorithms by it's performance
        * it's good to have good vocabulary to talk about how our code perfroms
        * discussing tradeoffs
      * ## Timing our code
        * you can use performance.now() in the browser
        * We shouldn't count time but count operations
        * ```javascript
function addUpTo(n) {
  return n * (n + 1) / 2
}```
          * ^^ there are 3 operations no matter how big **n** is
        * ```javascript
function addUptTo(n) {
  let total = 0;
  for (let i = o; i <= n; i++) {
    total += i;
  }
  return total;
}```
          * this one has much more operations and it grows based on n
        * We need to talk about in general terms
      * It's way how to formalize fuzzy counting
      * It allows us to talk formally about how the runtime of an algorithm grows as the inputs grow
      * ## The Big O types
        * types
          * linear - f(n) = n
          * quadratic - f(n) = n2
          * constant - f(n) = 1
          * f(n) can be something completely different
