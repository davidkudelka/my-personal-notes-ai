  * tags: #event-loop #javascript #nodejs #performance
  * author: [[Slava Knyazev]]
  * notes:
    * ## Description of issue
      * JavaScript runs in a single-threaded environment with an event loop, an architecture that is very easy to reason about. It’s a continuous loop executing incoming work. Said work can schedule more of it for the future.
    * ### Solution
      * If you have some longer running tasks in your JavaScript that can potentially block your event loop for longer period of times, you can use **setImmediate** function -> https://nodejs.dev/en/learn/understanding-setimmediate/
        * ```javascript
const asyncInterval = setInterval(() => {
  console.log("Event loop executed");
  exCount++;
}, 1);
const findNthPrimeAsync = async num => {
  let i, primes = [2, 3], n = 5;
  const isPrime = n => new Promise(
    resolve => setImmediate(() => {
      let i = 1, p = primes[i],
        limit = Math.ceil(Math.sqrt(n));
      while (p <= limit) {
        if (n % p === 0) {
          return resolve(false);
        }
        i += 1;
        p = primes[i];
      }
      return resolve(true);
    }
  ));
  for (i = 2; i <= num; i += 1) {
    while (!await isPrime(n)) {
      n += 2;
    }
    primes.push(n);
    n += 2;
  };
  return primes[num - 1];
}```
      * It will basically tell that it should run that chunk of code in **next iteration** of the **event loop handler**
    * ### Other solutions
      * **Off loading to another thread**
        * Using more workers to run your code 
          * ```javascript
const nth = 100; // play with this value

const findNthPrimeWorker = num => new Promise(resolve => {
  const worker = new Worker(require.resolve('./worker.js'), {
    workerData: num
  });

  worker.on("message", d => resolve(d));
})

findNthPrimeWorker(nth)```
      * **Throwing more server instances**
        * That is basically the same as more workers, but even more expensive. Since service workers can better utilise one CPU
    * ### Summary
      * If you choose to use service workers, you need better hardware
      * If you choose do it more async and use **setImmediate**, the hard part will be bit slower, but it will unblock other tasks from running
