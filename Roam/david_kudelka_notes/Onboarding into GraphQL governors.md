  * tags: #onboarding #graphql #governors
  * notes:
    * ### What should we go through?
      * This is description of the PB ticket
        * We have a Github team graphql-governance which is the schema governors group. Create a documentation which would be part of guild docs that would explicitly specify what schema governors group does (and possibly doesn't).
        * Note: "eyes" emoji should be used when someone from the group is in process of reviewing PR.
    * What should we focus on?
      * Code review of GraphQL schema
        * What exactly to look for, and what not to look for?
        * Should we assign sub-graphs to different people?
      * Linting issue's in Apollo Studio
        * How the process looks like?
        * Where can we adjust the deprecation dates? (it was partially answered by the doc by [[Ondrej Synacek]])
  * notes from the meeting
    * `graphql-gateway`, I should investigate here more
      * We are using `@tag` for marking some queries or fields as public
    * Relay and how it is opinionated
      * Maybe we should create some better on-boarding, in what exactly it is opinionated and node object, caching
    * deprecation
      * 60 days for removing field from FE
      * 90 days for BE to remove the field
    * FE schema -> link.schema.ts where all linters are enlisted
      * `white-list.ts`
      * `pbctl run lins-graphql`
        * It throws you list of errors
      * FE linters are donwloaded by all other repo's to run some eslint rules
    * Honeycomb runs some analysis on all our repos (link: https://ui.honeycomb.io/login/hd/productboard.com)
      * What is even honeycomb?
      * there are scraped data from all github repo's about linting issue's
