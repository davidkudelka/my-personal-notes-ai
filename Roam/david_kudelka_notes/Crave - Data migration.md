  * tags: #data-migration #data #crave
  * content:
    * ## Meridian
      * All current data available for meridian will be stay the same
      * Menu categories
        * sheet for with current menu categories - https://docs.google.com/spreadsheets/d/17usPuVGfNfDhBD9y6QwFbyyZgq-UmJdDvcgyddwAWxk/edit#gid=0
        * After the data migration all categories with same name, type and category type will merged into single menu category - connections to kitchen menu items will be kept so there won't be any more work needed
      * Extras
        * sheet with current meridian extras - https://docs.google.com/spreadsheets/d/1jtMUcBN4DMVYwssoJMLAFJ90mtBoDAz1CdFNP535Mc8/edit#gid=0
        * release won't affect extras for Meridian facility
      * Facility
        * here is link to sheet with facilities - https://docs.google.com/spreadsheets/d/17usPuVGfNfDhBD9y6QwFbyyZgq-UmJdDvcgyddwAWxk/edit#gid=1904440902
        * Please check
          * Address of both locations (mainly downtown)
          * Confirm that both locations support DELIVERY and PICK_UP on release date
          * Delivery times for both locations
        * We will need from you
          * logo image for both facilities
          * operation hours for both facilities
          * Delivery eligible areas for Downtown location (those are locations outside of normal delivery zone that we still wants to support)
    * ## Downtown
      * We will create basic data sets for second facility
      * Collected data from Evan
        * Menu categories
          * those menu categories will be in the database on release data - https://docs.google.com/spreadsheets/d/17usPuVGfNfDhBD9y6QwFbyyZgq-UmJdDvcgyddwAWxk/edit#gid=1079337182
        * Extras
          * those extras will be in database on release date - https://docs.google.com/spreadsheets/d/1jtMUcBN4DMVYwssoJMLAFJ90mtBoDAz1CdFNP535Mc8/edit#gid=622168861
        * Facility - https://docs.google.com/spreadsheets/d/17usPuVGfNfDhBD9y6QwFbyyZgq-UmJdDvcgyddwAWxk/edit#gid=1904440902
          * please check the data
        * Stations
          * this list of stations will be imported on release date - https://docs.google.com/spreadsheets/d/17usPuVGfNfDhBD9y6QwFbyyZgq-UmJdDvcgyddwAWxk/edit#gid=1719657423
        * Kitchens
          * No kitchens will be provided for the release date
          * Credential for those kitchens won't be provided (Restaurant owner and restaurant employee)
        * Kitchen menu items
          * No kitchen menu items will be provided for the release date
        * Menu Schedules
          * No menu schedules will be provided for release date
    * ## Common
      * Promos
        * we need to resolve those promo codes
          * ["CATER5","CRAVEHH","LUNCH"] , since they have usageLimit set to Time of day and time of day limitation will be removed
          * Bri in charge of communicating all other changes
      * Users
        * current user roles
          *   CUSTOMER
            * will be available to order from both facilities
          *   CATERING_CUSTOMER
            * no changes
          *   KIOSK_CUSTOMER
            * for signing to kiosk application, will be able to access just Downtown location
          *   RESTAURANT_OWNER
            * TBD
          *   RESTAURANT_EMPLOYEE
            * TBD
          *   CUSTOMER_SUPPORT
            * Should have both facilities - support@cravedelivery.com ?
          *   CRAVE_EMPLOYEE
            * [
              * 'cs7@cravedelivery.com',
              * 'cs8@cravedelivery.com',
              * 'cs9@cravedelivery.com',
              * 'cs10@cravedelivery.com',
              * 'cs11@cravedelivery.com',
              * 'cs12@cravedelivery.com'
            * ]
            * are those accounts used, if yes should they have both facilities?
          * ADMINS
            *   FACILITY_ADMIN
            *   CORPORATE_ADMIN
            * List of current admins and to which facilities they should have access
              * [[Crave - admin json]]
              * which accounts should be corporate admins and which normal admins (for normal admins what faciltiies they should have assigned)