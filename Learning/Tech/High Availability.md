  * tags: #web-development #high-availability
  * notes:
    * # What is high availability?
      * The ability to stay online despite having failures at the infrastructural level in real-time
      * It improves the reliability of the system and ensures minimum downtime
      * ### How important is high availability to online services?
        * There are businesses that just can't go down at all, they must remain online, because a lot of things depends on it - (businesses like stock-market, hospitals, aircraft systems)
        * To meet the high availability requirements, systems are designed to be **fault-tolerant** and their components are made **redundant**
      * ### Reasons For System Failures
        * **Software crashes**
          * software mistakes, we know this as BSOD on windows, games are crashing so do cloud nodes
        * **Hardware failures**
          * overloaded CPU or RAM, hard disk failure, network outages
        * **Human errors**
          * Flawed configuration - google made a tiny network config error and it took down almost half of the internet in Japan
        * **Planned downtime** 
          * Besides crashes, we have as well planned downtimes like system upgrades, patching software and so on...
    * ## Fault tolerance
      * There are few approaches how to make system HA, one important aspect is fault tolerance
      * ### What is fault tolerance
        * Fault tolerance is a systems ability to stay up despite taking hits
        * It means that system is running on multiple instances/nodes and when one goes down system is still able to respond with other healthy instances/nodes
        * Example is social network - it runs different services for image upload, comments, and instant messaging - so when one goes down others are still working - this is known as **soft fail**
      * ### Designing a highly available fault-tolerant service - Architecture
        * To achieve this you can split system into micro-services
        * Advantages of microservices
          * Easier management
          * Easier development
          * Ease of adding new features
          * Ease of maintenance
          * High availability
        * Every micro-service is running different features of an application such as image upload, comment, instant messaging
        * So even if a few services go down, the application as a whole is still up
    * ## Redundancy - Active-passive HA mode
      * Redundancy is duplicating the components or instances and keeping extras on standby to take over in case the active instances go down. It is the fail-safe, backup
      *  This approach is as well known as active-passive HA mode. Initial set of notes are active, and a set of redundant nodes are passive, on standby
        * For GPS, aircrafts, and communication satellites it is important to have zero downtown - those are using redundant components
      * ### Getting rid of single points of failure
        * Distributed systems became popular, because you are reducing risks of your application 
        * Single points of failure at the application level mean bottlenecks. We should detect bottlenecks in performance testing and get rid of them
      * ### Monitoring and Automation
        * System should be **always** real-time monitored to detect bottlenecks or single point of failures
        * Automation enables instances to self-recover without any human intervention - it gives the instances the power of self-healing
        * Systems became intelligent enough to add or remove instances on the fly as per requirements
        * It reduces **human error**
    * ## Replication - Active-active HA mode
      * replication means having a number of similar nodes running the workload together
      * there are no standby or passive instances
      * when one node goes down, the remaining nodes bear the load of the service - think of this as load balancing
      * ### Geographical distribution of workload
        * For natural disasters, regional power outages, big-scale failures - data center workloads are spread across different data centers across the world
        * Reduce point of failure for data centers and shortens latency
        * Businesses often use multi-cloud platforms to deploy their workloads -> increase of 
    * ## High availability clustering
      * also known as **fail-over cluster**, contains a set of nodes running in conjunction with each other that ensures high availability of the service
      * The nodes are connected with private network called **heartbeat network**, that continuously monitors the health and the status of each node in the cluster
      * There is as well shared memory - Zookeeper is example of product to do that
        * To ensure the availability, HA clusters use several techniques such as *disk mirroring/Redundant Array of Independent Disks (RAID)*, redundant network connections, redundant electrical power etc. The network connections are made redundant. So, if the primary network goes down the backup network takes over.
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/mGJvhoFLoM.jpeg]]