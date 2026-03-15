  * tags: #graphql #productboard #data-fetching #fetching-strategy
  * notes:
    * # Plan
      * Moving query on level of insights board
    * ## Open questions
      * How to resolve Suspense
        * Suspense has to be triggered only for usePreloadedQuery components so in that depth of components we can just pass the query reference and all levels will solve Suspense exactly how it needs to
      * How to resolve redirect functionality?
        * it can work as it works currently if there can router consumer and the logic stays the same
  * ### InsightsNoteList
    * NoteListItem -> isDateVisible
    * InfiniteList -> show different headers
      * before the data are loaded isFiltered is false, after data are loaded we run the comparison to check filtering is on
  * ### InsightsNoteViewRouter
    * noteViewBySlugId (download duration of the query will be 200ms ±)
      * 276,25
      * 182.92
      * 171.58
      * 208.43
      * 298.62
      * 179.11