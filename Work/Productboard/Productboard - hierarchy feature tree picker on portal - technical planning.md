  * tags: #technical-planning #productboard
  * notes:
    * ## Plan for implementing hierarchy feature tree picker on portal
      * Step by step plan #hierarchy-feature-tree-picker-todo ^DI4SASHdu
        * [x] Create Launch Darkly flag
          * Created Launch darkly flag with name - main.discovery_portal.lazy_loaded_tree_floating_button
        * Finish up main component functionality
          * Data fetching
            * [ ] Solve featureIds coming from portal cards
            * [ ] Filter out view only features
            * [x] Component is being lazy loaded
          * Events
            * [x] Selecting new features trigger portal card creation process
            * [x] Selecting already selected feature will show detailed card
            * [ ] You can create new feature or product and when you click enter it should automatically trigger portal card creation process
              * PortalRouter.react.tsx
            * [ ] You should be able to create as well subfeatures
          * Data representation
            * [x] Adjust current node component to support ticked but as well creation
            * [ ] You should be able to create feature even to view only or locked features as maker with admin rights
        * [ ] Separate logic on floating button level and other 2 places hierarchy feature tree picker is used and write down inputs for this picker

        * [ ] Create new nx lib to put this hierarchy feature tree picker to

        * [ ] Check if the permissions are implemented correctly

        * [ ] Test are passing and consider writing some unit tests

        * [ ] Manual testing done

        * [ ] Sent for review
