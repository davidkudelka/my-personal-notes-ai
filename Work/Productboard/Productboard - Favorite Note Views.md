  * tags: #discovery #productboard
  * date: [[2022-05-11]]
  * notes:
    * ## Acceptance Criteria
      * ### List
        * Note Views are personalised on the user level - each user has their own list of favorite note views.
        * Makers can favorite note views (not contributor or viewer)
        * The user can mark any number of Note Vies as favorites.
        * The Favorite section lists Note Views in the order of date for favoriting, with latest favorite on top.
        * The Favorites section can be collapsed/expanded.
        * There is no pagination currently for the favorite section - we display all favorites without hiding any items
      * ### Item
        * When you click into a favorite note view, we highlight the Collection in blue in both the Favorite section and the regular Collections sections. Actions can be accessed in either of these places.
          * We trigger analytics event on click
        * When I use the context menu (...) on existing Collections, there is a new option on top called 'Favorite'.
        * Changed context menu label Favorite -> Add to Favorites
        * Clicking on this will mark the Collection as my personal favorite.
        * The context menu on a favorited Collection includes the action 'Remove from Favorites'. By clicking on this, the Collection will be removed from the Favorites section and we trigger toast message.
        * Delete note collection removes the related existing favorite collection for each user
    * # What needs to be done
      * ## Backend
        * Add field when was note view added to favorites (used on frontend for default soring of the section -> last added to favorites at the top of the list)
        * Add query argument to get only Favorite Note Views noteViews(type: "FAVORITE") - for example
        * Deleting note collection should delete favorite relation in the database as well
      * ## FRONTEND
        * ### List
          * We will be getting the data from the query (just filtering out isFavorite and sorting by when it was added to favorites)
          * Is expanded controled by flux store (to persist state if user is navigating somewhere else than insights page)
        * ###  Item
          * On open we want to track this even to analytics (note view id, and type Collection or Favorite)
          * Changing labels of context menu item (Remove from favorites - Add to favorites)
          * On adding - removing items from favorites trigger toast messages