  * Pre-release data collection
    * Order 7680 - 12:30 pm today
    * before-release - master branch snapshot
  * Karol meeting
    * after release of mobile app should point to old url api - https://api-3.lb.cravedelivery.com/graphql
  * Before to check
    * double check delivery ele script that is correct
    * [x] double check that merge to production master branch is possible
  * Turn on maintanance mode
    * disable the slots first thing in the morning
    * make screenshots of the timeslots, maybe database logs
    * turn on promo banner with message - sync up about the message
  * Data preparations
    * Nothing required, download newest data from the sheets - https://oakslab.atlassian.net/secure/RapidBoard.jspa?rapidView=230&projectKey=CR&modal=detail&selectedIssue=CR-1483&assignee=5ebbb7b6767b660b7760346f
  * Data migrations
    * go step by step specified in the confluence page
    * double check delivery ele script that it is correct
  * Release deployment
    * Change env variables on production > higher version > database in database_url
    * change all override variables in cloud run to point to new v3 database
    * run release
    * after the release point Prod API to  [api5.cravedelivery.com](https://api4.cravedelivery.com/)
    * /status to check status if backend have access to everything
      * old log - {"status":"OK","bt":"OK","db":73} - take this log before deploy
    * Tell Matej
  * Turn off maintanance mode
    * Change banner
  * note
    * admin portal - problem 29th July made by alex
      * CONFLICT (content): Merge conflict in frontends/admin/src/facility/pages/runner.tsx
      * CONFLICT (content): Merge conflict in frontends/admin/src/facility/pages/pickup.tsx
      * CONFLICT (content): Merge conflict in frontends/admin/src/facility/pages/packager.tsx
      * CONFLICT (content): Merge conflict in frontends/admin/src/facility/pages/orderAssignment.tsx
      * CONFLICT (content): Merge conflict in frontends/admin/src/facility/pages/kitchen.tsx
      * CONFLICT (content): Merge conflict in frontends/admin/src/facility/pages/expo.tsx
      * CONFLICT (content): Merge conflict in frontends/admin/src/facility/pages/assignment.tsx
    * api2
      * CONFLICT (content): Merge conflict in api2/src/schema/kds/subscriptions.ts - problem  29th July made by Alex
      * CONFLICT (content): Merge conflict in api2/src/lib/pubsub.ts - problem 31st July made by Karol
      * CONFLICT (content): Merge conflict in api2/package.json - not a problem
    * workflows - not an issue
      * CONFLICT (content): Merge conflict in .github/workflows/test-api.yml
      * CONFLICT (content): Merge conflict in .github/workflows/deploy-staging-fe-catering.yml
      * CONFLICT (content): Merge conflict in .github/workflows/deploy-staging-api.yml
      * CONFLICT (content): Merge conflict in .github/workflows/deploy-production-fe-catering.yml
      * CONFLICT (content): Merge conflict in .github/workflows/deploy-production-fe-admin.yml
      * CONFLICT (content): Merge conflict in .github/workflows/deploy-production-api.yml
      * CONFLICT (content): Merge conflict in .github/workflows/deploy-demo-fe-catering.yml
      * CONFLICT (content): Merge conflict in .github/workflows/deploy-demo-fe-admin.yml
      * CONFLICT (content): Merge conflict in .github/workflows/deploy-demo-api.yml