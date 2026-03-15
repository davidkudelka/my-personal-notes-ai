  * tags: #react #conference #talk #local-storage
  * author: [[Ebenzer Don]]
  * notes:
    * # Dexie.js for offline data storage in React Apps
      * ### Link to Article
        * https://blog.logrocket.com/dexie-js-indexeddb-react-apps-offline-data-storage/
      * ### Problem with localStorage
        * Only string data
        * 5mb limit across major browsers
        * Vulnerable to XSS attacks
        * It's synchronous
      * ### IndexDB
        * **Plus**
          * it's asynchronous
          * storage limit depnds on users disk space
          * store different data types
          * it's structured
          * data can be queried
        * **Minus**
          * Not supported on some legacy browsers
          * can be complex to use
          * poor queries
      * ### Dexie.js
        * Library to help you work with IndexDB
        * Exposes react hooks for good implementation in react components