  * tags: #productboard #discovery
  * Short Description: #discovery-productboard-favorite-collections
    * Discovery on implementation of navigation on how to add collections to your favorite list - if the favorite list is empty
  * Planning: #planning-productboard-favorite-collections
    * [x] Look into the code on how to implement Favorite tab to be always expanded, if there are no favorites shows empty state with clickable CTA
    * [x] How hard would it be to implement CTA with steps on how to add collections to favorites
      * [x] Understand how the CTA happens, where do you need to put the logic?
    * [x] Look into NX, how hard would it be to move the logic from legacy into nx libs
  * notes:
    * ## Output
      * ### Permanent favorite collections in Insights tab
        * # Permanent Favorite Collections in Insights
          * ## Tasks
            * **Favorite section**
              * Implementing empty state
              * Tab should be by default expanded
            * **Show me how functionality**
              * Adding state to InboxMenu component that keeps track of this flow
              * This functionality should auto expand Collections
              * Open Menu of first item
              * Highlight menu item “Add to favorites”
                * We already have highlighting functionality for highlighting chat messages (notification mentions in chat)
                * You can view this logic to get idea how it is done (CommentedActivity.react.tsx)
              * Triggering toast message to display “Collection added to favorites”.
            * **Adjust MenuItem to supported highlighted mode**
              * There can 2 ways on how to implement this functionality
                * Create wrapper around MenuItem component which will change background color
                * Adding new background color to MenuItem component (nucleus)
        * ## Research on moving legacy code to NX libs
          * A lot of code is unfortunately depended on a lot of legacy code and even structure of this menu inbox is all over the place
          * Inbox menu item is dependent on a lot of legacy stores and selectors which turned out to be the most difficult to move to nx libs, for this reason we decided it doesn’t make sense to move code to nx for this task
          * My rough estimation at this point would be more than a week (approximately one sprint of time)
      * ### Implementing CTA
        * We can use already existing components
        * If in the legacy code, it should be easy to implement
          * Create new coachmark for this purpose
          * There will be state that this coachmark can change for openning 
      * ### Legacy -> NX
        * Description
          * We would have to probably migrate all the stores that operates on top of the collections
        * Favorite Collections to nx library (story points 5)
          * LinkToFolder
            * Inbox selectors
            * NoteSectionStore
            * InboxPageSettingsStore
            * ConfirmFilterResetDialog
            * NoteResultService
          * Note Collection Menu
          * RenameNoteCollectionInput
          * NoteSectionSelectors
          * FavoriteUserNoteCollectionStore
          * NoteSectionStore
          * NoteCollectionStore
        * Note Collection to nx library (story points 5)
          * Inbox selectors -> nx (research)
          * NoteSection store -> nx (reasearch)
          * NoteSection selectors -> nx (research)
          * NoteCollection store -> nx (research)
          * Note Collection helpers -> nx (easy)
          * Link to folder -> nx (research)
        * Putting NoteCollectionStore to NX library 
          * 2 SP
        * Problematic components
          * InputWithState
          * Pop components used in delete
          * Coachmark tooltip - it's already in the onboarding coachmark