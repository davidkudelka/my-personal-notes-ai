  * tags: #ruby #fixing-data
  * notes:
    * ### Commands
      * ```javascript
pb-backend-run rails c // run ruby console

SpaceContract.find(129).subscription_plan // find specific version of your space contract

space = Space.find_by(domain: 'test') // finding your space

space.update!(subscription_plans_version: 10) // updating your space subscription version```
      * After those commands your space and your space contract subscription versions should be in sync and you are free to update them through admin console