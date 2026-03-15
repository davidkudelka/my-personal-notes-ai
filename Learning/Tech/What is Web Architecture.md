  * notes:
    * # What is Web Architecture?
      * Web architecture involves multiple components like a *database*, *message queue*, *cache*, and *user interface*, all running in conjunction with each other to form an online service.
      * ## Client-Server Architecture
        * This architecture is fundamental building block of the web
        * Works on request-response model. The client sends the request to the server for information and the server responds with it
        * Opposite of client-server is peer-to-peer
      * ## Client
        * Hold our user interface, responsible for the look and feel of the application
        * Runs on client - mobile app, desktop, tablet or web-based console, running commands to interact with the backend server
        * **Technologies used to implement clients in web applications**
          * ReactJS, AngularJS, VueJS, jQuery etc... - all of them are using JavaScript
          * Mobile apps are using different ones
      * ## Types of Clients
        * **Thin client** and **thick client** (sometimes also called Fat client)
        * ### Thin client
          * Client that holds just user interface of the application - no business logic of any sort. For every action the client sends a request to backend server - (just like in three-tier app)
        * ### Thick client
          * Holds all or some part of the business logic. These are two-tier apps.
      * ## Server
        * **What is web server?**
          * The primary task of a web server is to receive the requests from the client and provide the response after executing the business logic based on the request parameters received from the client.
        * Besides application servers, there are also other kinds of severs with specific tasks assigned to them
          * Proxy server, mail server, file server, virtual server
        * The type of server differ depending on use case
          * For Java - Apache Tomcat or Jetty
          * For hosting static websites - Apache HTTP Server
        * ### Server-side rendering 
          * it's possible to render the user interface on the backend and then send the rendered data to the client
      * ## Communication Between the Client and the Server
        * **Request-response model**
          * The client sends request and server answers with response
        * **HTTP protocol**
          * this is the web protocol that defines how information is transmitted across the web
          * It's stateless protocol, and every process over http is executed independently and has no knowledge of previous processes
        * **Rest API and API endpoints**
          * every client has to hit a REST endpoint to fetch data from backend
          * It's interface to the outside world for requests
        * **Real world examples of using a REST API**
          * We would write a client to hit the Facebook Social Graph API which as a REST-API to get the data and then run business logic on the data
    * ## What is a REST API?
      * It's architectural style for implementing web services, they are known as RESTful web services
      * **REST API**
        * api that follows REST architectural constraints (it acts as an interface)
        * communication happens over http
        * it also enables sever to cache response to improve performance
        * It's stateless communication
          * So every time client needs to send authentication information with it
        * This way we completely de-couple client and server components
      * ### Decoupling clients and backend service
        * This way developers can have separate codebases for frontend implementations - browser, mobile and so on
        * Introducing new types of clients or modifying the client code has no effect on the functionality of the backend service - this means the clients and the backend service are decoupled
      * **Application development before the REST API**
        * Before the implementation was in one codebase making the business logic spread across different layers
      * **API gateway**
        * REST API acts like a gateway - it encapsulates business logic and handles all request, take care of authorization, authentication, sanitising the input data
    * ## HTTP Push and Pull - Introduction
      * ### HTTP PULL
        * If you send request and you receive data - this mechanism is called **HTTP PULL**
        * Important to note that every request consumes bandwidth - every request costs money, because it needs server to be involved
        * Because http protocol we don't know about past and therefore we don't know if we need to pull new data and therefore this can cause a lot of sever load
      * ### HTTP PUSH
        * To tackle pull problem we have another mechanism **HTTP PUSH**
          * The client sends the request only once and after that server keeps pushing the new updates to the client whenever they are available
        * This saves a lot of bandwidth
        * Common example is user notifications
        * Technologies that are using HTTP PUSH
          * Ajax Long polling
          * Web Sockets
          * HTML5 Event Source
          * Message Queues
          * Streaming over HTTP
      * ### HTTP PULL - POLLING with AJAX
        * 2 ways of pulling the data
          * sending HTTP GET request
          * using some polling library like AJAX
        * **AJAX - (Asynchronous JavaScript and XML)**
          * Ajax is doing long polling - it sends the request in regular intervals
          * Once data is received - particular section of user interface is updated based on the data
          * This dynamic technique of requesting information from the server after regular intervals is known as polling
      * ### HTTP Push
        * **Time To Live (TTL)**
          * normally there time to live interval which can be 30, 60 or some other value in seconds
          * if client won't receive the response in this interval - the browser kills the connection and the client has to re-send the request
          * open connections consumes resources so if connections are not being closed and there are new coming, the server will eventually run out of memory
        * **Persistent connection**
          * A persistent connection is a network connection between the client and the server that remains open for further requests and responses, as opposed to being closed after a single communication
            * This facilitates HTTP PUSH-based communication between the client and the server
        * **Heartbeat interceptors**
          * The browser is sending blank requests to the sever to prevent the browser from killing the connection
        * **Resource intensive**
          * Persistent connections consumes a lot of resources compare to **HTTP PULL**, but sometimes it is necessary
          * For example some browser-based multiplayer game 
      * ### HTTP Push-Based Technologies
        * **Web sockets**
          * Preferred connection when we need bi-directional low latency data flow from client to server and back
          * Examples - chat, messaging
          * We can keep the connection as long as possible
          * Doesn't run over HTTP, it uses TCP
          * sources - api https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API, introduction https://www.html5rocks.com/en/tutorials/websockets/basics/
        * **AJAX - Long polling**
          * Sever doesn't return response empty response, it holds until it has something to send, connection stays open bit longer. If connection breaks down, client needs to re-establish it
          * Long polling can be used in simple async data fetch, when you don't want to ping the server too often
        * **HTML5 Event-Source API and Server-Sent Events**
          * Client sends request to sever and that way sever adds it for it's pushed events
          * Every-time server notices change, it pushes message to all it's clients
          * You need to have **UI HTML5 Event-Source API** supported on the client
          * The data flow is only one direction - server to client
          * source - https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events
        * **Streaming over HTTP**
          * Streaming something by breaking into smaller pieces
          * Possible with HTML5 and JavaScript Steam API
          * used for - large images, videos
          * sources - https://developer.mozilla.org/en-US/docs/Web/API/Streams_API/Concepts
      * ### Client-Side vs Server-Side Rendering
        * **Client-side rendering - How does a browser render a web page?**
          * When browser hit's the server and get back the response it needs to render a web page
          * For that it uses
            * Browser engine
            * Rendering engine
            * JavaScript interpreter
            * Networking and the UI backend
            * Data storage etc.
          * It needs to construct the DOM tree and renders and paints the construction - this takes a bit of time
        * **Server-side rendering**
          * Rendering happens on the server side
        * **Use cases for server-side & client-side rendering**
          * It's good for delivering static content, like WordPress or good for **SEO**, because crawlers can easily read the generated content
          * Cons
            * for AJAX requests - every single time client requests the data, server is not sending just response with needed data, it needs to re-render the whole page again and send that
            * It puts a lot of bandwidth on the server
          * we can use combination - server side rendering for static pages (home page, ...) and client side rendering for all dynamic pages