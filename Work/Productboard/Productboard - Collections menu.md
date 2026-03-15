  * tags: #productboard #discovery
  * Short description: #discovery-productboard-collections-menu
    * Discovery on extracting collections from legacy code to nx structure
  * Planning: #planning-productboard-collections-menu
    * [x] Find out about dependencies between Filters and Collections
    * [x] Create Miro board with list of dependencies
    * [x] Create plan with discovery findings
    * [x] Present plan
  * notes:
    * ### Output
      * Dependency graph - https://miro.com/app/board/uXjVOCm2wEM=/
    * ### Structures list of stores that needs to be converted
      * Basic stores
        * RouteService
        * LabsFlagStore
        * TagStore
        * NoteStore
        * OrganizationStore
          * ConnectionStore
        * CurrentBoardStore
      * Inbox stores
        * InboxMenuStore (dependent on InboxMenuService)
        * InboxMenuService (dependent on CoachmarkService, InboxSelectors, SpaceMembership)
        * InboxMenuSelectors (dependent on few stores NoteSectionStore, NoteFilterStore)
        * InboxPageSettingsStore
        * InboxPageSettingsService
        * InboxSelectors (maybe we don't need all of the functions and we can convert just needed selectors) 
      * Note
        * Collection
          * NoteCollectionStore (user store dep, but just type)
          * NoteCollectionService  (NoteCollectionStore, NoteFilterStore)
        * Section
          * NoteSectionStore (easy)
          * NoteSectionSelectors (NoteCollectionStore, **CurrentBoardStore**)
        * Favorite
          * FavoriteUserNoteCollectionStore (user store but just type, NoteCollectionStore)
          * FavoriteUserNoteCollectionService (NoteCollectionStore, FavoriteUserNoteCollectionStore)
        * NoteResultService (**TagStore**, **OrganizationStore**, **NoteStore**)
        * NoteResultStore (easy)
      * Note-filters
        * NoteFilterStore (easy)
        * NoteFilterService (**TagStore**, CoachmarkStore and CoachmarkService)
    * ### List of stores
      * RouteService (easy)
      * LabsFlagStore (easy)
      * Inbox
        * InboxMenuStore (easy - dependend on Service)
        * InboxMenuService (dependend on CoachmarkService, Inbox selectors, SpaceMembership)
        * InboxMenuSelectors (dependent on few stores NoteSectionStore, NoteFilterStore)
        * InboxPageSettingsStore (easy)
        * InboxPageSettingsService (easy)
        * InboxSelectors (maybe we don't need all of the functions)
      * Pricing (we can potentially inject this pricing components, research further, otherwise extra story points for converting PricingEnforcement component to nx)
        * PricingEnforcement
          * PricingEnforcementSelectors
        * PricingEnforcementPresets (easy no dep)
        * PricingEnforcementFeatures (some constant dep)
      * Note
        * Collection
          * NoteCollectionStore (user store dep, but just type)
          * NoteCollectionService  (NoteCollectionStore, NoteFilterStore)
        * Section
          * NoteSectionStore (easy)
          * NoteSectionSelectors (NoteCollectionStore, **CurrentBoardStore**)
        * Favorite
          * FavoriteUserNoteCollectionStore (user store but just type, NoteCollectionStore)
          * FavoriteUserNoteCollectionService (NoteCollectionStore, FavoriteUserNoteCollectionStore)
        * NoteResultService (**TagStore**, **OrganizationStore**, **NoteStore**)
        * NoteResultStore (easy)
      * Note-filters
        * NoteFilterStore (easy)
        * NoteFilterService (**TagStore**, CoachmarkStore and CoachmarkService)
    * Extra stores that are dependencies
      * TagStore (easy)
      * NoteStore (easy)
      * OrganizationStore (easy)
        * ConnectionStore (easy)
      * CurrentBoardStore (easy)