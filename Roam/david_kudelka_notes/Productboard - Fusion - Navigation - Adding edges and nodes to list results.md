  * tags: #relay #nodes #edges #pagination
  * notes:
    * # Proposal of new navigation query schema
      * **What is the issue?**
        * Current implementation of **navigationHierarchyLevel** is returning list od edges and Relay client assumes that all queries displaying lists are implemented in connection/edge architecture
      * ```javascript
navigationHierarchyLevel(parentId: ID): [NavigationNode!]!

We would change the return structure of this query to


navigationHierarchyLevel(parentId: ID): NavigationConnection

NavigationConnection {
  edges: [TeamspaceEdge | NavigationEdge | NavigationViewEdge!]!
  pageInfo: PageInfo!
}```
      * **Solution**
        * All Relay's example and tooling assumes you are using connection based architecture of lists
        * So if we implement connection based lists we can use relay directives to manipulate with relay cache very easily (@appendNode...). But mainly @connection (key: 'result_key') directive that sets connection key in relay's cache and we can easily access those results
          * To be honest I don't think it's even possible to add the record the the query result, there is no relay cache reference in the store for those records (I might be wrong, but I didn't find any easy way how to do it)
      * **Risks**
        * I don't have experience developing connections with different edge types. We should investigate if you can return different type of edges and how does relay react to it