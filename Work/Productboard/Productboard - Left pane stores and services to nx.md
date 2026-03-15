  * tags: #productboard #technical-planning
  * notes:
    * # Structure
      * ### Miro board link
        * https://miro.com/app/board/uXjVOBB08ys=/
      * ### File separation
        * /inisghts/left-pane 
          * /data-access
            * note-collection - done
              * NoteCollectionStore
              * NoteCollectionService
            * menu - done
              * InboxMenuStore (-> InboxMenuService)
              * InboxMenuService (-> InboxSelectors & SpaceMembershipStore & Coachmarks)
                * Coachmarks and SpaceMembership can be put out of the docuemnt and it is used only in one file
              * InboxMenuSelectors (-> FavoriteNoteCollectionStore, InboxMenuStore) -> this one will be injected
              * InboxSelectors (NoteStore and many others, but I might need just one function from those selectors) - done
                * I am using just one function here and it can be easily exported
            * page-settings - done
              * InboxPageSettingsStore
              * InboxPageSettingsService
            * note-section - done
              * NoteSectionStore
              * NoteSectionSelectors (will be injected)
            * favorite-note-collection - done
              * FavoriteUserNoteCollectionStore
              * FavoriteUserNoteCollectionService
            * note result service - done
              * if needed will be injected