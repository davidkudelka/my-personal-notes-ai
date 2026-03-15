  * Tags:
    * [[Plextrac]]
    * [[Plextrac GraphQL]]
  * Scaffolding should contain list of mutations and list of queries that are used on frontend, plus there should be schema as well
  * ==Mutations==
    * {{[[table]]}}
      * Name
        * Args
          * Return Type
      * createRunBook
        * ?
          * RunBookType
      * updateRunBook
        * ?
          * RunBookType
      * deleteRunBook
        * ?
          * Boolean
      * createCategory
        * parentKey, name, description
          * CategoryType
      * updateCategory
        * parentKey, name, description
          * CategoryType
      * deleteCategory
        * key
          * Boolean
      * createActivity
        * name, categoryKey
          * ActivityType
      * updateActivity
        * data: (name, categoryKey), activityKey
          * ActivityType
      * deleteActivity
        * activityKey
          * Boolean
      * createActivityStep
        * name, activityKey
          * ActivityStepType
      * updateActivityStep
        * data: (name, activityKey), activityStepKey
          * ActivityStepType
      * deleteActivityStep
        * activityStepKey
          * Boolean
  * ==Queries==
    * {{[[table]]}}
      * Name
        * Args
          * Return Type
      * getRunBook
        * ?
          * RunBookType
      * getRunBooks
        * ?
          * Array of RunBookType
      * getCategory
        * categoryKey
          * CategoryType
      * getCategories
        * ?
          * Array of CategoryType
      * getActivity
        * activityKey
          * ActivityType
      * getActivities
        * ?
          * Array of ActivityType
      * getActivityStep
        * activityStepKey
          * ActivityStepType
      * getActivitySteps
        * ?
          * Array of ActivityStepType
  * ==Types==
    * RunBookType
      * ?
    * CategoryType
      * key
      * name
      * description
      * parentKey
      * updatedAt
      * createdAt
    * ActivityType
      * key
      * name
      * categoryKey
    * ActivityStep
      * key
      * name
      * activityKey
  * ==Subscription==
    * [[GraphQL Subscription]]
  * Implemented
    * [x] runbook
    * [x] runbookList
    * [x] runbookCreate
    * [x] runbookUpdate
    * [x] runbookDelete
    * [x] Category
      * [x] runbookCategory
      * [x] runbookCategoryList
      * [x] runbookCategoryCreate
      * [x] runbookCategoryUpdate
      * [x] runbookCategoryDelete
    * [x] Activity
      * [x] runbookActivity
      * [x] runbookActivityList
      * [x] runbookActivityCreate
      * [x] runbookActivityUpdate
      * [x] runbookActivityDelete
    * [x] ActivityStep
      * [x] runbookActivityStep
      * [x] runbookActivityStepList
      * [x] runbookActivityStepCreate
      * [x] runbookActivityStepUpdate
      * [x] runbookActivityStepDelete