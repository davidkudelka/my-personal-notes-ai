  * tags: #graphql #relay #conditional-rendering
  * when: [[2022-08-08]]
  * notes:
    * Conditional fetching/rendering
      * For conditional rendering you should consider using @skip and @include GraphQL directives
        * ```javascript
query TestQuery(showSection1: Boolean!) {
  ...section1Fragment @include(if: showSection1)
  ...section2Fragment @skip(if: !showSection1)
}```
        * You can see implementation on those 2 links
          *  Query definition -> https://github.com/productboard/pb-frontend/blob/387371ea26ee2b311462bd34b6c78a020d9b528e/libs/insights/left-pane/feature/src/lib/components/left-pane-sections.tsx
          * Fragment definition -> https://github.com/productboard/pb-frontend/blob/387371ea26ee2b311462bd34b6c78a020d9b528e/libs/insights/left-pane/feature/src/lib/components/my-favorites-section.tsx
          * Relay docs link -> https://relay.dev/docs/api-reference/graphql-and-directives/#arguments