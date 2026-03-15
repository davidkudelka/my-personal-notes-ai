  * tags: #graphql
  * Folder structure
    * src/
      * graphql/
        * generated/
          * nexus.ts - file with all generated types
        * schema/
          * nameOfEntity/
            * index.ts - just for easy import  reasons
            * queries.ts - put  in all queries
            * mutations.ts   - put  in all mutations
            * types.ts - put in all types (input types, entity types, enums...)
          * types.ts - file that exports all types, mutations and queries
    * schema.ts - setup of the nexus schema
    * schema.graphql - graphql file with schema
    * server.ts  - initialization in register function
  * Commands
    * npm run generate:nexus - generate types into nexus.ts and schema.graphql
  * Endpoints
    * /graphql
    * /voyager 
      * on development 
      * Graphical representation of GraphQL schema