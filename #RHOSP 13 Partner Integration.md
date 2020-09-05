#RHOSP 13 Partner Integration

## Chapter 1.  Introduction
        - to help Partner in their effors to Integration of their solution with RHOSP director
        - broad benefits in optimization of resources, reduction in deployment time & reduction in lifecycle mgmt costs
    - Partner Integration Requirements
        -  as a first step, the partner solution must first be certified with RHOSP --> https://access.redhat.com/documentation/en-us/red_hat_openstack_certification/1.0
  
## Chapter 2.  Architecture
    - Core components
        - The director advocates the use of native API to configure, deploy and manage OSP env
        - Major benefits of using API
          - well documented
          - undergo extensive testing upstream
          - mature
          - makes understanding of how director works easier for those with foundational knowledge of OSP 
        - Director is a tool set for Installing and managing  complete OSP env.
        - director is primarliy based on project TripleO - OpenStack-On-OpenStack
        - director provides a simple method for Installing a complete RHOSP env that is lean and robust.
        - director use 2 main concepts 
          - Undercloud
            - single system OpenStack env, a management system that can create a production-level cloud for workloads to run.
          - Overcloud
        - director ships with tools, utils and example Templates for creating Overcloud
        - director captures:
          - Configuration data
          - parameters
          - network topology
          and uses this info in conjuction with components like ironic, heat and puppet to orchestrate Overcloud installation

      - Ironic
        - provides dedicated bare metal hosts to end users through self-service provisioning
        - director uses ironic to manage bare metal hardware in Overcloud
        - Ironic has its own native API for defining bare metal nodes.
        - nodes must be registered with ironic using specific driver.
        - main supported driver -- IPMI for power management function
        - ironic also contains vendor specific dirvers like iLo, UCS, DRAC. 
        - along with power management ironic also collects hardware info from nodes in a process called introspection.
        - director uses this info to match the nodes to various predefined roles like controller, compute or storage node. 
        - involed components:
          - Ironic RESTful API
          - Ironic Conductor
          - Database
          - dirvers 
        - Partner wishing to have director support for their hardware will need to have their driver coverage in ironic.
  
      - Heat
        - acts as an application stack Orchestration engine
        - allows organizations to define elements for a given application before deploying it in cloud
        - involves creating a stack Template that include a number of infrastructure resources like
          - instances
          - networks
          - storage volumes
          - floating IPs
        - along with a set of parameters for Configuration
        - heat creates them based on given dependency chain, monitors them for availability and scales them where necessary.
        - these templates enables application stacks to become portable and achive repeatable results.
        - director uses native OpenStack Heat APIs to provisioning and managing the resources associated with deploying Overcloud
        - this includes precise details such as 
          - defining number of nodes to provision per role
          - software components to configure for each nodes
          - order in which the director configures these components and node types.
        - director also uses heat for troubleshooting a deployment and making changes post-deployment with ease.
        - involed components of Orchestration service
          - openstack-heat-api
          - openstack-heat-engine
          - Orchestration DB
        - heat consumes templates included with the director to facilitate creation of Overcloud, which includes calling ironic to power the nodes.
        - using standard heat stack tools we can view the resources and its status of an in progress Overcloud
        - for eg: we can use heat tools to display Overcloud as a nested application stack                                 
  
      - Puppet
        - Is a configuration management and enforcement tool.
        - used to describe the end-state of a machine and keep it that way.
        - the end state is defined in puppet manifest
        - 2 model are supported
          - standalone mode, in which instructions in the form of manifests are ran locally
          - server mode, where it retrives its manifest from a central server called puppet master.
        - admins make changes in 2 ways: 
          - Uploading new manifests and executing them locally
          - in client/server model making changes to the puppet master
        - used in many areas of director
          - used in Undercloud host locally to install and configure packages as per configurations in Undercloud.conf
          - inject `openstack-puppet-modules` packages into base Overcloud image. these puppet modules are ready for post deployment configuration. By default, we can create an image that contains all services and use it for each node.
          - we can provide additional puppet manifests and parameters to the nodes via Heat, and apply the configuration after overcloud's deployment. This include services to apply and openstack configurations to apply which are dependent on node type. 
          - we provide `puppet hieradata` to nodes. usually puppet modules are free from site or node-specific parameters to keep manifests consistent. Hieradata acts as a form of parameterized values that can be pushed to a puppet module and reference in other areas. 
          - An example, for  this is to reference the MySQL password inside of a manifest, we save this information as hieradata and reference it with in the manifest.
          - hieradata is a yaml file
          - manifest is a .pp file

      - TripleO and TripleO Heat Templates
        - director is based on upstream TripleO project
        - this project combines a set of openstack services:
          - Glance store overcloud images
          - Heat orchestrate the overcloud
          - Ironic and Nova provision bare metal machines
        - TripleO also uses heat tempalte collection that defines Red Hat-supported 
      - Composible services
      - containerized services
      - containerized services and Kolla
      - Ansible
## Chapter 3. Overcloud Images
    - 
      - Obtaining Overcloud Images
      - INITRD - Modifying the initial RAMDISK
      - QCOW2 - Installing virt-customize to the director
      - QCOW2 - Inspecting Overcloud Image 
      - QCOW2 - Setting the root password
      - QCOW2 - Registering the image 
      - QCOW2 - Attaching the sub and enabling Red Hat Repos
      - QCOW2 - Installing RPMS
      - QCOW2 - Cleaning the sub pool
      - QCOW2 - Unregistering the image 
      - QCOW2 - Reset the Machine ID
      - Uploading the images to the director
## Chapter 4. Configuration
## Chapter 5. Orchestration
## Chapter 6. Composable Service
## Chapter 8. Building certified container images
## Chapter 9. Integration Points



