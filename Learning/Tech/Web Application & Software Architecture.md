  * notes:
    * ### Objectives
      * Understand concepts, components, and technology trade-offs involved in architecting a web application
      * Learn various architectural styles such as the client-server, peer to peer decentralised architecture, the fundamentals of data flow in a web application, concepts like scalability, high availability and much more
      * Master the techniques of picking the right architecture and the technology stack to implement a use case
    * ## Different Tiers in Software Architecture
      * ### **What is a tear?**
        * Separation by components
          * Examples
            * Database, Backend application server, User interface, Messaging, Caching
        * **Single-Tier Applications**
          * A single-tier application is an application where the user interface, backend business logic, and the database all reside in the same machine
          * Typical examples - MS Office, PC Games or an image editing software like Gimp
          * Advantages
            * No latency, every component is in the same machine
            * Real performance of a single-tier app largely depends on how powerful the machine is and the software's hardware requirements
            * Higher data safety - you are not sending data over the internet
          * Disadvantages
            * No control over the application - user must download new features, you can't disconnect him
            * Performance is inconsistent, since it depends on the users machine
        * **Two-tier Applications**
          * Includes server and client. Client = user interface and business logic in one machine, Backend server = database (database is hosted by business and have control over it)
          * Important - business logic is still on client side
          * Can be used for todo apps or some browser games so it doesn't make too many network calls for different things
        * **Three-tier Applications**
          * User interface, application logic, and the database all lie on different machines and, thus, have different tiers. They are physically separated
          * React app -> node js server -> PostgreSQL - is example of three-tier app
        * **N-tier Applications (Distributed applications)** 
          * Application that has more than three components involved
          * Component examples
            * Cache, Message queues for asynchronous behaviour, load balancers, search severs for searching through massive amounts of data, components involved in processing massive amounts of data, components running heterogeneous tech commonly known as web services etc.
          *   Why the need for so many tiers?
            * Single responsibility and separation of concerns
          * Single responsibility
            * Giving the component one responsibility and letting it execute perfectly (saving data, uploading image, running app logic)
            * You can have different repo's for different components
          * Separation of Concerns
            * Keeping the components separate makes them reusable. Different services can use the same database, messaging server or any component as long as they are not tightly coupled with each other.
          * Difference between layers and tiers
            * layers represent the conceptual organisation of the code and its components, whereas, tiers represent the physical separation of components