  * tags: #mentoring #task-refinement
  * content:
    * Refining this task - https://oakslab.atlassian.net/secure/RapidBoard.jspa?rapidView=230&projectKey=CR&modal=detail&selectedIssue=CR-715&quickFilter=461
    * ## Menu view task
      * special view - https://www.figma.com/file/SYSAcmm9CqAdbuvZBXwdE7/Downtown-Kiosk-MVP?node-id=532%3A625
      * normal kitchen view - https://www.figma.com/file/SYSAcmm9CqAdbuvZBXwdE7/Downtown-Kiosk-MVP?node-id=177%3A0
      * ### Splitting the tasks
        * Front end
          * Kitchen picker (top part)
            * This part contains of icons of kitchens
            * Frontend should fetch data from backend with kitchen information
            * We should solve how the icons should be displayed with different number of active kitchens and what is the limit of active kitchens (if there is no limit how can we fit all the information to the page)
          * Menu selection (bottom part)
            * How to handle bigger amount of menu categories displayed on the screen
            * We can investigate how to properly load images on the page
        * Backend
          * Query for getting kitchens in the menu
            * Potentially with pagination (should pagination be FE or BE)
          * Query for getting items from each kitchen
            * FE pagination for menu items
      * ### Questions
        * **User story**
          * Should we include as well menu item detail to this user story?
            * Because those things are very interconnected and one is blocked by another, working at the both tasks together can bring a lot of confusion and can create a lot of miss-communication
        * **Splitting tasks**
          * How to handle situation where 2 stories that are being worked together contain same components and you want to avoid duplicates?
          * Should I as lead engineer think about UI structure of the application and create additional tasks for some UI components before the story is developed, to avoid duplicate work on those?
          * Working with junior engineers and how to explain them how exactly you can work on all of those, maintaining small pr's (what pr size can be ideal), how to handle duplicate components?
        * **Data fetching**
          * It would be the best if we are loading all data for Kiosk before user starts any interaction, but this can be more difficult way how to handle stuff, is it a good think to go for this solution for MVP or is it a good thing to implement this solution as part of versioning? (how to )
    * Notes
      * First point
        * Understand if it make sense to the business (sometimes it can be overcomplicated, not efficient)
        * First the product thinking (make sure to fully understand)
      * Second point
        * Look at the frontend and understand feasibility 
        * if it is MVP cut off everything that is not necessary
        * make sure everything make sense to you
      * Splitting tasks
        * Consider team you have - before you start splitting
        * It is always better to have frontend and backend stuff in one ticket (easier communication, less time to settle on solution)
      * Don't try to refine tasks for everyone
        * Give people opportunity - 
      * Estimation
        * try to split estimation and refinement