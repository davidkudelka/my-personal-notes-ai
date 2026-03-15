  * Todo's
    * [ ] Scalar types for Date
    * [ ] Testing (After MVP)
    * [ ] Authentication
    * [ ] Pagination
    * [ ] Error Handling
    * [ ] Caching (After MVP)
    * {[x]}} File Upload
    * [ ] Documentation - [[Plextrac GraphQL Documentation]]
  * Link to GraphQL Documentation - [[Plextrac GraphQL Documentation]]
  * Link to GraphQL Error Handling - [[Plextrac GraphQL Error Handling]]
  * Link to GraphQL Pagination and Sorting - [[Plextrac GraphQL Pagination&Sorting]]
  * Pro's and Con's
    * Is GraphQL better than REST
      * The key difference between GraphQL vs REST is that GraphQL doesn't deal with dedicated resources. Instead, everything is regarded as a graph implying it's connected. What this means in practical terms is that you can tailor your request to match your exact requirements using the GraphQL query language.
    * What is advantage of GraphQL
      * A query language like GraphQL on the server-side and client-side lets the client decide which data it needs by making a single request to the server. Network usage was reduced dramatically for Facebook's mobile applications as a result, because GraphQL made it more efficient with data transfers.
    * What are the advantages of switching to GraphQL
      * Less endpoints are leading to less code, less code = less space for bugs to appear
      * You can automatically generate types from graphql schema
      * You can as well generate schema from code if you are using nexus for exmaple
      * It means that by writing code you are  automatically writing typescript types which leads to better documentation of code and much faster documentation of code
      * Front-end developers has much easier work, because they can download GraphQL schema and generate types from it as well, plus with tools like apollo they can as well generate hooks that communicates with API
      * This said with GraphQL you are reducing number of lines written and it automatically generates types for you which leads big bug reduction
      * By writting code you can easily generate documentation
    * How hard is to implement GraphQL into plextrac
      * Basic setup of GraphQL should be very easy Hapi supports graphql so it would be just adding one endpoint to the api and basic setup of authentication (we can reuse auth function that are already written)
    * Disadvantages ?
      * We would have another approach how to do stuff
      * Bigger dependencies stack