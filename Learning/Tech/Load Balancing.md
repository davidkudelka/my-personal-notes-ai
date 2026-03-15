  * tags: #web-development #high-availability
  * notes:
    * # What is load balancing?
      * Load balancing helps us avoid all overloading of the system
      * Load balancers automatically routes the future requests to other up and running servers in the cluster. This enables the service as a whole to stay available
        * They can manage any traffic in your application. Between users and your endpoints but as well between all sorts of components in your system
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/-LOQA9koG-.jpeg]]
      * ### Performing health checks of the servers with load balancers
        * In order to intelligently route all the user requests to the running servers in the cluster, a load balancer should be well aware of its running status
          * Load balancers usual perform **health checks** in the cluster
        * It keeps list of in-service devices (and distributes traffic there), but as well out of service devices
    * # Understanding DNS
      * How DNS works - [[DNS]]
      * ## DNS load balancing
        * When a large-scale service such as **amazon.com** runs, it needs way more than a single machine to run it's services. - it's deployed across many different data centers and geographical locations across the globe
        * To spread this traffic across different data centers, we will discuss DNS load balancing, which is set up at the DNS level on the authoritative server
          * It allows return different IP addresses of a certain domain to the clients - every time it receives a query for an IP, it returns a list of IP addresses of a domain to the client
            * Client access the first IP address on the list - the other IP addresses are there in case client doesn't get response in stipulated time
          * It uses round robin algorithm to spread traffic between servers - just iterating over the list of IP addresses
        * ### Limitations
          * It doesn't take into account the existing load on the servers, the content they hold, their request processing time, their in-service status, and so on.
          * There is always possibility of a request being routed to a machine that is out of service
          * DNS load balancing despite it's limitations, is preferred by companies because it is an easy and less expensive way of setting up load balancing on their services
    * ## Load Balancing Methods
      * There are primarily 3 modes of load balancing
        * DNS Load Balancing
        * Hardware-based Load Balancing
        * Software-based Load Balancing
      * ### Hardware-based Load Balancing
        * They are highly performant physical hardware. They distribute load based on the number of existing open connections to a server, compute utilization, and several other parameters
        * They need to be maintained, updated and so on... , quite expensive to run
        * They are usually picked because of their top-notch performance
      * ### Software-based Load Balancing
        * they can be run on commodity hardware and VMs
        * There exist as well Load Balancers as a Service (LBaaS), without you having to setup anything
        * They are quite advanced compared to DNS load balancers
          * they consider - content hosted by servers, cookies, http headers, CPU and memory utilization, load on network, and so on to route traffic across the servers
          * They continually perform health checks on the servers to keep an updated list of in-service machines
          * HAProxy is one example of software load balancer - used by big names - Github, Reddit, Instagram ...
    * ## Algorithms / Traffic Routing Approaches Leveraged by Load Balancers
      * ### Round Robin and Weighted Round Robin
        * They send IP addresses of machines sequentially to the clients. Not taking into consideration CPU consumption, or any other parameter.
        * **Weighted Round Robin**
          * Based on the server's compute and traffic handling capacity weights are assigned to the IP addresses, and then based on weights, traffic is routed to them using the Round Robin algorithm
            * With this approach more traffic is routed to the machines that can handle more traffic - more effective
      * ### Least connections
        * Traffic is routed to the machine that has the least open connections of all the machines in the cluster
        * **2 ways how to implement**
          * **First** - it is assumed that all connections consume an equal amount of server resources, and the traffic is routed to the machine with the least open connections based on this assumption
            * Issue with this is that machine with the least open connections might already be processing requests demanding most of it's CPU power
          * **Second** - we are taking into account CPU utilization and the request processing time of chosen machine - machines with shortest processing time, smallest CPU utilization, and the least open connections are the right candidates to process future client requests
        * This comes in handy when the server has long opened connections. For instance, consider persistent connections in a gaming application
      * ### Random
        * Traffic is randomly routed to the servers. The load balancer may also find similar servers in terms of existing load, request processing time, and so on. Then it randomly routes the traffic to these machines
      * ### Hash
        * Source IP address and the request URL are hashed to route the traffic to the backend servers
          * It ensures client with certain IP will always be routed to the same server
          * Facilitates better user experience, because client session is already present on the device, it reduces latency
          * Even when connection drops, it can re-establish connection with same server
          * It ensures that it hits cache that already has data on it