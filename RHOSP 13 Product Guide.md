RHOSP 13 Product Guide

[[Topics to cover later]]
    - Red Hat CloudForms
    - 
[[Tips]]
    - 

1. Understanding Red Hat OpenStack Platform
   1. delivers integrated foundation to create, deploy and scale a secure public/private cloud
   2. is packaged so that available physical h/w can be turned into  cloud platform which includes:
      1. fully distributed object storage
      2. persistant block storage
      3. virtual machine management and image storage
      4. authentication and authorization
      5. integrated networking
      6. web based interface accesible to users and admins
   3. Red Hat OpenStack cloud platform IaaS cloud is implemented by a collection of integated services that 
      1. control its computing
      2. storage
      3. networking resources
   4. Cloud is managed by web-based interface which allows admins to:
      1. control
      2. provision
      3. automate resources
   5. OpenStack infrastructure is implemented by extensive API which is available to end users
   
2. Advanatages of Using RedHat OpenStack Platform
   1. scalability
   2. need basis
   3. instant response
   4. stable and agile

3. Relationship between RDO and OpenStack foundation
   1. OpenStack Foundation -- Upstream
   2. RDO - RPM distribution of OpenStack

4. Software
5. Components
      1. Horizon
         1. GUI for user administration
         2. instance creation
         3. managing networking
         4. setting access control
         5. modular design enabled dashboard to interface with other products like billing, monitoring and additional management tools
      2. Keystone
         1. provides authentication and authorization to all OpenStack Components
         2. Identity supports multiple authentication mechanisms like, username, password credentials, token-based systems and AWS style logins
      3. Neutron
         1. creation and management of virtual networking infrastructure
         2. infrastructure elements include subnetworks, networks and routers
      4. Octavia(loadbalancing)
         1. provides LBaaS implementation for director based installation
         2. enables multiple provider drivers
         3. reference provider driver Amphora is an open-source , scalable, highly available load balancing provider.
         4. it accomplishes its delivery of loadbalancing services by mapping a fleet of virtual machines collectively known as Amphorae - which it spins up on demand 
      5. Cinder
         1. provides persistant block storage management of virtual hard drives
         2. enables users to create, delete and manage attachment block devices to servers
      6. Nova
         1. core of OpenStack Cloud
         2. provides virtual machines on demand
         3. nova schedules VMs to run on a set of nodes by defining drivers that interact with the underlying virtualization mechanisms
         4. and by exposing the functionality to other OpenStack Components
      7. Glance
         1. registry for virtual disk images
         2. users can add new images
         3. take snapshot of existing server and store and add as image 
         4. these snapshots can be used as backups or templates for new servers
      8. Swift
         1. provides HTTP accessible storage system for large amount of data for static entities (videos, photos, VM images)
         2. objects are stored as binaries on underlying filesystem along with metadata in extended attributes of each file.
      9. Ceilometer
         1.  telemetry provides user-level usage data for OpenStack based clouds.
         2.  data can be used for billing, monitoring or alerts
         3.  can collect data from notifications send by existing OpenStack components 
         4.  or by polling OpenStack infrastructure resource like libvirt
      10. Heat
          1.  Orchestration provides templates to create and manage cloud resources such as network, storage, instance or applications
          2.  templates are used to create stacks, which are a collection of resources
      11. Sahara
          1.  enables provision of Hadoop clusters
      12. Ironic
          1.  provides bare metal provisioning which enables user to provision physical   machines from a variety of hardware vendors with hardware specific drivers
          2.  ironic integrates with nova to provision bare metal machines the same way that virtual machines are provisioned
      13. Manila
          1.  provides shared filesystem that nova instances can use
          2.  basic resources offered by shared filesystems are shares, snapshots and shared networks
      14. Designate (DNS-as-a-service)
          1.  tech preview in RHOSP 13
      15. Barbican
          1.  Its a key manager service and is a REST API 
          2.  its designed for secure storage, provisioning and management of secrets such as passwords, encryption keys and X.509 certs.
          3.  This includes keying materials like, Symmetric keys, Asymmetric Keys, certs and raw binary data
      16. RHOSP director   
          1.  A toolset for installing and maintaing a complete OpenStack environment
          2.  Its based on TripleO
          3.  Takes advanatage of OpenStack components  to install fully operational OpenStack environment, including components that provision and control baremetal systems to use as OpenStack nodes
          4.  provides a simple method for installing and provisioning a lean and robust environment
          5.  uses 2 main concepts, Overcloud and Undercloud
          6.  Undercloud installs and configures Overcloud  
      17. OpenStack HA  
          1.  to keep OpenStack env up and running
          2.  director lets you create configs that offers HA and LBaaS across all major services in OpenStack
      18. operational tools (optional suits)
          1.  centralized logging
          2.  Availability monitoring
          3.  Performance monitoring
      
  6. Integration
    OpenStack can be integrated with 3rd party software -->  https://catalog.redhat.com/#/ecosystem/Red%20Hat%20OpenStack%20Platform?sort=sortTitle%20asc&category=Software
    
   
  
    


   
   
   

[//begin]: # "Autogenerated link references for markdown compatibility"
[Tips]: tips "Tips"
[//end]: # "Autogenerated link references"