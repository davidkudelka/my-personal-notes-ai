  * tags: #productboard #technical-planning
  * tasks: #pb-left-pane-tasks
    * Legacy -> nx feature libraries
      * Create monolith interface (done)
        * [x] Pr posted
        * [x] Reviewed
        * [x] Merged
      * Move common components: pop-ups, link-to-folder, context-menu
        * [x] Pr posted
        * [x] Reviewed
        * [ ] Merged
      * Move common components: inputs, helpers
        * [ ] Pr posted
        * [ ] Review
        * [ ] Merged
      * Note Collection separatoin of ui/common components
        * [ ] Pr posted
        * [ ] Reviewed
        * [ ] Merged
      * Note Collection
        * [ ] Pr posted
        * [ ] Reviewed
        * [ ] Merged
      * Favorite Collection
        * [ ] Pr posted
        * [ ] Reviewed
        * [ ] Merged
      * Personal Folder
        * [ ] Pr posted
        * [ ] Reviewed
        * [ ] Merged
  * notes:
    * ### Miro board link
      * https://miro.com/app/board/uXjVOBB08ys=/
    * ### Structure
      * **Main files**
        * Inbox menu
        * **Sub main categories**
          * NoteCollectionSection
            * NoteCollectionSectionContent (why is this different?)
              * NoteCollectionList (extra layer as well)
                * NoteCollectionItem (look for ui and similarities)
                  * NoteCollectionMenu (same as in favorites, probably the pop up menu with options)
              * NoteCollectionListUtils (extra layer as well)
                * NoteCollectionHelpers
          * FavoriteCollectionSection
            * FavoriteCollectionItem (look for ui and similarities)
          * PersonalFolderSection
            * PersonalFolderItem (look for ui and similarities)
        * **Common components**
          * CreateNoteCollectionInput
          * DeleteCollectionPopUp
            * ContextMenu (what is this?)
          * RenameCollectionInput
            * RenameCollectionInputHelpers
          * ConfirmResetDialog
          * LinkToFolder
      * **How to inject** 
        * There is notion page guide, plus roadmap-comments.tsx there is already injection implemented
    * ## Folder separation
      * features
        * context-menu (done)
        * link-to-folder (done)
        * inputs
          * rename-collection-input (TBD)
          * create-note-collection-input (TBD)
        * pop-ups (folder)
          * delete-collection-pop-up (done)
          * confirm-reset-pop-up (done)
      * ui
        * left-pane-context-menu (done)
        * input-with-state (probably should be injected, ??)