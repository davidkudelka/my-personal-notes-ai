  * tags: #graphql #relay #tree-structure
  * tasks:
    * [ ] Create list of problems with current implementation
    * [ ] Do some research on list headless and our options with Relay
    * [ ] Create some Miro schema explaining my approach
  * notes:
    * ### Current structure
      * MainMenuInner
        * useMainMenu (inside of this component we are constructing items that will be added into ListHeadless)
          * useMainMenuHierarchy (query results are stored in react useState -> on open we are assigning sub-items)
            * useNavigationLevel (query definition with reduce function that filters through the list of results)
      * ListHeadless (that implements NavigationItem)
        * NavigationItem (TeamspaceItem | FolderItem | BoardItem)
          * useNavigationLevel (with props -> parentId, skip: !isLoading || isCollapsed)
    * ### What is the problem?
      * **isLoading** is handled with useState and takes care only of initial loading
      * **decoding GraphQL id** on frontend to find out about type
        * optimistic response handling becomes difficult
        * we already have this information returned by GraphQL and it is __typename
      * We don't use Relay to manage state of our data, but instead, we are using react useState to manage everything (so we are giving up this whole relay ecosystem, with normalized cache and everything)
        * How do we want to handle item updates? (we would have to write it ourselves)
        * Current solution works with polling the data every 5s and we can't use properly any caching management, because the same query is used across the whole navigation sidebar - so relay is very confused about what is happening
    * ### Proposed solution
      * ```javascript
navigationHierarchyLevel(parentId: $parentId) {
  __typename
  ... on Teamspace {
    iconColor
    id
    name
    childrens @skip(if: $isCollapsed) {
      ...FragmentSomething
    }
    hasChildren
  }
  ... on NavigationFolder {
    id
    name
    childrens @skip(if: $isCollapsed) {
      ...FragmentSomething 
    }
    hasChildren
  }
  ... on NavigationView {
    id
    name
  }
}

fragment FragmentSomething on SomeConnection {
  edges {
    node {
      __typename
      ... on NavigationFolder {
        id
        name
        children @skip(if: $isCollapsed) {
          ...FragmentSomething 
        }
        hasChildren
      }
      ... on NavigationView {
        id
        name
      }
    }
  }
}```
    * what if
      * ```javascript
navigationHierarchyLevel {
  edges {
    node # TeamspaceEdge {
      id
      name
      hasChildren
      ...NavigationFragment
    }
  }
}

fragment FragmentSomething on Teamspace {
  children @skip(if: $isCollapsed) {
    __typename
    ...on NavigationFolder {
      id
      name
      hasChildren
      ...FragmentSomething2 
    }
    ... on NavigationView {
      id
      name
    }
  }
}

fragment FragmentSomething2 on NavigationFolder {
    children @skip(if: $isCollapsed) {
    __typename
    ...on NavigationFolder {
      id
      name
      hasChildren
      ...FragmentSomething2 
    }
    ... on NavigationView {
      id
      name
    }
  }
}```
  * questions:
    * First layer on the sidebar - can there be only teamspaces? Or is it possible to have there as well navigation folders or navigation boards?
    * Can you put teamspace inside of an teamspace?
