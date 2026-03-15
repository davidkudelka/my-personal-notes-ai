  * Engagement
    * clientId
    * tags
    * title
    * description
    * status (in-progress / closed)
    * runbookId
    * engagementActivities
      * name
      * isCompleted
      * status (enum)
      * outcome (enum)
      * included as finding (boolean)
      * operators (userid or just storing user information)
      * executionSteps
        * isCompleted
        * description
      * notes
        * text
      * attachments
        * filename
        * filePath (URL)
        * include in finding
        * createdAt
        * updatedAt
      * attack source 
        * text
      * activity log
        * activity
        * start Date
          * date
          * timezone
        * end Date
          * date
          * timezone
  * Runbook
    * Title
    * Categories
    * Activities
    * Category (methodology)
  * Naming convention
    * rb - for runbooks
    * rb-e - for runbooks engagement etc ...
  * -------
  * There will be just one mutation for creating category, with parentId argument and based on that the level is set
  * When importing techniques with sub-techniques the technique is replaced with sub-techniques beginning with technique name.
  * ------
  * Queries
    * runbookList - sort  by title, methodologies, number of Tactics, number Of Techniques, number of Activities
    * categoryList (parentIds) - search by name ?
    * activityList (categoryId) - search by name ?
  * Mutations
    * createRunbook (title: )
    * updateRunbook (categories, activities, title)
    * createEngagement (clientId, tags, description, runbookId)
    * deleteRunbook (runbookId)
    * runbook(runbookId)
  * first, after
  * edges