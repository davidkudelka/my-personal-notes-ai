  * Issue - we are not dealing with assigning relationship between menu category and items, when item is assigned to 2 categories we can experience issues with resolving to which category is this item assigned
  * Solution
    * JSON - saving to the database JSON instead of sortedMenuCategoryIds and sortedMenuItemIds
      * {'arrayOfCategories": [{"menuCategoryId": ["menuItemId1", ",menuItemId2"]}, {"menuCategoryId2": [...]}]}
    * Another Table Describing Relationship  
      * MenuScheduleToCategory
        * id
        * categoryId: string
        * category: MenuCategory
        * itemIds: string[]
        * items: MenuItems