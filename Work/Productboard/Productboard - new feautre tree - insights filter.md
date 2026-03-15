  * tags: #productboard #technical-planning
  * planning: #planning-productboard-new-feature-tree-insights-filter
    * **Discovery**
      * [x] Discover features board filtering component
        * **FeatureHierarchyFilterDropdownContent.react.tsx** implements LD flag that turns on or off lazy loaded component
      * [x] Discover the old filtering component
        * Old components is called -> **HierarchyFilter.react.tsx** and is located in **src/js/modules/inbox-filter/filters/HierarchyFilter.react.tsx**
      * [x] Create LD flag
        * main.insights.insights-hierarchy-filter-lazy-loading
      * [ ] Create list of inputs that goes into the filter hierarchy component
      * [ ] List of differences between feature board hierarchy component and insights board component (hidden functionality for example)
    * **Functionality**
      * [x] Rendering correct entites
      * [x] Search should work
      * [x] Selecting should work even for filters (in connection with filter store)
        * [x] Initial selected should work
        * [x] Selecting should work
      * [x] Clear should work (in connection with filter store)
      * [x] Showing restricted items should work (need some research)
        * we might be getting this information from the endpoint already
      * [x] If I don't have permission to see some features, it should display such message at the end of pop-up
        * [x] Skim through the messages and find restricted ids
        * [x] UI developed
        * [x] Remove action implemented
      * [x] Show hidden should work (need some research what it exactly means)
        * [x] network requests works correctly
        * [x] ui is polished
    * **Polishing everything up**
      * [x] Show hidden footer
      * [x] Filtered-products- skipRestricted
      * [x] The way how to get restricted items
      * [x] Check all analytic events
      * [x] Remove functionality with picking item higher in the hierarchy - check about this