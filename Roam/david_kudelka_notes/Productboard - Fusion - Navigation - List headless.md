  * tags: #relay #tree-structure #graphql
  * notes:
    * Current limitations for our main menu
      * Schema
        * Pre-fetching one layer of items even when don't know if we need them (interesting question about fetching timings)
    * List headless is not allowing us currently
      * Loading states for sections. Not sure if we have even any designs for it, or how it should work?
      * List headless needs firmly set array of items as property, making it hard to use dynamic structure we would like to have with GraphQL
        * This leads to in-ability to use Relay store for data-management, instead we are taking data from Relay store and inserting it into React state
          * React state is not optimised for storing changing data, performance bottle-neck
          * We need to resolve how we can dynamically construct data into list headless, so that it allows us display loading states in reasonable way
  * summary:
    * We are using List-headless component provided by Nucleus to display our Main Menu Navigation List
    * **What is List-headless?**
      * It's component that builds some functionality around displaying lists like
        * Virtualisation - rendering optimization 
        * Drag & Drop (we are definitely interested in this)
    * What's the problem with **List-headless**
      * We didn't find out way how to use Relay store for constructing array of item's that goes to list-headless, there needs to be static array of items as input of list-headless
        * Currently we are forced to extract data between Relay store and React state
          * This complicates the whole functionality, we have to take care of syncing data between 2 stores, plus Relay is using their own data management with normalized cache
          * React state doesn't have any data management functionality, it's not performance optimized - we would have to develop all this functionality
      * How do we want to solve loading states of the sections? No loading states in list headless are supported currently (only for infinite scrolling)
    * **Solution**
      * We need to find a way how to use Relay store as input for List-headless
        * This needs to happen after analysing both implementations of Relay and list-headless, understanding limitations of the libraries and etc...
    * **Risks**
      * There needs be collaboration between Fusion team and Nucleus team, big risk as this is one of the main components and there is unknown solution of this problem. So potentially we can spend a lot of time finding solution.