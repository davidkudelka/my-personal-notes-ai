  * tags: #react #article
  * link to article: https://joshcollinsworth.com/blog/antiquated-react
  * author: [[Josh Collins]]
  * notes:
    * ## Things you forgot (or never knew) because of React 
      * ### Your ecosystem doesn't need to be massive anymore
        * React is written in JavaScript, so in theory -> you should be able to use other libraries written in JavaScript as well
        * It's surprising how React is un-compatible with other JavaScript code
          * Mainly because of the lifecycle methods and it's quirks
      * ### React hooks are actually kind of outdated
        * They were released long time ago
        * It became good standart, but some of it implementations are not ideal -> like `useEffect`, not `Signals` in React, which makes the state management more difficult (and less performant)
      * ### You don't need to micro-manage rendering anymore
        * React is bit more harder to make performant, this is because of few reasons
          * `V-DOM` syncing with `DOM` - one way data flow
          * all the component tree's get re-rendered all the time
        * Some other frameworks have performance out-of-the-box
      * ### Nobody else is afraid of their framework's version of `useEffect`
        * Very complicated hook with bad implementation of dependency list
      * ### Scaling isn't really a frontend concern anymore
        * Writing modular code, abstract complexity, namespace collisions, data reactivity and etc... is **no longer**, just something that exist in React - other frameworks have it too, some of them even better
      * ### Server-side rendering isn't special anymore
        * Initial there was only `Next.js` in combination with `React` that could do server-side rendering very well, but that's not true anymore
          * Some of other frameworks have even by default server side rendering support - `SvelteKit`, `Fresh` (deno's frontend framwork), `Astro` (mainly just SSG) or `SolidStart` (Solid's meta framework)
      * ### Two-way data binding isn't hard and it isn't bad idea
        * syncing of `V-DOM` and `DOM` can be cumbersome and make's forms much harder in React (much less performant as well)
          * Some newer framework's allow two-way data binding, making the flow much simpler
          * Dogmatic ideals of best practices get in the way as much or more than they help - for something one-way data flow is good idea, for something it can be much more difficult
      * ### Styling is easy, actually 
        * Some frameworks solve styling out of the box -> scoped CSS
      * ### Frameworks aren't as hard to learn anymore
        * Just as a reminder how hard it is actually to learn `React` and all it's quirks and performance bottle-necks
        * Other framework's can be much simpler and much closer to basic browser API
      * ### Other options aren't just "new and shiny" (and nobody cares about that anyway)
        * Some of other frameworks are here for already quite some time
          * Astro, Svelte, Vue, Solid -> all of those framework's are already on stable versions, some of them for quite some time
      * ### React is way behind in performance
        * Not much to add, a lot of times it's difficult to make React performant, especially as you developing more complex web-apps with more and more interactions
    * ## The other stuff you should try
      * ### Svelte
        * compiler, instead of run-time, can ship much less JavaScript and it ship only code that it's using
      * ### Vue
        * close to react, but is more focused on the UI, using templating, more performant than React
      * ### Solid
        * We could call it almost newer version of React without tech-debt
      * ### Fresh
        * Server-side rendered frontend framework from Deno
        * **Good** if you want to run it in the cloud, shipping absolutely minimal JavaScript
      * ### Astro
        * Mainly SSG, but recently adding some server-side rendering features
        * By default not containing any JavaScript, you can add JavaScript if you need some additional features
      * ### Preact
        * Faster and more minimalist version of React
      * ### Qwik
        * New approach to hydratation and performance -> it serialises JavaScript into the DOM, and loads tiny bits only when it's needed 
        * **Good** if you're shipping lot of JavaScript to the browser, and you want a way to make that more performant
  * ### **Interesting topics to re-search**
    * **scoped CSS** - scoped styling should supposedly solve a lot of styling issue's, we are currently experiencing in React world