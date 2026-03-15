  * tags: #nx #monorepo #useful-commands
  * notes: 
    * Running **renaming** of the project
      * nx g @nrwl/workspace:mv --project insights-trends-feature-trends --destination insights/trends/feature
      * **Recommend using this custom one**
        * yarn nx workspace-generator move 
    * ### Type check
      * Running **type check** on the project (insights-digest-feature = name of the lib)
        * yarn nx run insights-digest-feature:type-check
      * Running **type check** on the **affected code** only
        * yarn nx affected --target=type-check
    * Running **storybook**
      * yarn nx storybook <name of the lib>
    * Running **dependency graph**
      * yarn nx dep-graph
    * ## How to run GraphQL generators
      * yarn nx run graphql-schema:update && yarn nx run graphql-client:compile
    * ## How to run e2e tests locally
      * You need to have staging database imported to your local 
      * Commands
        * yarn nx run insights-filtering-e2e-tests:e2e-tests --setupSpace
          * --setupSpace will setup the space and most likely it will get stucked, you need to re-run it without setupSpace
          * It will open cypress and you can then run your e2e tests as you wish
    * ## How to generate nx lib test coverage
      * commands
        * yarn nx run <nx-lib>:test --codeCoverage