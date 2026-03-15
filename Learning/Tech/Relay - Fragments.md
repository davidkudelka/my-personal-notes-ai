  * tags: #relay #fragments
  * notes:
    * Implementation
      * ```javascript
fragment Avatar_user on User {
  avatarUrl
  firstName
  lastName
}```
    * Relay **enforces** following naming on the fragments <moduleName>_<propertyName>
      * Read more here - https://relay.dev/docs/guided-tour/rendering/fragments/#internaldocs-banner
    * Fragments allow you to define reusable selections of fields on GraphQL types - helps you with scaling
      * ```javascript
// Instead of doing this when you want to render the avatar for the author 
// and the first two who liked the blog post...
query BlogPostQuery($blogPostId: ID!) {
  blogPostById(id: $blogPostId) {
    author {
      firstName
      lastName
      avatarUrl
    }
    likedBy(first: 2) {
      edges {
        node {
          firstName
          lastName
          avatarUrl
        }
      }
    }
  }
}

// ...you can do this
query BlogPostQuery($blogPostId: ID!) {
  blogPostById(id: $blogPostId) {
    author {
      ...Avatar_user
    }
    likedBy(first: 2) {
      edges {
        node {
          ...Avatar_user
        }
      }
    }
  }
}```