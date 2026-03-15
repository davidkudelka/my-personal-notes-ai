  * Pages:
    * /manager/promos
    * /manager/promos/add
    * /mamger/promos/[promo-id]
  * List of promos
    * List of promos
    * Filters:
      * Radio button filters - selecting radio button filter reset Date picker filter
        * All - Display all promo codes
        * Active - Display all promo codes with status active and (starting date < now && end date > now)
        * Scheduled - Display all promo codes with status active and start date > now
        * Inactive - Display all promo codes with status Disabled
        * Expired - Display all promo codes with end date < now
      * Promo code name filter - filtering by promo code string
      * Date picker filter - filtering promo codes by selecting date when promo code is active (this filter resets radio button filters)
    * Promo codes form (add or update)
      * Fields:
        * Kitchen Select
          * Placeholder - Select Kitchen
          * You should be able to select multiple kitchens
          * Rules: 
            * Selecting All kitchens will unselect all kitchens previously selected
            * Selecting particular kitchen will unselect All Kitchen option if selected
        * Promo Code
          * Placeholder - e.g. SUMMERSALE
          * You should be able to enter promo code string
          * Rules: 
            * All letter you enter are transformed into capital letters
        * Type
          * Default Value - Offer % off
          * 5 Options
            * Offer % off
              * Placeholder - %
              * Rules
                * If you selected this option you have to provide value
            * Offer $ off
              * Placeholder - $
              * Rules
                * If you selected this option you have to provide value
            * Offer free Delivery
              * No input component
            * Buy X get Y
              * 2 inputs
              * 1st Placeholder - Define X value
              * 2nd Placeholder - Define Y value
              * Rules
                * If selected this option you have to specify both options
            * Free X
              * 1 Select input
              * Placeholder - Select Item
              * Rules
                * You have to select value
        * Applies To
          * 4 options
            * Entire Order
              * No Input
            * Specific Items
              * 1 Multi Select
              * Placeholder - Select Items
              * Rules
                * If selected this option you have to select at least 1 item
                * You have to first select at least one kitchen in Kitchen Select
            * All Items Except
              * 1 Multi Select
              * Placeholder - Select Items
              * Rules
                * If selected this option you have to select at least 1 item
                * You have to first select at least one kitchen in Kitchen Select
            * Specific Categories
              * 1 Multi Select
              * Placeholder - Select Items
              * Rules
                * If selected this option you have to select at least 1 item
          * Default Value - Entire Order
          * Rules
            * All Options are disabled if you select Buy X get Y, Free X or Offer Free Delivery options in Type
        * Order Method
          * 2 options - Delivery, Pick Up
          * Default value - Delivery
          * Rules
            * You can select and deselect both options
            * At least one option needs to be selected
        * Minimum Requirements
          * 3 options
            * None
              * No Input
            * Minimum purchase amount ($)
              * 1 Input
              * Placeholder - $
              * Rules
                * If selected this option, you need to provide value
            * Minimum quantity of items
              * 1 input
              * Placeholder - Quantity
              * Rules
                * If selected this option, you need to provide value
          * Default Value - None
        * Eligibility 
          * 4 options
            * Everyone
              * No Input
            * Segment groups
              * 1 Multi select component
              * Placeholder - Select Groups
              * Rules
                * If selected this option, you need to select at least 1 item
            * Specific customers
              * 1 Multi select component
              * Placeholder - Select Customers
              * Rules
                * If selected this option, you need to select at least 1 item
            * Employees
              * 1 Multi select component
              * Placeholder - Select Employees
              * Rules
                * If selected this option, you need to select at least 1 item
          * Default Value - Everyone
        * Usage Limits
          * 4 options
            * Limit to one use per customer
              * No Input
            * Limit number of times
              * 1 input
              * Placeholder - x Times
              * Rules
                * If selected this option, you need to provide value
            * Limit to day of the week
              * 1 Multi select component
              * Placeholder - Select days of the week
              * Rules
                * If selected this option, you need to select at least 1 item
            * Limit to time of day
              * 1 Multi select component
              * Placeholder - Select times of day
              * Rules
                * If selected this option, you need to select at least 1 item
          * Default Value - Limit to one use per customer
        * Active Dates
          * 2 date pickers with time pickers and 1 checkbox enabling end date
            * Start Date
              * Default Value - time now
              * Rules
                * Start date is mandatory field, you need to provide value
            * End Date
              * No Default Value
              * Rules
                * You have to select date that is > start date
      * Rules
        * All validation happens when clicking Save button
    * Promo Code Order Validation
      * Rules
        * Main Rules - if we one of the condition is not sufficient return just one error
          * Promo Needs to in Active State and Promo needs to exist otherwise returning error INVALID_PROMO
          * Promo Needs to have at least one order item that is that is from one of the kitchens in promo entity
          * Promo Needs to have startDate < now && endDate > now
        * Secondary rules - if user passes the main rules, you will get list of errors you are not sufficient in
          * Promo is having correct order method
          * Min Requirements
            * Min Amount -
            * Min Items - 
          * Eligibility
            * If promo has everyone option, this check is skipped and everyone is allowed
            * If promo has customer option you need to be customer that is in promo customer list
            * If promo has employee option you need to be employee that is selected in promo employee list
            * If promo has segment group option you need to be member of on of the segment groups specified in promo segment group list
          * Usage Limit
            * If promo has Limit to one use per customer option, you can use promo code just once
            * If promo has Limit number of times, promo can be used just this number of times by **anyone**
            * If promo has Limit to day of the week, your order needs to be in promo list of allowed day of the weeks
            * If promo has Limit to time of the day, your order needs to be in promo list of allowed times of the week
    * Promo Code Order Calculation
      * If you passed order validation you will get calculated promo discount
    * My questions:
      * Do you agree with Main Rules and Secondary Rules ?
      * Offer % off or Offer $ off is it calculated from total value of order or items that are specified in promo entity ?
      * Offer free delivery but method is pick up, should I throw error or just return 0 discount value ?
      * Buy X get Y / Free X - if we don't have these items in order, should I return error or 0 discount ?