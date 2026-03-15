  * tags: #fusion #shortcuts #productboard
  * open questions:
    * ### How to implement shortcuts in URL? Or maybe do not implement it at all
      * Issue that can occur when not having unique URLs
        * `auto-expanding` functionality on pathname change won't work, or we would have to change the functionality
        * In the future if we want to have different `Breadcrumbs` in the header
      * **Possible solutions to this problem**
        * Using `queryParam` in the url -> `?shortcut=uuid`
        * Using Shortcut ID in the url instead of `queryParam`
          * We would have to add support for each board
            * New GraphQL boards
              * We would have to add `... on ShorcutBoard` support and transform the data correctly for each board
            * Old (legacy) boards
              * We would have to add wrapper for `FeatureBoard` and `Roadmap` board that can input GraphQL id and return slug with slugId
          * Summary
            * Quite a lot of effort and legacy code changes to make this work, can lead to nicer URL's - but requires quite a lot of time to spend on ...
  * notes:
  * pull requests: 
    * Display navigation shortcuts in the main menu list #productboard-fusion-shortcuts-display-in-main-menu ^DlzHG6bVE
      * Create functional PR
        * [ ] PR with added badge icon
        * [x] functionality is done
        * [ ] cleaned up
      * [ ] Tests are added
      * [ ] Send for Review
      * [ ] PR merged
    * ...