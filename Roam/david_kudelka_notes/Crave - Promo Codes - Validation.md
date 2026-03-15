  * Todos #crave-promo-todo ^HL-Zlh4PC
    * [x] Refactor validateOrder function
      * ~~Refactor orderValidateFunction~~
      * [x] Refactor promoValidate function
    * [x] Change enum of "methods" in db
      * Research
      * Change
    * [x] Create correct errors
    * [x] Implement segment groups
      * [x] Ask alex about the feature
      * [x] Implement solution
    * Multiple Errors issue
      * [x] Ask Jamie about the errors
      * [x] Implement solution
    * [x] Write tests for promo validation
      * Validation #crave-promo-todo-validation
        * [x] Promo
        * [x] Valid Since
        * [x] Valid Till
        * [x] Order method
        * Requirements
          * [x] MIN_AMOUNT
          * [x] MIN_ITEMS
        * Eligibility
          * [x] Employee
          * [x] Customer
          * [x] Segment
        * Usage Limit
          * [x] Once
          * [x] Number of times
          * [x] Day of week
          * [x] Time of Day
      * Calculation #crave-promo-todo-calculation
        * [x] Free delivery
        * [x] Discount amount
        * [x] Discount percentage
        * [x] Free X
  * Input
    * addressId [id]
    * timeslotId [id]
    * items [array of items]
    * promoCode [string]
    * tip [float]
    * utensilsCount [int]
    * deliveryOption [MEET_AT_DOOR / LEAVE_AT_DOOR]
  * Flow
    * {[x]}} validatePromo function
      * {[x]}} Check Active Dates
      * {[x]}} First check order method (if it applies)
      * {[x]}} Check minimum requirements
      * {[x]}} Check eligibility
      * {[x]}} Check usage limits
    * {[x]}} applying discount
      * {[x]}} if % get percentage off (From which amount)
      * {[x]}} if $ dollars off 
      * {[x]}} Free delivery so promo discount same as delivery cost
      * {[x]}} Buy X get Y -> check items and discount price of the item
      * {[x]}} Free X -> discount price of item
  * Questions for meeting
    * [x] Should I just integrate it to the validate order function or do we need more stuff
    * [x] What we want to do with old promo codes, we can run script and try to change them for the new structure
    * [x] There will be new order validation errors (do I need to sync with Jamie or someone ??)
    * [x] If I have percentage discount from which amount am I making discount ( I guess the same way and it's subtotal)
    * [x] There can't be bigger discount than price of the item (does apply to delivery or just cost of the product)
    * [x] Should I return type of discount
      * plus what item was for free
      * or percentage of discount
  * Checks:
    * If the promo is Invalid return error invalid promo
    * If the promo doesn't have any items return error no items
