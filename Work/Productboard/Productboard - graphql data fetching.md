  * tags: #discovery #productboard #graphql #data-fetching
  * notes:
    * Main query that takes care of routing
      * ```javascript
// at this point I distracted slug id from url
// I am sending this slug id to query to get filterString

query noteViewByRoutingSlugId(slugId: Int) {
  ... on SlugIdNotExistingReturningAllNoteView {
    id
    filterString
    slugId
  }
  ... on Success {
    id
    filterString  
  }

  
}


// or it throws error and error boundary I retry 
```