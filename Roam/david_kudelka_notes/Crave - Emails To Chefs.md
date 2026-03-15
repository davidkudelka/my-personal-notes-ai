  * tags: #crave
  * notes:
    * So we will need some scheduler running every day on each chefs account and checking how many orders they have in advance
    * Database schema of the settings
      * id
      * orderNumber: boolean
      * orderDetails: boolean (quantity, menu items)
      * beltTime: boolean
      * deliveryDate: boolean
      * userId ???
    * If this will be connected to the user we will be saving it on user model
    * We will have to setup endpoint for scheduler
  * questions:
    * To what account is this attached to?
      * Do we need to create new user role for chefs or is it going to be on restaurant owner?
    * How to setup scheduler?
      * Answer:
    * Is there some special protection for the endpoint?
      * Answer: there should be but it seems like we haven't setup any protection yet
    * How to send emails?
      * There is mailingService in the context and I will just send custom data in there