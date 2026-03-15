  * How can we connect to the payment device?
    * App is running in the browser, so I would guess the payment device doesn't have to be connected into the same machine and the communication is running differently?
    * Do we need to store some connection secret for each kiosk user to be able to connect to the device?
  * How is it with paypal module? How is it with custom UI?
  * We can go through database and introduce Petr the architecture of our orders (we can start thinking how Kiosk app fits into that)
  * Notes from the meeting
    * Service for refreshing tokens on paypal
    * Implementation of paypal sdk to react
    * Webhook backend implementation