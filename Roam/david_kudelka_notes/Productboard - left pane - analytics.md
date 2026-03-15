  * tags: #productboard #analytics #discovery #note-views
  * date: [[2022-05-13]]
  * notes:
    * # List of all left pane (note views analytics)
      * Personal folder item
        * tracking which insights folder was opened ('all-notes' ...)
      * Favorite and Collections items
        * openning note collection (tracking noteCollection id and type - Favorite or Collection)
      * Context menu of collection items
        * Set Filters option
          * tracking on which note collection (collection id) this option was clicked
      * Filter reset pop-up
        * unsaved filters send to analytics
        * track if users clicks clear filters (not arguments)
      * Save button (three options - save | save as | clear filters)
        * track if users clicks clear filters (not arguments)
      * Note Collection Section
        * Note Collections Search
          * if users uses search (types something) we track this information without any other arguments
        * Toggle (expand)
          * we track if user expand or hide note collection section
    * ### Note view analytics implementation plan
      * NoteView opened -> id of note view and type (favorite | custom | ...)
        * Note View opened
          * view id
          * section type (favorite, my views, all views)
          * sharing type (public,private, null - for system views)
          * view type - (assigned to me, all notes, custom ....)
      * Note View item -> context menu -> set filters
        * id of note view on which clicked
        * tracking just this event as click (someone clicked on the button)
      * SaveButton
        * 2 events
          * Filter reset - just event
          * Which un-saved filters were discarded
      * FilterReset PopUp
        * 2 events
          * Filters reset
          * Which un-saved filters were discarded