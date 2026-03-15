  * tags: #productboard #rendering #react #performance #discovery
  * dates: 
    * First session [[2023-07-12]]
    * Second session [[2023-07-13]]
    * Third session [[2023-07-14]]
    * Fourth session [[2023-07-20]]
  * tasks:
    * [x] Create notion page and transfer most of the knowledge there
      * Plan for context separation
        * [x] Start with document
        * [x] Document is ready
      * [x] useLocation optimisations - describe in notion doc the approach
  * notes:
    * ### Steps
      * [x] View videos from [[Tom Svoboda]] and point out solutions he is proposing
        * **Topics**
          * **Stateful context** - context provider contains too many values
            * Maybe there is a way how to trigger re-render of those components only for the values that are exposed??
          * Use **smart memo** for component where it matters
      * [x] Come up with your own possible solutions
        * **Virtualisation** - can reduce number of actually rendered items (can be difficult for implementation)
    * ### Topics to re-search
      * Refresh knowledge about React concurrent features
        * There are 2 hooks that we can potentially use
          * **useTransition** -> to offload less important state updates
          * **useDefferedValue** -> the same as useTransition, but when we don't have control over setting the state, maybe some 3rd party library does it
    * ### Topics to consider
      * Relay fragments refactoring
      * Virtualisation
      * Smart memo of components
    * ## Smart memo of components (re-render because parent component got re-rendered)
      * Changing routing re-renders whole main menu navigation again
        * **Why?**
          * Crossroads can be memoized, because it's re-rendering only because parent was re-rendered - easy fix, not much value
    * ## Fusion External dependencies context refactoring
      * It contains following logic
        * useActivityNotifications
        * useMainMenuExpansion
        * menuConfig
      * Every time user navigates to different page, this context is getting re-calculated and triggers re-render of all components that are using it in main menu. By refactoring it and separating it to more logical context it will be easier to optimise for re-rendering.
      * ### Task separation
        * **Preparation tasks**
          * Separate `useActivityNotifications` from main useDependencyFusionProvider
          * Separate `useMainMenuExpansion` from the main hook
          * Separate `menuConfig` from the main hook
        * **Section improvements tasks**
          * Static section fix - navigating between boards or different pages shouldn't trigger unnecessary re-renders to this section
          * Data section fix - navigating between boards or different pages shouldn't trigger unnecessary re-renders to this section
          * Favorites section fix - navigating between boards or different pages shouldn't trigger unnecessary re-renders to this section
    * ## Memoize isActive prop coming out of useLocation hook
      * As described in [[Tom Svoboda]]'s video, by doing this item wrapper that momoize's the rest, we will be able to cache components that listen to pathname change, but it doesn't change isActive state for them. (Catching re-render chain reaction at the root cause)
    * ## Virtualization (unknown solution)
      * Currently we are trapped in using ListHeadless component provided by Nucleus
      * Nucleus doesn't like some of our design patterns = we have to separate main menu navigation into multiple lists
      * ListHeadless supports virtualization only if all the items are inside one list, but we are forced to use more lists for each section one => resulting in in-ability for us to implement virtualization
        * Potentail solutions
          * Do some custom implementation at least for sections
            * Sections that are not visible, won't be rendered
          * Stop using ListHeadless component
            * We would loose a lot of functionality, drag and drop mainly and we could end up loosing our heads with those implementations
          * Initiate call with Nucleus about this
            * Maybe this brings in good argument for them to support our design patterns and allow us using their virtualization solution 
  * Open questions?:
    * To me it seems like some NX modules are OK to import to different libs
      * Which modules?
        * `@productboard/activities/data-access` - which imports useActivityNotificationsCount
          * Most likely, because the library imports some legacy code
        * `@productboard/view/data-access` - which imports getSubscriptionPlanNameForRestrictedView
          * Library imports stores and services from legacy