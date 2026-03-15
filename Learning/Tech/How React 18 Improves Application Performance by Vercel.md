  * tags: #article #react #performance 
  * notes:
    * ## Intro
      * JavaScript runs in **single thread**, if some tasks take long time to complete it can happen that they are blocking user interactions or other tasks to be completed -> lagging UI
        * Even user interactions, input's are handled by this single thread
        * Tasks are added into the JavaScript event loop
      * Every task longer **than 50ms** is considered **"long task"**
      * ### Metrics
        * [**TBT** - Total Blocking Time](https://vercel.com/docs/concepts/speed-insights#total-blocking-time-tbt)
          * It's an important metric measuring time between [**FCP** - First Contentful Paint](https://web.dev/fcp/) and [**TTI** - Time to Interactive](https://web.dev/tti/)
    * ## New important features
      * ### Transition
        * Currently we can mark some UI updates as non-important and they can be de-prioritised from the main ui updates, making the UI faster
      * ### Suspense
        * The same, we can be waiting for data to be downloaded and not rendering the component meanwhile
    * ## Conclusion
      * We have more tooling how to set some updates as non-important
      * Separate our UI updates into more chunks and therefore make more room to listen to user interactions, make ui less laggy