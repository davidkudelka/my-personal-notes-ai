  * tags: #productboard #eventual #consistency #fusion
  * notes:
    * Schema

    * Creation flow 
      * Async events of data distribution to other parts
      * During mutation creation we don't know about slugUrl or any board data like isVisible, isLocked
    * Update flow
      * name, isVisible, isLocked, slug, slugUrl
    * Delete flow
      * I am going to delete board, it goes through pb-navigation first, so we are not able to navigate to the board first, if something goes wrong we could still get to that board through url