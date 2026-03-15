  * Inputs of menu categories
    * id
    * name
    * menuItemType
      * FOOD
      * DRINK
      * MEAL_PACK
    * categoryType
      * REGULAR
      * SPECIAL
      * CATERING
    * facility picker
      * pick from facilities - only one option available
  * Features list
    * Adding new categories
      * Adding brand new menu categories
      * Simple form with those fields
        * name - string input - required
        * menuItemType - select with one selectable option - required
        * category type - select with one selectable option - required
      * This would be put on the facility page, not common page for MVP, since all menu categories are separated by facility anyway (it would be easier implementation)
    * List of all current menu categories
      * List with those fields
        * name
        * menuItemType
        * categoryType
        * MenuItems
          * First Question
            * we can show number of how many items have this assigned currently, but no update possible, because re-assignment would mean deleting all current items and updating the menu category - solution would be removal and adding new one
          * Second Question
            * should we show name of the menu items in pop up or maybe there will be detail that shows all menu items that belongs to this menu category with names and what else are you looking for on this form regarding menu items
        * MenuSchedule categories
          * First Question
            * we can show number of how many menu schedule categories are assigned but no updating - it would mean deep check of the menu schedule categories which can lead to complex solution - not mvp
          * Second Question
            * Should we again do detail page with name 
    * Removal of the menu category
      * remove button
        * remove menu category from all menu items
        * remove all menu schedule categories with this menu category and check if menu schedule category was the last one on any menu schedules if yes remove menu schedule 