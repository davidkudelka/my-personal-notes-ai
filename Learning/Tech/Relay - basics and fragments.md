  * tags: #relay #data-fetching #library #fragments #basics #graphql
  * notes:
    * ## Basics and fragments
      * ### Relay consist of 2 main parts
        * **Compiler**
        * **The library**
      * ### Important part of relay are **fragments**
        * [[Relay - Fragments]]
      * ### How relay supercharges the **GraphQL fragment**
        * **Co-located data requirements and modularity**
          * Each component should list all the fields that it's using right in the file of that component, that way, it's easy to re-factor or understand the components
        * **Performance**
          * Relay re-renders your components only if data that are specified for this specific components changes - helps you scale your application as it is easy to track those changes
      * ### Render as you fetch
        * Video -> https://www.youtube.com/watch?v=Tl0S7QkxFE4
        * React docs article -> https://17.reactjs.org/docs/concurrent-mode-suspense.html#approach-3-render-as-you-fetch-using-suspense
        * Thanks to this approach you can avoid in most cases waterfall data fetching - you fetch all data that are required for the page
      * ### How Relay enforces modularity
        * As the BlogPost component, I only know I want to render two children components -> **BlogPostHeader** and **BlogPostBody**
        * I don't know what data they need (why would I? That's their responsibility to know!)
          * Instead, they've told me all the data they need is in a fragment called **BlogPostHeader_blogPost** and **BlogPostBody_blogPost** on the **BlogPost** GraphQL type
          * As long as I include their fragments in my query, I know I'm guaranteed to get the data they need, even though I don't know any of the specifics
          * And When I have the data they need, I'm allowed to render them
      * ### The Relay compiler knows all GraphQL code you've defined in your project
        * Using fragments tightly coupled to components allows Relay to hide the data requirements of a component from the outside world, which leads to great modularity and safe refactoring
      * ### How Relay distributes data to the components?
        * Normal graphql framework (like apollo)
          * There is one data source and you need to pass all your data as props (prop drilling of the data)
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/o-OGVIgcmf.png]]
        * Relay does it differently - something like Redux
          * Each component just ask the stores which data it is interested in
          * Only thing you have to prop drill is the query key
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/eSps_jmdJy.png]]
      * ## Summarising fragments
        * Through the type system, Relay is making sure this component cannot be rendered without the exact right object from GraphQL, containing its data. One less thing to mess up
        * Since each component using fragments will only update if the exact data it uses updates, updates to the cache is performant by default in Relay
        * Through type generation, Relay is ensuring that any interaction with this fragment's data is type safe. Worth highlighting here is that type generation is a core feature of the Relay compiler