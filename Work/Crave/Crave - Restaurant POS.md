  * # Pages
    * ## Login page
      * What's on the page
        * Input for name
        * Input for password
        * Login button - logs in to the system
        * Forgotten password
      * Mutations
        * login
      * Queries
        * me
    * ## Forgotten Password Page
      * What's on the page
        * Email input
        * Send reset email button
      * We already have those mutations from catering and admin portal
    * ## Tables page
      * List of tables, you can either add, delete or update table - CRUD
      * Table is either empty or has active order
      * Queries
        * Tables - argument facility id
      * Mutations
        * Create
        * Update
        * Delete - only if there are no active orders on the table
        * Reassign tableOrder to different table ??
    * ## Table Detail Page
      * List of current items in order
        * Grouping of the items as they go
      * Add more items
        * List of menu items, separated by kitchens
        * Same as catering, you can add extras as well
        * Confirmation button which puts items into KDS and Order - at this point I am creating normal  TableOrder connection
          * Sends items to the kitchen, add items to the order
      * Button to complete order
    * ## Order Summary Page
      * User is able to group items, and then pay just part of the order
        * Adding promo for each subsection of order - creating bills
      * Completes order - removes order from Table
    * ## Order Status Screen Flow Page
      * List of orders for James restaurant
      * Order detail - Table Order
  * ## Database schema
    * ### Table
      * id - string
      * name - string
      * notes - string
      * orders - TableOrder[]
      * GraphQL
        * activeOrder - Order 
    * ### TableOrder
      * id
      * status
      * table
      * isJames - boolean
      * orders - Order[]
      * kitchenTickets - KitchenTicket[]
    * ### Order
      * id
      * subtotal              Float
      * delivery              Float
      * tax                   Float?
      * fee                   Float?
      * taxFees               Float
      * total                 Float
      * tip                   Float
      * discount              Float
      * menuItems - OrderMenuItems
  * Question
    * Splitting the order ??
    * How should work returning items ??