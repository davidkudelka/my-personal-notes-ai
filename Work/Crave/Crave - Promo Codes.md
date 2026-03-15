  * Schema -> [[Crave - Promo Codes - Schema]]
  * Todo list
    * Backend
      * {[x]}} Implement latest changes in the design
      * {[x]}} Fix issue with date filtering
      * {[x]}} Fix issue with moment
      * {[x]}} Add filtering by disabled/inactive
      * {[x]}} Implement feedback
      * {[x]}} Ping Jakub to re-review
      * {[x]}} Merge pr
    * Frontend
      * Promo List
        * {[x]}} Rebase with changes on backend
        * {[x]}} Fix issue with timespan component
        * {[x]}} Fixing filtering of inactive state
        * {[x]}} Add loading state
        * {[x]}} Fix caching issue
        * {[x]}} Fix fragment in list
        * {[x]}} Fix values display in promo list
          * {[x]}} Adjust filter
          * {[x]}} Add description - [[Crave - Promo codes - description in list]]
          * {[x]}} Add restaurant tag 
            * {[x]}} Create custom component for this
        * {[x]}} Review pr
        * {[x]}} Implement 1 round of feedback
        * {[x]}} Wait for review
        * {[x]}} Implement 2nd round of feedback
        * {[x]}} Merge PR
      * Promo Form
        * {[x]}} Move code from old pr
        * {[x]}} Add mutations, queries and fragments
        * {[x]}} Create new multi choice select component
        * {[x]}} Adjust sections according to new changes
          * Type
            * {[x]}} Get answer about Buy X get Y
            * {[x]}} Buy X get Y
            * {[x]}} Free X
          * Applies To
            * {[x]}} Hide when (Buy X get Y, Free X)¨
            * {[x]}} Specific Item
            * {[x]}} Specific Category
            * {[x]}} All Items Except
          * Order Method
            * {[x]}} Fix
          * Eligibility
            * {[x]}} Segment groups
            * {[x]}} Specific customers
            * {[x]}} Employees
          * Usage Limits
            * {[x]}} Limit number of times
            * {[x]}} Limit to day of the week
            * {[x]}} Limit to time of day
        * {[x]}} Finish up creating
        * {[x]}} Finish up updating
          * {[x]}} Bug with validTill
          * {[x]}} Parse data as initial values
            * {[x]}} Segment groups
            * {[x]}} Usage limits
            * {[x]}} Minimum requirements reset 
            * {[x]}} ValidSince
            * {[x]}} ValidTill
        * {[x]}} Data not appearing in list after adding
        * {[x]}} Maybe same issue with data update
        * {[x]}} Pagination
        * {[x]}} Description format fix
        * {[x]}} Add types to all props
  * Improvements
    * [x] Add disabled and stats when updating promo
    * [x] Multi select
      * [x] Add grouping as optional
      * [x] Add groups to multi select
      * [x] Add placeholders
      * [x] Add message for no entries
      * [x] Bad dropdown in buyx and freex
      * [ ] Styling
        * [ ] Checkboxes
        * [x] Change color of group name
      * [x] Placeholders
      * [x] Applies to
      * [x] eligibility
      * [x] usage limits
    * [x] Validation
      * [x] Kitchens
      * [x] Code
      * [x] Type
      * [x] AppliesTo
      * [x] Order Method
      * [x] Minimum requirements
      * [x] Eligibility
      * [x] Usage Limits
      * [x] Active Dates
      * [x] BuyXGetY checking I have both values
    * [x] Add loading to PromoList Loading (if there are many records it loads for quite some time)
    * [ ] If I deselect kitchen remove all options from select
    * [ ] Refactoring
  * Promo codes validation
    * [x] Do some basic research #promo-validation
    * Validation research -> [[Crave - Promo Codes - Validation]]
  * Release to production
    * [ ] Write a script for transforming old data to the new ones
      * [ ] Set default values for all old records
      * [ ] method - we need to add manually both options
  * [[Crave - Promo Codes - Calculation]]