#Clustering

## High Availability
    - Vital servers in server will be protected 
    - essential even when running Virtual machines
    - HA makes sure services are restarted after a failure of either the service or the host currently hosting the service


1. Types of clusters
   1. HA cluster
   2. Load balancing clusters
   3. High Performance clusters
2. HA cluster
   1. Multiple nodes, to provide Availability of vital services, i.e. the nodes are going to work together to guarantee the Availability of the service
   2. Multiple layers
      1. Lower layer, this is where the communication happens, call this layer the Membership layer, this layer detects if the nodes are still available
      2. Resource management layer, takes care of the availabilty of the resources
      3. Here there are 2 failure domains, 
         1. One of the node in the cluster goes down
            1. If this happens, the Membership layer detects the failure, and if it affects the resource, it will be able to migrate the resource to next available node
         2. If the resource goes down the resource management knows about it because of monitoring (the resource management layer checks the availability of the resources) and makes sure the resource is restarted somewhere else.
   3. In HA cluster the resource will be running on a specific node, if something goes wrong, the resource is restarted on another node.
   4. HA cannot guarantee a 100% uptime of a resource. that is , it detects failure and brings up the service. so there is some unavailability of service. This is true if you configure basic Failover HA cluster
   
3. Load balancing clusters
    1.  They work in a different way compared to HA clusters
    2.  They will have backend server farm, it evenly disrtibutes the incoming workload among these backend servers. The loadbalancer works as a fronend for these backend servers.
    3.  The client connects to the loadbalance not the backend servers, the load balancer , the LB uses its algorithms and protocols to distribute the workload among  the backend servers.
    4.  The purpose is different for LB clusters compared to HA cluster
        1.  LB adds scalability, makes sure the client requests are dealt in a faster way 
    5. The loadbalancer can detect the failure of any of the backend servers and it will stop sending traffic to that failed server, likewise we can scale the number of backend servers and by making config changes to the LB node, we can add new backend server to the cluster and start sending traffic to the new server
    6. The LB node itself will need some HA if the node goes down,  thats the reason LB software is very often integrated as a resource in the HA cluster
 
 4. High Performing Clustering 
    1. Here multiple nodes will work on 1 task, using Single Site Image (ssi), ssi is like a virtual computer , from the connected H/w the virtual computer makes sure it has as much as resources like CPU and RAM is added to it to work.
    2. Different levels of HPC
       1. At application level, 
       2. At a computer level, uses a virtual HPC OS that allows to monitor the task is dealt with as fast as possible.
    3. Used in Universities, in places where large calculations are needed in a fast way
    4. Provides alternativce to buying Mainframe
    5. provisioning and deprovisioning of nodes is easy
 
 5. Creating a HA cluster
    1. Needs atleast 3 nodes, for majority and a higher level of guarantee that atleast one server is available to run the service.
    2. The HA cluster will have a service on top that will service the actual service, for eg, if the main service is a web server, the HA will have a service that will service the web server
    3. The service (the web service not the web server) itself will have an ip address. The cluster will make sure , the `IP address` plus the `web server` is failing over in the cluster.
    4. the actual web server service will be running on all nodes in the cluster , that is even if the webserver is running through the cluster,  if the cluster decides to run the web service in a particular node in the cluster, that node should have the service installed. 



