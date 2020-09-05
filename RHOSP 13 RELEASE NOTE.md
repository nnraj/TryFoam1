# RHOSP 13 RELEASE NOTE

[[ Topics to cover later]]
-L3 routed spine-leaf network

- composable networks
- RT-KVM
- Instance HA
- What are Huge pages
- What does collectd do
- What is OpenDaylight
- What is LUKS (to encrypt disks attached)
- What is  AES in CTR mode
- What is keycloak-httpd-client-installation



[[Tips]]

1. [RHOSP Life Cycle]([https://link](https://access.redhat.com/support/policy/updates/openstack/platform/) "RHOSP 13 Life Cycle")
2. [Installing and Managing Red Hat OpenStack Platform]([https://link](https://access.redhat.com/articles/2477851))
3. [Deployment Limits for Red Hat OpenStack Platform]([https://link](https://access.redhat.com/articles/1436373))
4. [Database Size Management]([https://link](https://access.redhat.com/articles/1553233) " Database Size Management for RHEL OSP (5 & 6)" )
 1.  [Certified Drivers and Plug-ins]([https://link](https://access.redhat.com/articles/1535373) "Component, Plug-In, and Driver Support in Red Hat OpenStack Platform")
 2.  
### More Notes from Installing and Managing Red Hat OpenStack Platform
- Director is must for RHOSP 7 and above for support or SE needed -- valid only for  new deployments
  - This rule does not apply retroactively to existing deployments
  - Does not apply to partners which are embedding OpenStack in a larger solution that has its own installer.
  - For exceptions , CU needs to reach out to support team, they will review the request for a SE.
  - Regardless of deployments methods, essential life-cycle management activity such as manual installation of bug-fix (RHBA) and Security (RHSA) updates is always supported in RHOSP and all Red Hat products


### Director
 - offers the most advanced and flexible method of installation
 - including use of automated platform-wide upgrades and updates
 - Its built upon upstream, fully open source OpenStack projects.
 - Offers an enterprise tool for deployments and orchestration, including high availability.

### RHEL OSP installer -- EOL no longer supported
### Packstack -- all-in-one, small POC upto 3 servers, does not require enterprise-level configurations, such as HA. -- NOT Recommended
### Manual -- Only supported in very special cases, if Director installation is possible then it is recommended over manual installer.
### Ansible
  - Currently ansible handles a portion of installation process. In future, Ansible will be used extensively for installation.
  - Director leverage Ansible integration in :
    - deployments
    - minor updates
    - major updates
    - pre-deployment validations
    - many other areas 


2.2 Containers
  - Fully containerized services for Overcloud

2.3 Bare Metal services
  - L3 routed spine-leaf network 
    - capability to define mulitple networks for provisioning and introspection 
    - This feature, in conjuction with composable networks allows users to provision and configure complete L3 routed spine-leaf architecture for overcloud.
  - Red Hat Virtualization Driver
    - Ironic service includes a driver (staging-ovirt)  to manage virtual nodes within a Red Hat Virtualization Environment

2.4 Ceph storage
  - Red Hat Ceph Storage 3.0 support
    - Support for Red Hat Ceph Storage 3.0 (luminous)included with RHOSP 13
    - Above said version is the default deployed version and default supported version of Ceph
    - Ceph now supports rolling upgrades from 2.x to 3
    - Upgrading to new OpenStack release also upgrades Red Hat Ceph Storage to 3.0 if your ceph cluster was deployed using Director
 
  - Scale our Ceph Metadata server and Rados Gateway nodes
 
  - Manila CephFS storage with NFS -- Shared File System service (manila)
    - NFS-Ganesha servers operating on Controller nodes are used to export CephFS to tenants with HA
    - Dedicated NFS gateway interface for each tenants, this feature is fully integrated with Director

  - Enhanced multiple Cinder Ceph pools support
    - RBD (Rados block device)  can be mapped to differernt pools within the same Ceph cluster (CinderRdbExtraPools)
    - New RBD backend is created for Ceph pool associated with this parameter.
  
  - RBD mirror director with ceph-ansible
    - RBD mirror is deployed as a container using ceph-ansile with Red Hat Storage 3.0
    - RBD mirror pulls image updates from a remote cluster and applies them to the image within a local cluster
    - 

2.5 Compute 
  - Real-Time KVM integration
    - RT-KVM with compute service is now fully supported
    - Benefits
      - low average latency  for system calls
      - Precision Time Protocol (PTP) support in guest  for accurate clock sync

2.6 High availability.
  -  Now deploy and configure Instance HA with director
  -  Director integration is availabile only from RHOSP 13, to upgrade from previous versions to 13, including FFU, you must first manually disable Instance HA 

2.7 Metrics and Monitoring
 - collectd 5.8 integration
   - ovs-stat -- This plugin collects stats of OVS connected bridges and interfaces
   - ovs-events -- 
     - this plugin monitors the link status of Open vSwitch connected interfaces
     - dispatches the values to collectd
     - sends noticification whenever link state change occurs in OVS
   - hugepages -- This plugin allows monitoring for free and used hugepages by numbers, bytes, or percentage on a platform
   - intel-rdt (Intel Resource Director Technology)
   - libvirt plugin extension

 - collectd and gnocchi integration
   -  the collectd-gnocchi plugin sends metrics to gnocchi
   -  by default, it creates a resource type named collecd and a new resoruce for each host monitored.

- Support `sensu` with multiple RabbitMQ servers
- Intel Resource Director Technology / Memory Bandwidth Monitoring support
- Removal of Telemetry  API and ceilometer-collector
  - Telemetry API service is replaced by:
    -  OpenStack Telemetry Metrics (gnocchi)  
    -  Openstack Telemetry Alarming (aodh)
  - Ceilometer-collector service is replaced by ceilometer-noticification-Autogenerated
  - Ceilometer as a whole is not depricated, just the Telemetry API service and the ceilometer-collector service.

2.8 Network Functions Virtualization
  - Real-Time KVM compute role  for NFV workloads

2.9 OpenDaylight

2.10 OpenStack Networking
  - Octavia LBaaS
    - Octvia is fully supported , is an official OpenStack project that provides load balancing capability
    - intended to replace HAProxy based implementation
    - implements LBaaS v2  API 
    - includes a reference load balancing driver that provides load balancing with amphora which is implemented as a compute VM
  - OVN
    - fully supported
    - is a Open vSwitch based network Virtualization for supplying network services to Instance
    - fully supports neutron API
   
2.11

  - Barbican -- secrets manager, barbican API + command line to centrally manage certs, keys and passwords used by OpenStack.
  - Barbican - support for encrypted volumes -- used for block storage encryption keys. Uses LUKS to encrypt disks attached to instances including boot disk. 
  - Barbican - glance image signing  -- Can configure image service to verify the uploaded image has not been tampered with. The image is singed with a key that is stored in barbican, with the image beeing validated before use.  
  - Integration with Policy Decision Points (PDP)
  - AIDE intrution detection is tech preview

2.12 Storage
  - containerized deployment of Block Storage service (cinder) is now default
  - If using backend for these services that has external installation dependencies, then must obtain vendor specific containers for your deployment
 
  - Block Stoage - Multi-back end availability zones.
 
  - Block Storage - OpenStack Key Manager support
    - configure keymanager in director
    - new keys can be added by users with admin or creator roles by keystone
 
  - Block Storage - RBD driver encryption support
    - RBD driver now handles block storage service volume encryption using LUKS
    - provides capability to encrypt volume on RBD 
    - barbican is required to use RBD driver encrytption 
    - only supported for block storage service.
 
  - Image service - image signing and verification support
    - Glance now provides signing and signature validations of bootable images using barbican
    - image signatures are are verified prior to storing image 
    - must add encryption signature before uploadingthe image to glance
    - this signature is used to validate the image upon booting.
 
  - Object storage - At-Rest encryption and OpenStack Key Manager support 
    - Swift can store objects in encrypted form using AES in CTR mode
    - key stored in barbican 
    - once encryption is enabled, the system creates a single key to encypt all objects in the cluster.
    - helps maintain Security compliance
 
  - Shared File System - Containerized deployment of the Shared File System service.
    - Containerzied deployment of the Shared File System service is default now.
    - if using backend for these services that has external installation dependencies, obtain vendor specific container for your deployment

  - Shared File System - Manila CephFS storage with NFS.
    - Tenants are isolated from one another and may only access CephFS through the provided NFS gateway interface.

2.13 Tech Previews
  - Ansible-based configuration (config download)
    - Director can generate a set of Ansible playbooks using overcloud plans as basis.
    - This changes the overcloud configuration menthod from heat to Ansible-based
    - features like upgrades, use this feature as part of their process.
    - usage outside of these supprted areas is not recommended for prod and only avaiable as tech preview

  - OVS hardware offload
    - Open vSwitch hardware offload accelarates OVS by moving heavy processing to hardware with SmartNICs.
    - This saves host resources by offloading the OVS processing to the SmartNIC 

  - Previous Tech preview list which are still tech preview 
    - Benchmarking service -- Rally benchmarking tool
    - Cells -- nova cells, for dividing computing resources, Cells v2, no support for multi cell yet, `cell of one` is the default configuration
    - DNS-as-a-Service (DNSaas) -- designate, integrates with keystone, allows automated DNS records, includes integratin with Bind9 back end.
    - Firewall-as-a-Service (FWaaS) -- adds perimeter firewall mgmt to neutron, uses iptables to apply firewall policy to all virtual  routers within a project
      - sec grp operates at  instance level
      - FWaaS oprates at perimeter level filtering traffica the neutron server.
      - Google Cloud storage backup driver (Block storage) 
        - Cinder can use google cloud storage for storing volume backups.
      - Link aggregation of Baremetal nodes.
        - allows to configure bonding to support failover and load balancing.
        - specific h/w switch 


   













[[To check]]

[//begin]: # "Autogenerated link references for markdown compatibility"
[Tips]: tips "Tips"
[To check]: to-check "To Check"
[//end]: # "Autogenerated link references"