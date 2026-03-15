  * tags: #discovery #productboard
  * analytics:
    * [[Productboard - left pane - analytics]]
  * tasks:
    * [[Roam/david_kudelka_notes/Productboard - Sharing Note Views (public/private)|Productboard - Sharing Note Views (public/private)]]
    * [[Productboard - Favorite Note Views]]
    * [[Productboard - Managing Note Views]]
  * notes:
    * ## Questions
      * **Redirection**
        * All un-accessible links will be redirected to all notes
      * **Tag menu section** - discuss on the call tomorrow
        * Are we removing tag section?
      * **Search functionality** - not implement for feature parity
        * Are we implementing text search functionality (where should be this text search located)?
      * **Pagination**
        * When are we planning to have this functionality
        * How do we want to do it together with 
      * **Context menu**
        * Should we have general state - when is one context menu opened other one is closed ??
      * **Favorite section** - for feature parity yes
        * No pagination - we display all items, without hiding any
    * ## Implementation details

    * ## Notes
      * ### UI
        * Section Component
          * Implement sections and section item component from nucleus
        * Pop-ups
          * Description
            * We need to re-implement pop-ups (current implementation is using old higher order pop-up components)
            * First check nucleus if there are new pop-up components
          * List of pop-ups
            * Delete pop-up
            * Confirm filter reset pop-up
              * Save to analytics which filters we are getting rid of on on-cancel
        * Inputs (creating / renaming) **Nice to have**
          * Creating new note view is using legacy input (this component is imported from monolith as well - it has some hotkeys functionality that is hard to convert - class based component)
      * ### Sections
        * **Pricing dependency**
        * **Implement permissions** (showing note views only under some circumstances)
          * should be implemented for the main left pane component
        * **Implement coachmarks** - creating first note views ...

        * **Finishing sections**
          * Adding nucleus component
          * Functionality for hiding more than x number of items
      * ### Missing things
        * **Context menu actions**
          * Context menu - Should we have general state - when is one context menu opened other one is closed ??
          * Renaming
          * Set filters actions (open inbox filter action)
            * Send analytics
          * Delete -> pop-up

        * **Navigation**
          * Navigating to another note view without saved filter s (filters have changed) -> pop-up

  * New stories:
    * ## Managing note views
      * ### Groomed
        * Favorite Note Views section - **groomed**
          * Implementing whole favorite section
        * Sharing note views (public / private) - **groomed**
          * Setting it to private / public 
      * ### TODO
        * Rename collection - **todo**
          * Permissions
          * Adding renaming option
        * Delete collection - **todo**
          * Permissions
          * pop-up
        * Creating note view - **todo**
          * Permissions
          * Coachmarks
        * Set filters actions - **todo**
          * Trigger openning filter component
        * Left Pane sections - **todo**
          * Implement basic permission
          * Implement pricing enforcement (will be done later)
          * Hiding x number of items
    * ## Routing
      * Navigation
        * Reset filter pop-up
      * Auto Routing
        * Getting data for router
          * Re-route when viewing something you shouldn't
          * Opening correct note view through link
        * Backwards compatibility with old links
    * Save button - **groomed**
      * Save button functionality
      * tracking selected filters versus filters of note view
      * (still looking into it)
    * Styling - added to pb - not groomed
      * Adding nucleus components, finishing up all sections
  * TODO:
    * [ ] Check about routing
    * [x] Check pricing settings
    * [x] Check nucleus for pop-ups
      * there is pop-up with custom state
      * pop with state can be switched
      * we have as well dialog pop up with custom state
    * [ ] Deprecated input
      * There is textfield component which seems very similar
      * Does it support all necessary hotkeys?
    * Coachmarks
      * [x] Ask about coachmarks for M2