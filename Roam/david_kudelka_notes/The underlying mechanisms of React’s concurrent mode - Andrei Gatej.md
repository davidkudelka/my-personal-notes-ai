  * tags: #react #article #concurrency
  * link to article: https://andreigatej.dev/blog/the-underlying-mechanisms-of-reacts-concurrent-mode/
  * author: [[Andrei Gatej]]
  * notes:
    * ### Introduction
      * In this article, written explains React concurrent mode by diving deeper into `startTransition` function exported by `useTransition` hook
      * **`startTransition`**
        * Is able to breakdown expensive component work into multiple function calls, so this way their **computation** doesn't block the main thread
    * ### Yielding to the main thread
      * JavaScript runs in a single-threaded environment
        * Potentially you can make use of another threads (eq. **WebWorker**, **ServiceWorker**), but that's for different article
      * Main thread can run only task at a time, so it can block other tasks from executing
      * **So how can be this achieved?**
        * `window.setImmediate` - [link to the documentation here](https://developer.mozilla.org/en-US/docs/Web/API/Window/setImmediate)
          * This method is used to break up long running operations and run a callback function immediately after the browser has completed other operations such as events and display events
        * **Although** - this method is not expected to be implemented in the browsers. The **good** news is that there are alternatives -> [MessageChannel API](https://developer.mozilla.org/en-US/docs/Web/API/MessageChannel)
          * -> [Here is link on how React is implementing this API](https://github.com/facebook/react/blob/v18.2.0/packages/scheduler/src/forks/Scheduler.js#L569-L574), to schedule functions to be run after the browser performed some of its essential tasks
    * ### Visualizing the concurrent rendering process
      * ```javascript
while (workInProgress !== null) {
  performUnitOfWork(workInProgress);
}```
        * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/OcmU183yUv.png]]
      * This is how **concurrent** React works
        * ```javascript
while (workInProgress !== null && !shouldYield()) {
    performUnitOfWork(workInProgress);
  } 

const shouldYield = () => {
  const timeElapsed = getCurrentTime() - startTime;
  if (timeElapsed < frameInterval) {
    // The main thread has only been blocked for a really short amount of time;
    // smaller than a single frame. Don't yield yet.
    return false;
  }
  // ... Some details have been omitted for brevity.
  return true;
}```
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/kGT6iz4Uf7.png]]
