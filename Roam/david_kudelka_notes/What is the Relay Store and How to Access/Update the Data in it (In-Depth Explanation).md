  * tags: #relay #relay-store #graphql #article
  * author: [[Yaroslav Kukytsyak]]
  * notes:
    * ## Entry point of Relay store
      * Relay store starts with `root` object, it's the entry point of the store with following starting structure
        * ```json
{
  'client:root': {
    __id: 'client:root',
    *typename: '*Root'
  }
}```
      * When we call some query, it's result is added to this `root` object 
        * Query definition
          * ```json
query PostQuery($postId: ID!) {
  post(id: $postId) {
    title
    author {
      name
    }
  }
}```
        * Root store after the query
          * ```javascript
{
  'client:root': {
    __id: 'client:root',
    *typename: '*Root',
    'post(id:"UHsd8J")': {
      __ref: 'UHsd8J' // ID of the post record
    }
  },
  UHsd8J: { // Post record
    __id: 'UHsd8J',
    __typename: 'Post',
    id: 'UHsd8J',
    title: 'An example post',
    author: {
      __ref: 'HnT09q' // ID of the user record
    }
  },
  HnT09q: { // User record
    __id: 'HnT09q',
    __typename: 'User',
    id: 'HnT09q',
    name: 'John'
  }
}```
      * ### Difference between `DATA IDs` and `object IDs`
        * You might be wondering what is the difference between `id` and `__id`
        * Normally all the objects should have matching values between `id` and `__id`
          * But some objects that are **saved** to **Relay store**, doesn't have database id from backend, but Relay store still **needs** to **reference them** 
          * Like **connections**
    * ## Connections
      * How is Relay generating connection id's mentioned above?
        * Example query
          * ```javascript
query PostCommentsQuery($postId: ID!) {
  post(id: $postId) {
    comments(first: 2) {
      edges {
        node {
          id
          body
        }
      }
    }
  }
}```
        * Generated reference
          * ```javascript
{
    'client:root': {
    __id: 'client:root',
    *typename: '*Root',
    'post(id:"UHsd8J")': {
      __ref: 'UHsd8J' // ID of the post record
    }
  },
  UHsd8J: { // Post record
    __id: 'UHsd8J',
    __typename: 'Post',
    id: 'UHsd8J',
    title: 'An example post',
    author: {
      __ref: 'HnT09q' // ID of the user record
    },
    // This new field has been added
    'comments(first:2)': {
      // ID of the comments connection record
      __ref: 'client:UHsd8J:comments(first:2)'
    }
  },
    // Record for the comments connection
  'client:UHsd8J:comments(first:2)': {
    __id: 'client:UHsd8J:comments(first:2)',
    __typename: 'CommentConnection',
    edges: {
      __refs: [
        // ID of the record for the first edge
        'client:UHsd8J:comments(first:2):edges:0',
        // ID of the record for the second edge
        'client:UHsd8J:comments(first:2):edges:1'
      ]
    }
  },
  // First edge
  'client:UHsd8J:comments(first:2):edges:0': {
    __id: 'client:UHsd8J:comments(first:2):edges:0',
    __typename: 'CommentEdge',
    node: {
      // ID of the first comment record
      __ref: 'QW5zd2',
    }
  },
}```
      * **Important** - Relay **automatically** generate data IDs in **deterministic way**
    * ## Store proxy and records proxies (how to access store data)
      * To **access** store data, we use **record proxy**
      * How to get any record? - `const postRecordProxy = storeProxy.get('UHsd8J');`
      * How to get primitive value of that record? - `const title = postRecordProxy.getValue('title');`
      * How to get linked entities on that record? - `const authorRecordProxy = postRecordProxy.getLinkedRecord('author');`
        * For arrays - `const edgeRecordProxies =
  commentsConnectionRecordProxy.getLinkedRecords('edges');`
      * ### Accessing root object with ease
        * How to access root object? - `const root = store.getRoot();`
        * How to access query result in the root object? - `const post = root.getLinkedRecord('post(id:"UHsd8J")');`
          * **Important** - better way
            * `const post = root.getLinkedRecord('post', { id: 'UHsd8J' });`
    * ## Mutation of data
      * Mutating **primitive** type
        * `post.setValue('New Title', 'title');`
      * Mutating **linked record** type
        * ```javascript
const newAuthor = store.get(newAuthorId);

post.setLinkedRecord(newAuthor, 'author');```
      * Mutating **linked records** type
        * ```javascript
const newCommentEdge = store.get(newCommentEdgeDataId);
const commentsConnection = post.getLinkedRecord('comments', { first: 2 });
const commentEdges = commentsConnection.getLinkedRecords('edges');
const nextCommentEdges = [...commentEdges, newCommentEdge];

commentsConnection.setLinkedRecords(nextCommentEdges, 'edges');```
      * ### Creating new records
        * ```javascript
const newPost = store.create(
  generateUniqueClientID(),
  'Post',
);```
        * Notice that we use **generateUniqueClientID**, which is imported from **relay-runtime**, and ensures that this record will be **globally unique**
        * After this creation we can add fields to it via
          * **setValue** or **setLinkedRecord** or **setLinkedRecords**
        * **Important - or we can copy fields from different record**
          * `newPost.copyFieldsFrom(post);`
          * this code will copy all fields, besides ***id** and ***typename**
      * ### Deleting records
        * You can use command - `store.delete(userId);`
        * **Important**
          * It will leave null in that place
          * ```javascript
{
  UHsd8J: { // Post record
    author: {
      __ref: 'HnT09q' // ID of the deleted user record
    },
    // ...
  },
  HnT09q: null, // User ID now points to null
  // ...
}```
    * ## @connection directive
      * Should be mainly useful for paginated results
      * **Why?**
        * query definition
          * ```javascript
fragment PostComments_post on Post {
  comments(first: $firstComments, after: $afterComment) @connection(key: "PostComments_post_comments") {
    edges {
      node {
        id
        body
      }
    }
  }
}```
        * results in
          * ```javascript
{
    'client:UHsd8J:__PostComments_post_comments_connection': {
    edges: {
      __refs: [
        // IDs of the edge records
        'client:UHsd8J:__PostComments_post_comments_connection:edges:0',
        'client:UHsd8J:__PostComments_post_comments_connection:edges:1'
      ]
    },
    // ...
  },
}```
        * Which is probably expected, but it's interesting when we fetch more records through that query
          * ```javascript
{
    'client:UHsd8J:__PostComments_post_comments_connection': {
    edges: {
      __refs: [
        'client:UHsd8J:__PostComments_post_comments_connection:edges:0',
        'client:UHsd8J:__PostComments_post_comments_connection:edges:1',
        // The two new edges were appended
        'client:UHsd8J:__PostComments_post_comments_connection:edges:2',
        'client:UHsd8J:__PostComments_post_comments_connection:edges:3'
      ]
    },
    // ...
  },
}```
        * You can see that it adds those 2 new records at the end of the list
      * ### ConnectionHandler utilities
        * Accessing connection
          * ```javascript
const commentsConnection = post.getLinkedRecord('__PostComments_post_comments_connection');
// Can be replaced with
const commentsConnection = ConnectionHandler.getConnection(
  post,
  'PostComments_post_comments'
);```
        * Creating new edge
          * ```javascript
const newCommentEdge = ConnectionHandler.createEdge(
  store,
  commentsConnection,
  newComment,
  'CommentEdge'
);```
        * Insert edge after
          * ```javascript
ConnectionHandler.insertEdgeAfter(
  commentsConnection,
  newCommentEdge
);```
        * Remove from connection
          * ```javascript
ConnectionHandler.deleteNode(
  commentsConnection,
  commentId
);```
    * ## Updater functions
      * We are talking about updater functions in mutations
      * How to access data returned from BE by that mutation?
        * `const createCommentPayload = store.getRootField('createComment');`
        * This mutation had arguments as `postId` and `body` and you might be wondering how can the updater find the result in store by just mutation name?
          * It's because this updater object knowns about the context of mutation
        * **Different commands for accessing result of mutation**
          * For single return type - `store.getRootField`
          * If mutation returns list - `store.getPluralRootField`
          *  