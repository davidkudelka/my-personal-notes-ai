  * What is the issue?
    * We currently have unstable staging environment making it hard to test it with QA
    * We need to push sooner all the completed User stories throughout the sprint
  * Pain points
    * We are still merging unstable stuff into the staging, making not ideal to merge staging to demo mid sprint or even more often
    * Mobile team and more junior devs are using staging for development, making working with data unstable
  * List of improvements
    * Better seed data - making it possible for QA to test start testing without any additional adjustments
    * Have everyone using local development and dynamic deploys
    * Tasks without splitting backend and frontend tickets can still merge to staging, but using local development database
    * Tasks that depend on separation backend tasks ( mobile development, frontend engineers ) will always have dynamic deploy