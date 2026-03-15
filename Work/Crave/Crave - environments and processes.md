  * How to solve environments?
    * Creating new development environment where people can push the code
      * We will be able push small pr's on daily basis and release to staging only finished user stories, making it easier for QA
      * Cons
        * We have big team and with this process we would get to the point where certain user stories have to cherry picked (either because other teams can be in the middle of their user stories or members of the same team started working on different user story, to get unblocked), which is even quite difficult if we want to go for solution that should enable us push small pr's very often
    * Utilizing our dynamic deploys
      * We will be able to create bigfeature (or different tag - userStory) for each user story and push this user story once it is finished
      * Pros
        * We have already good seed data that can ensure that those dynamic deploys have meaningful data on them
      * Cons
        * There needs to be responsible person which is responsible for rebasing conflicts often so it is still manageable
        * I can see situation where the same backend work is required for multiple user stories and can potentially break staging and with this we would face duplicate work on both big feature branches and then resolving commits with same content
          * This issue can be solve by creating big feature with those backend changes and let's say the other user story branches would have to rebase from that branch from now on. This would make rebasing quite a painful experience since you would have multiple layers of rebasing that needs to be done, but it can solve the issue quite nicely
    * Questions
      * It would make sense to me that QA should receive for testing only completed user stories that doesn't break the system, since this can lead to unnecessary testing (things breaking, working again and anyway features have to be re-tested) and it terms of early feedback from QA regarding the functionality of user stories should be in my opinion be done by engineers (really owning the work that is shipped, no half broken features and so on...). Do you agree?
      * What seems to be the biggest challenge with any solution I listed is managing rebasing of the branches, only-thing I can think of is to have owners of the product parts or user stories that are developed which will solve this rebasing immediately when the changes are introduced to the related branches, any ideas?
        * Other solution seems very difficult to implement (like nx tool to manage monorepo or something like this)