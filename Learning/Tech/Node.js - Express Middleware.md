  * tags: #middleware #express #nodejs
  * notes:
    * Express has several different types of middleware
      * Application-level middleware
        * ```javascript
var express = require('express')
var app = express()

app.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})```
      * Router-level middleware
        * ```javascript
var express = require('express')
var app = express()
var router = express.Router()

// a middleware function with no mount path. This code is executed for every request to the router
router.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})

// mount the router on the app
app.use('/', router)```
      * Error-handling middleware
        * Define error-handling middleware functions in the same way as other middleware functions, **except with four arguments instead of three**, specifically with the signature (err, req, res, next))
        * ```javascript
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})```
      * Built-in middleware
        * [express.static](https://expressjs.com/en/4x/api.html#express.static) serves static assets such as HTML files, images, and so on.
        * [express.json](https://expressjs.com/en/4x/api.html#express.json) parses incoming requests with JSON payloads. **NOTE: Available with Express 4.16.0+**
        * [express.urlencoded](https://expressjs.com/en/4x/api.html#express.urlencoded) parses incoming requests with URL-encoded payloads. **NOTE: Available with Express 4.16.0+**
      * Third-party middleware
        * ```javascript
var express = require('express')
var app = express()
var cookieParser = require('cookie-parser')

// load the cookie-parsing middleware
app.use(cookieParser())```