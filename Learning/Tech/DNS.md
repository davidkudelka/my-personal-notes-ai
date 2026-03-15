  * # Understanding DNS
    * Every machine that is online have unique IP address, so it can be contacted by other devices on the network
      * IP = internet protocol - it's a protocol that facilitates the delivery of data packets from one machine to another using their IP addresses
    * ## Domain name system
      * It averts the need to remember long IP addresses to visit a website by mapping easy to remember domain names to IP addresses
        * e.g. amazon.com is a domain name that is mapped to it's unique IP address, so we don't have to type that IP address every time
      * ### How does a domain name system work?
        * When a user types in the URL of the website in their browser and hits enter, this event is known as **DNS querying**
        * Main components that make up DNS infrastructure
          * DNS recursive nameserver aka DNS Resolver
          * Root nameserver
          * Top-Level Domain nameserver
          * Authoritative nameserver
        * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/NpcewUjAdG.jpeg]]
        * **DNS Recursive server - DNS resolver**
          * Is usually managed by internet service provider and this big database is stored in data center - and managed there
          * Data centers contain clusters of servers that are optimized to process DNS queries in minimal time that is in milliseconds
        * **Root Nameserver**
          * it returns address of top-level domain nameserver in response - which for **amazon.com** is **.com**
        * **Top Level Domain Nameserver**
          * After receiving top level domain ip from root nameserver -> it sends request to fetch the details of the domain name - top level domain nameserver hold the data for domains using their top-level domains
        * **Authoritative Nameserver**
          * This server is owned by the owner of the domain name. It returns the IP address of actual website to the DNS resolver.
        * All this process is usually cached on the DNS resolver level, but as well on the client side in the browser and it has TTL - Time to Live until which it's cached
