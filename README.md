Welcome to summary of relevant learning content for the IBM Certified Solution Architect – Cloud Pak for Data v4.x. certification.

An IBM Certified Solution Architect on Cloud Pak for Data V4.x is a person who can design, plan, and architect a Data and AI solution in a hybrid cloud environment. This architect can lead and guide the implementation and operationalization of a solution that may include Data Governance (Data Ops), Analytics, and Data Science/Machine Learning/AI (ML Ops). They can do this with limited assistance from support, documentation, and/or relevant subject matter experts.

# Exam Objectives
During exam development, the Subject Matter Experts (SMEs) define all the tasks, knowledge, and experience that an individual would need to successfully fulfil their role with the product or solution. These are represented by the objectives below and the questions on the exam are based upon these: 
- Number of questions: 63
- Number of questions to pass: 42
- Time allowed: 90 minutes

## Outline: 
- [Section 1: Cloud Pak for Data Architecture](#section-1---cloud-pak-for-data-architecture) (21%)
    1. Understand the underlying infrastructure and installation 
    2. Understand sizing and deployment options
    3. Understand Cloud Pak for Data reference architecture 
    4. Understand Cloud Pak for Data reliability options 
    5. Secure the solution and client data
- [Section 2: Build Data Science algorithms](#section-2---build-data-science-algorithms) (14%)
    1. Describe the differences between traditional programming and machine learning as well as no code, low code and visual programming
    2. Understand the process and available tools in Cloud Pak for data to build, deploy and monitor ML/AI algorithms
    3. Identify and explain how to collect, explore, and prepare data for ML/AI algorithms in Cloud Pak for Data
    4. Identify and explain how to build and deploy ML/AI algorithms in Cloud Pak for data
    5. Map business opportunities into a Data Science use case 
- [Section 3: Machine Learning Operations](#section-3---machine-learning-operations) (16%)
    1. Describe the key considerations when selecting a platform for model deployment
    2. Explain the workflow of deploying and monitoring models
    3. Monitor deployed models inside Cloud Pak for Data
    4. Monitor machine learning models running on an external platform 
    5. Manage risk and regulatory compliance using Open Pages 
- [Section 4: Analytics](#section-4---analytics) (17%)
    1. Explain the difference between Descriptive, Prescriptive, Predictive, Diagnostic, and Cognitive Analytics
    2. Describe the capabilities of AI for financial operations in Cloud Pak for Data 
    3. Describe the capabilities of business intelligence in Cloud Pak for Data 
    4. Map business opportunities into an Analytics use case
- [Section 5: Data Governance](#section-5---data-governance) (22%)
    1. Describe the capabilities of a data fabric topology 
    2. Define the Governance structure
    3. Use smart ingestion for auto cataloging 
    4. Understand how workflow is used in Cloud Pak for Data 
    5. Explain the use of Guardium in auditing and monitoring data
    6. Leverage the platform to understand data flow and usage 
    7. Explain the concepts of Knowledge Accelerators
    8. Map business opportunities into a data governance use case
- [Section 6: Integration, Implementation, Deployment, and Scaling](#section-6---integration-implementation-deployment-and-scaling) (10%)
    1. Develop an appropriate process to take a Data and AI solution from inception to production
    2. Develop a strategy to monitor the Data and AI platform
    3. Accelerate the solution using Industry Accelerators and External Data sets
    4. Integrating Business Applications using Cloud Pak for Data


# Section 1 - Cloud Pak for Data Architecture 

[Back to top](#outline)

![cpd_platform](/images/cpd_platform.png)
## 1.1 Understand the underlying infrastructure and installation
### 1.1.1. Describe the features in Cloud Pak Foundational Services 
![found](/images/found_services.png)

Cloud Pak Foundational Services is also known as "Bedrock." It provides key services that run on top of OpenShift Container Platform to power all Cloud Paks, including Cloud Pak for Data, and serves as a layer to support integration between all Paks. 
These capabilities enabled by the CPFS services include the following:
- **Certificate Management Service**: This service enables Cloud Paks to generate TLS certificates, manifest them as Kubernetes secrets, and be mounted in Pods that need them. This helps in securing inter-microservice communications and promotes easier automatic rotation of certificates.
- **Identity and Access Management (IAM) service**: IAM enables authentication for the Cloud Pak. It provides mechanisms for admins to configure one or more identity providers (such as LDAP/AD) to help integrate with existing systems in the enterprise. IAM exposes the OpenID Connect (OIDC) standard that also makes it possible for users to single sign-on between multiple Pak installations.
- **License and metering service**: This service captures utilization metrics for individual services in the cluster. Each Cloud Pak Pod is instrumented with details that identify it uniquely. The license service collects the Virtual Processor Core (VPC) resources associated with each Pod and aggregates them at a product level. It also provides reports for license audit and compliance purposes.
- **Operand Deployment Lifecycle Manager (ODLM)**: The operator pattern is used by all Cloud Paks to deliver and manage services on OpenShift Kubernetes. Kubernetes resources, such as Deployments and StatefulSets that are orchestrated and managed by an operator, are collectively referred to as the Operand controlled by that operator. ODLM [21] is an operator, developed as an open source project, that is used to manage the life cycle of such operands, in a similar way to how OLM manages operators. With higher-level constructs such as OperandRequests, ODLM can provide abstractions and simpler patterns for Paks to manage operands and even define inter-dependencies between them.
- **Namespace Scoping and Projection of privileges**: Operators are granted significant Role-Based Access Control (RBAC) privileges to perform their functions. They connect to the Kubernetes API server and invoke functions that allow it to deploy and manage Kubernetes resources in the cluster. It is very common for OpenShift clusters to be shared among multiple tenants and multiple vendors. Hence, from a security perspective, it becomes imperative to be able to control the breadth of access that both operators and operands are granted.
Frequently, operands are assigned to specific tenant namespaces and are expected to only operate within that namespace. Operators, however, are installed in a central namespace and need to have authority in these individual tenant namespaces. At the same time, it is desirable not to grant cluster-wide authority to operators and to limit their influence only to those namespaces.
IBM introduced the namespace scope operator [22], in open source, to help address this need. This operator can project the authority of operators (and operands if needed) to other namespaces selectively. It also provides the ability to automatically change the configurations of these operators to have them watch additional namespaces and only those namespaces, thereby improving the security posture of the Paks in shared clusters.
- **Zen – the platform experience**: Zen is a framework developed specifically to enable the extensibility and adoption of a plug-n-play paradigm for both the end user experience and for backend service APIs. It is a set of foundational capabilities and UI components that are leveraged by higher-level services in Cloud Paks. It ensures a focus on a single pane of glass for persona-driven and customizable (even re-brandable) user experiences. It fosters collaborations between personas and across product boundaries and, with the plug-n-play model, capabilities are dynamically enabled as and when services are provisioned.
- **The cloudctl utility**: This command-line interface (CLI) provides functions to deploy and manage Cloud Paks on OpenShift Container Platform. cloudctl helps with mirroring Cloud Pak images into an Enterprise Private Container Registry, even into air-gapped environments. Services in Cloud Paks are packaged and made available in the Container Application Software for Enterprises (CASE) format, a specification defined in open source [23]. The utility enables important automation for installing and upgrading services in a Pak, including creating OLM artifacts such as catalog sources and operator subscriptions.


### 1.1.2. Describe the value of running on Redhat OpenShift 
OpenShift Container Platform is a platform for automating the deployment and management of containerized applications. While OpenShift Container Platform uses Kubernetes to orchestrate containers, Kubernetes does not manage platform-level requirements or deployment processes. Therefore, OpenShift Container Platform enhances the capability of Kubernetes by providing platform management tools and processes.
- **Container**: A container is an executable unit of software in which application code is packaged — together with libraries and dependencies — in common ways so that it can be run anywhere on the desktop, traditional IT, or the cloud. Containers take advantage of a form of Operating System (OS) virtualization that lets multiple applications share the OS by isolating processes and controlling the amount of CPU, memory, and disk those processes can access. Containerization is the process of packaging up software code and all its dependencies so that it can run consistently on any infrastructure. That is, containerization allows applications to be "written once and run anywhere". Benefits are (a.o.): Portability, Agility, Speed, Fault isolation, ease of management 
- **Kubernetes** — also known as "k8s" or "kube" — is a container orchestration platform for scheduling and automating the deployment, management, and scaling of containerized applications. As containers proliferated — today, an organization might have hundreds or thousands of them — operations teams needed to schedule and automate container deployment, networking, scalability, and availability. 

- **K8s capabilities**: 
    1. Deployment: Deploy a specified number of containers to a specified host and keep them running in a desired state.
    2. Rollouts: A rollout is a change to a deployment. Kubernetes lets you initiate, pause, resume, or roll back rollouts.
    3. Service discovery: Kubernetes can automatically expose a container to the internet or to other containers by using a DNS name or IP address.
    4. Storage provisioning: Set Kubernetes to mount persistent local or cloud storage for your containers as needed.
    5. Load balancing and scaling: When traffic to a container spikes, Kubernetes can employ load balancing and scaling to distribute it across the network to maintain stability.
    6. Self-healing for high availability: When a container fails, Kubernetes can restart or replace it automatically; it can also take down containers that don’t meet your health-check requirements.


### 1.1.3. Describe the benefits of modernization 
Application Cloud modernization enables organizations to make the most of the digital technologies, including AI, machine learning, big data, and cloud. It helps transform your IT ecosystem based on current market trends and build a flexible foundation for future innovation.
IBM Cloud® Paks are the path toward digital transformation. The speed and agility of the public and hybrid clouds are helping businesses keep pace with customer demand and build and deliver innovative new technologies and services. In addition, cloud-native tools such as containers help businesses to modernize their applications at scale with AI. IBM Cloud Paks can help change how your business works, how you work, and most importantly, how you serve your customers.

### 1.1.4. Describe how CPD can Simplify lifecycle management (upgrades/fixpaks) 
- Unified lifecycle: Users can design, build, test, orchestrate, deploy to production, and monitor different types of data pipelines in a unified way. Users can create or find data assets, search for them across the platform, and move them across workspaces. Users can orchestrate data transformations and other actions by scheduling jobs that run automatically.
- TODO: add additional information around upgrades and fixpacks. 

### 1.1.5. List the benefits of/use cases for multitenancy 
- **Multitenancy** is a reference to the mode of operation of software where multiple independent instances of one or multiple applications operate in a shared environment. The instances (tenants) are logically isolated, but physically integrated. The degree of logical isolation must be complete, but the degree of physical integration will vary.
- **Multitenancy for the platform**: Cloud Pak for Data (the Cloud Pak for Data control plane) can be installed multiple times on the same cluster by installing each instance of Cloud Pak for Data in a separate project (Kubernetes namespace). This configuration offers complete logical isolation of each instance of Cloud Pak for Data with limited physical integration between the instances. When you set up your cluster, a Red Hat OpenShift cluster administrator can create multiple projects (Kubernetes namespaces) to partition your cluster. Within each project, you can assign resource quotas. Each project acts as a virtual cluster with its own security and network policies. In addition to being logically separated, you can use different authentication mechanisms for each Cloud Pak for Data deployment. 
    - This tenancy model addresses the following **use cases**:
        - Partitioning your nonproduction environment from your production environment in a continuous integration, continuous delivery (CICD) pipeline. In this model, tenants work in discrete, isolated units with a clear separation of duties.
        - Creating instances for different departments or business units that have distinct roles and responsibilities within your enterprise. In this model, each tenant has their own authentication mechanism, resource quotas, and assets.
    - This tenancy model also offers several advantages:
        - You can minimize your overhead costs by deploying multiple instances on the same cluster.
        - The cluster administrator can establish tenant-specific quality of service characteristics in each instance.
        - The cluster administrator can assign project administrators to manage an instance of Cloud Pak for Data
        - The project administrator can control which services are deployed in the project and can manage the resources that are associated with the project. However, the project administrator does not have access to cluster-level settings and cannot change the resource quotas for their project.
- Multitenancy for services: The Cloud Pak for Data platform supports multiple mechanisms for achieving service multitenancy. However, not all services support the same mechanisms. The platform offers the following mechanisms:
    - Installing a service one time in each project where the control plane is installed. (This is the most common method for achieving multitenancy.)
    - Installing a service multiple times in the same project as the control plane
    - Installing a service one time in the same project control plane and provisioning multiple instances of the service in that project
    - Installing a service one time in a project that is tethered to the project where the control plane is installed
    - Installing a service one time in the same project as the control plane and deploying instances of the service to projects that are tethered to the project where the control plane is installed
- Tethered projects: If you need to isolate a service instance by deploying it to a separate project (namespace), you can create a tethered project for the service instance during installation. The service instance in the tethered project can be managed by Cloud Pak for Data but is otherwise isolated from Cloud Pak for Data and the other services that run in the Cloud Pak for Data project.


### 1.1.6. Describe the differences between Cloud Pak as a Service and Cloud Pak v4.0 
![deploy](/images/deployment_options.png)

### 1.1.7. Describe advantages of using Operators 
- An Operator is a set of Kubernetes-native resources that packages, deploys, and manages a Kubernetes application by extending the Kubernetes API.
- An operator is an application that manages other applications and does not have user functionality. It adds the important functional value to the Red Hat OpenShift Container Platform. With operators you can deploy applications and their components, without the need for manual upgrades of operating system and control plane applications. They enable simplified, cluster-wide management of critical components.
- An Operator consists of several pieces of software that allow efficient management of applications on Kubernetes — a controller and one or more custom resource definitions (CRD). The controller is custom code that is deployed to a Kubernetes cluster and is designed to watch for changes to custom Kubernetes resources and react to them. A custom resource is an extension of the Kubernetes API and is used to provide additional capability that may not be available in the default Kubernetes installation. It allows for customization and modularization of Kubernetes.

### 1.1.8. Understand the installation procedure for Cloud Pak 
When you install IBM® Cloud Pak for Data, you update the IBM Cloud Pak® for Data platform operator and the IBM Cloud Pak foundational services operator to watch the project where you will install IBM Cloud Pak for Data. Then, you create a custom resource to install Cloud Pak for Data in that project.
- (Pre-) installation procedure: 
    - Installing Red Hat OpenShift Container Platform: IBM Cloud Pak for Data is deployed on a Red Hat OpenShift Container Platform cluster. If you don't have an existing cluster, complete the appropriate steps to install Red Hat OpenShift on your environment. 
    - Setting up shared persistent storage: Before you can install Cloud Pak for Data, you must set up persistent storage on your Red Hat OpenShift cluster.
    - Setting up projects (namespaces) on Red Hat OpenShift Container Platform: Before you install IBM Cloud Pak for Data on Red Hat OpenShift Container Platform, a cluster administrator should create and configure the OpenShift projects (Kubernetes namespaces) where you plan to deploy the Cloud Pak for Data software.
    - Obtaining your IBM entitlement API key: The IBM entitlement API key enables you to pull software images from the IBM Entitled Registry, either for installation or for mirroring.
    - Mirroring images to your private container registry: IBM Cloud Pak for Data images are accessible from the IBM Entitled Registry. In most situations, it is strongly recommended that you mirror the necessary software images from the IBM Entitled Registry to a private container registry.
    - Configuring your cluster to pull Cloud Pak for Data images: To ensure that your cluster can pull Cloud Pak for Data software images, you must update your cluster configuration.
    - Creating catalog sources: To ensure that your cluster uses the correct software images, you must create the appropriate catalog sources for your environment.
    - Installing IBM Cloud Pak foundational services: IBM Cloud Pak foundational services is a prerequisite for IBM Cloud Pak for Data. IBM Cloud Pak foundational services is installed one time on the cluster and is used by any instances of Cloud Pak for Data or other IBM Cloud Paks that are installed on the cluster.
    - Creating operator subscriptions: An operator subscription tells the cluster where to install a given operator and gives information about the operator to Operator Lifecycle Manager (OLM).
    - Custom security context constraints for services: Most Cloud Pak for Data services use the restricted security context constraint (SCC) that is provided by Red Hat OpenShift Container Platform. However, if you plan to install certain Cloud Pak for Data services, you might need to use some custom SCCs.
    - Changing required node settings: Some services that run on IBM Cloud Pak for Data require specific settings on the nodes in the cluster. To ensure that the cluster has the required settings for these services, an operating system administrator with root privileges must review and adjust the settings on the appropriate nodes in the cluster.


## 1.2 Understand sizing and deployment options 
1.2.1 Demonstrate an understanding of the Cloud Pak deployment options.
- Deployment options (see above): 
    - IBM Cloud Pak® for Data: This open, extensible data and AI platform is built on Red Hat® OpenShift® and can be deployed on any cloud.
    - IBM Cloud Pak® for Data System: Accelerate AI with this all-in-one data and AI platform in-a-box. Deploy faster using preconfigured plug-and-play nodes.
    - IBM Cloud Pak® for Data as a Service: Access a set of IBM Cloud Pak for Data platform services that are fully managed on the IBM public cloud and brought to your data through IBM Cloud Satellite™.
- Cloud Pak for Data *Software* is deployed on a multi-node cluster. Although you can deploy Cloud Pak for Data on a 3-node cluster for development or proof of concept environments, it is recommended that you deploy your production environment on a larger, highly available cluster with multiple dedicated master and worker nodes. This configuration provides better performance, better cluster stability, and increased ease of scaling the cluster to support workload growth. The specific requirements for a production-level cluster are identified in System requirements.
- In a production-level cluster, there are **three** master + infrastructure nodes and three or more worker nodes. Using dedicated worker nodes means that resources on those nodes are used only for application workloads, which improves the performance of the cluster.

![prod](/images/prod.png)

- Hardware requirements:

![hardware](/images/hardware.png)

    - Load balancer: A load balancer is required when using three master nodes. The load balancer distributes the traffic load of the master and proxy nodes, securely isolates the master and compute node IP addresses, and facilitates external communication, including accessing the management console and API or making other requests to the master and proxy nodes.
    - Bastion node: You can optionally use a bastion node to download the required software images. If you choose to use a bastion node, use an x86-64 system with Red Hat Enterprise Linux®. The bastion node must be able to run the following software: OpenShift CLI, IBM Cloud Pak CLI (cloudctl), httpd-tools, skopeo. 
- Software requirements:
    - Following software to install Cloud Pak for Data:
        - RH OCP (Version 4.6.29 or later, Version 4.8.0 or later)
        - Container runtime (OCP must include container runtime): CRI-O version 1.13 or later
        - K8s Metrics Server: optional, to gather pods and nodes metrics
        - Cloud Pak Foundational services
        - Service software requirements: see https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=requirements-software
- Storage requirements: 
    - Platform level: 
        - Container image registry: in case of mirroring image to local container registry, minimum of 300GB of storage space in container registry
        - Local storage for container images per node: minimum 300GB of storage space per node
        - Persistent storage for services: The Cloud Pak for Data control plane and services store data in persistent storage.
            - Supported storage types: The platform supports several different types of persistent storage: 
                - Red Hat OpenShift Container Storage: Version: 4.6 or later fixes
                - IBM Spectrum® Fusion: Version: 2.1.2 or later fixes
                - IBM Spectrum Scale Container Native storage: IBM Spectrum Scale Container Native Storage Access Version: 5.1.1.3 or later fixes
                - Network File System (NFS) :Version: 4
                - Portworx: Version: 2.7.0 or later fixes
                - IBM Cloud File Storage: Version: Not applicable
    - Control Plane level: The Cloud Pak for Data control plane supports all of the shared persistent storage types that are supported by the platform. The shared cluster components: Foundational Services (all except NFS), Scheduling Service (no storage needed), Common Core Services(all)) 
    - Service level: all major services support all storage types (OpenShift Container Storage, IBM Spectrum, NFS, IBM Cloud File Storage, Portworx)

## 1.3 Understand Cloud Pak for Data reference architecture 
![stack](/images/stack.png)
![stack_1](/images/stack_1.png)

## 1.4 Understand Cloud Pak for Data reliability options 

### 1.4.1. Explain how Cloud Pak for Data uses OpenShift to achieve service availability. 
- TODO

### 1.4.2. Understand the backup and restore strategy.
- IBM® Cloud Pak for Data provides two utilities to back up and restore your deployment: 
    - OpenShift® APIs for Data Protection (OADP) backup and restore utility: The Cloud Pak for Data OADP backup and restore utility backs up the Kubernetes metadata and persistent volumes in a Cloud Pak for Data instance project (namespace). The OADP backup and restore utility can restore an entire Cloud Pak for Data deployment to the same cluster or to a different cluster.
    - Volume backup and restore utility: The Cloud Pak for Data volume backup and restore utility can create volume snapshots (Portworx only) and volume backups of the PersistentVolumeClaims (PVCs) of a set of projects. The Cloud Pak for Data volume backup and restore utility restores only volume data, and only within the same Cloud Pak for Data instance. Kubernetes resources in the project must still exist.

### 1.4.3. Scaling: 
- Scaling changes the capacity of services by adjusting the memory resource settings, the number of CPUs, and the number of pods that are available. Pods act as servers with that run applications or functions. Pods consume resources such as core and memory when components distribute tasks to them. Scaling the pods to medium, for example, increases the processing capacity of the application. You use the scaleConfig setting in the service custom resource (CR) to set the scaling configuration for a service. The following predefined scaling configurations are provided for services that support scaling:
    1.	Small (default configuration)
    2.	Medium
    3.	Large
- You can adjust IBM® Cloud Pak for Data services by scaling the resources that they use to support high availability or to increase processing capacity. Resources can be scaled based on predefined resource configurations. You must be either: A cluster administrator or An administrator of the project where the software is installed, for example cpd-instance. If a service supports scaling, you can scale the service at any time after you install it. 
    - Not all services support scaling
    - Not all services use the scaleConfig setting
    - You can scale a service by using one of the following commands: oc edit or oc patch

## 1.5 Secure the solution and client data 
### 1.5.1. Explain security for users available on CPD
TODO

### 1.5.2. Differentiate between authentication and authorization on Cloud Pak for Data
- Authentication verifies the identity of a user or service, and authorization determines their access rights.
- By default, Cloud Pak for Data user records are stored in an internal LDAP. The initial setup of Cloud Pak for Data uses the internal LDAP. However, after you set up Cloud Pak for Data, it is recommended that you use an enterprise-grade password management solution, such as SAML SSO or an LDAP provider for password management.
- Tokens and API keys
- Shared credentials: By default, connections that are created in Cloud Pak for Data are shared

### 1.5.3. Explain encryption on CPD
- Cloud Pak for Data supports protection of data at rest and in motion. It supports FIPS (Federal Information Processing Standard) compliant encryption for all encryption needs.
- **Data**: In general, data security is managed by your remote data sources. OpenShift uses resources that are known as Security Context Constraints (SCCs) to enforce the security context of a Pod or a Container (the Kubernetes equivalent is the PodSecurityPolicy). Cloud Pak for Data containers use restricted SCC by default. Restricted SCC deny access to all host features and requires pods to run with a UID, SELinux context that is scoped within the namespace. To ensure that your data in Cloud Pak for Data is stored securely, you can encrypt your storage partition. If you use Linux Unified Key Setup-on-disk-format (LUKS), you must enable LUKS when you install Red Hat OpenShift Container Platform. 
- **Communications**: You can use TLS or SSL to encrypt communications to and from Cloud Pak for Data.
- **FIPS**: Cloud Pak for Data also supports protection of data at rest and in motion. It supports FIPS (Federal Information Processing Standard) compliant encryption for all encryption needs.

### 1.5.4. Describe Network security on CPD: 
- To ensure secure transmission of network traffic to and from the Cloud Pak for Data cluster, you need to configure the communication ports used by the Cloud Pak for Data cluster.
- **Primary port**: The primary port is what the Red Hat OpenShift router exposes.
- **Communication ports for services**: When you provision a new service or integration on your Cloud Pak for Data cluster, the services might require connections to be made from outside the cluster.
- **DNS service name**: When you install the Cloud Pak for Data control plane control plane, the installation points to the default Red Hat OpenShift DNS service name. If your OpenShift cluster is configured to use a custom name for the DNS service, a project administrator or cluster administrator must update the DNS service name to prevent performance problems.

### 1.5.5. Explain how Red Hat OpenShift Container Platform provides security for CPD 
- Security is required for every enterprise, especially for organizations in the government, financial services, and healthcare sectors. OpenShift® container platform provides a set of security features. These features protect sensitive customer data with strong encryption controls and improve the oversight of access control across applications and the platform itself.
- Red Hat® OpenShift Container Platform enables an improved security posture with the addition of many capabilities that greatly increase the security of the platform.
    - Uses Red Hat CoreOS as the immutable host operating system.
    - Provides stronger platform security with FIPS (Federal Information Processing Standard) compliant encryption (FIPS 140-2 Level 1). For more information, see Services that support FIPS
    - Uses the Node Tuning Operator, which provides opportunities to further reduce privilege requirements in the security context constraints (SCC). For more information, see Using the Node Tuning Operator.
    - Supports encrypting data that is stored in etcd, which provides extra protection for secrets that are stored in the etcd database. For more information, see Encrypting etcd data.
    - Provides a Network Bound Disk Encryption (NBDE) feature that can be used to automate remote enablement of LUKS encrypted volumes, making it better protected against physical theft of host storage.
    - Enables SELinux as mandatory on Red Hat OpenShift Container Platform.
- Cloud Pak for Data builds on the security features provided by OpenShift by creating Security Context Constraints (SCC), service accounts, and roles so that Cloud Pak for Data pods and users have the lowest level of privileges to the OpenShift platform that is needed for them. Cloud Pak for Data is also security hardened on the OpenShift platform and is installed in a secure and transparent manner.
- Security hardening is enforced on Cloud Pak for Data on Red Hat OpenShift. The following security hardening actions are taken:
    - Only non-root processes are run in containers. The UIDs of the processes are in the OpenShift Project's pre-defined range only, enforced by the use of the restricted SCCs. The restricted SCC does not allow running containers as root.
    - Cluster Admin privileges are not required for Cloud Pak for Data workloads at runtime. Cluster Admin authority is needed only to set up projects and custom SCCs (and only for the services that do need them). Service accounts in each Cloud Pak for Data instance are granted privileges that are only scoped within their OpenShift project.
    - Cloud Pak for Data users are typically not granted OpenShift Kubernetes access, and even if they are, it would be only for express purpose of installing or upgrading services inside their assigned OpenShift project.
    - Strict use of service accounts with RBAC privileges is enforced, and the least privilege principle is applied. Cloud Pak for Data ensures that any pod that is running user code (such as scripts or analytics environments) is not granted any RBAC privileges.
    - No host access is required for Cloud Pak for Data workloads at runtime. This restriction is enforced by the SCCs. There is no access to host paths or networks.
    - All pods have restricted resource consumption. Pod resource requests and limits are set for each pod, which restricts the consumption. This approach helps protect against noisy neighbors that cause resource contention.
    - Reliability gauges (liveness and readiness probes) are present for each pod to ensure that the pods are working correctly.
    - For consumption monitoring, each of the pods on Cloud Pak for Data is annotated with metering annotations to uniquely identify add-on service workloads on the cluster.

### 1.5.6. Describe Security and Auditing considerations
- Audit logging provides accountability, traceability, and regulatory compliance. The regulatory compliance must be set in a way that it allows access to and modification of data.
- A complete auditing solution that works with Cloud Pak for Data requires contributions and coordination of solutions from OpenShift®, Guardium®, and Cloud Pak for Data
![audit](/images/audit.png)
- Exporting CPD audit records to SIEM solution (Splunk, LogDNA, or QRadar®): 
    - The Audit Logging Service is automatically installed when you install an instance of Cloud Pak for Data. However, you must enable and configure the Audit Logging Service if you want Cloud Pak for Data to collect and forward Cloud Auditing Data Federation (CADF) compliant audit records from the services that are associated with your Cloud Pak for Data deployment.
    - Auditing logging is not supported by certain components and services of Cloud Pak for Data. 

### 1.5.7. Describe SSO, IAM and LDAP use in user management
TODO


# Section 2 - Build Data Science algorithms 

[Back to top](#outline)

## 2.1 Describe the differences between traditional programming and machine learning as well as no code, low code and visual programming 
TODO

## 2.2 Understand the process and available tools in Cloud Pak for data to build, deploy and monitor ML/AI algorithms 

### 2.2.1. Explain the process of Model Ops and Tools in Cloud Pak for data projects are used to develop AI/ML algorithms
![modelops](/images/modelops.png)
1. Collect the data: 
![collect](/images/collect.png)
2. Explore the data: 
![explore](/images/explore.png)
3. Build the models: 
![build](/images/build.png)
4. Deploy the model: 
![deploy](/images/deploy.png)
5. Monitor the model: 
![monitor](/images/monitor.png)

### 2.2.2. Describe the available tools to choose when developing the models.
To pick the right tool, consider these factors.
- **The type of data you have**
    - Tabular data in delimited files or relational data in remote data sources
    - Image files
- **Textual data in documents**
    - The type of tasks you need to do
    - Prepare data: cleanse, shape, visualize, organize, and validate data.
    - Analyze data: identify patterns and relationships in data, and display insights.
    - Build models: build, train, test, and deploy models to make predictions or optimize decisions.
- **How much automation you want**
    - Code editor tools: Use to write code in Python, R, or Scala.
    - Graphical canvas tools: Use menus and drag-and-drop functionality on a canvas to visually program.
    - Automated builder tools: Use to configure automated tasks that require limited user input.

Following tools are available: 

- Tabular data: 
![tab](/images/tabular.png)

- Textual data: 
![text](/images/text.png)

- Image data: 
![image](/images/image.png)

Further information can be found [under this link](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=projects-choosing-tool). 

## 2.3 Identify and explain how to collect, explore, and prepare data for ML/AI algorithms in Cloud Pak for Data 
- **Jupyter notebook editor**
    - Use the Jupyter notebook editor to create a notebook in which you run code to prepare, visualize, and analyze data, or build and train a model.
    - Data format: Any
    - Data size: Any
    - How you can prepare data, analyze data, or build models  Write code in Python, R, or Scala.  Include rich text and media with your code.  Work with any kind of data in any way you want.  Use preinstalled or install other open source and IBM libraries and packages.  Schedule runs of your code   Import a notebook from a file or a URL.  Share read-only copies of your notebook externally.
- **Data Refinery**
    - Use Data Refinery to prepare and visualize tabular data with a graphical flow editor. You create and then run a Data Refinery flow as a set of ordered operations on data.
    - Data format: Tabular: Avro, CSV, JSON, Parquet, SAS with the "sas7bdat" extension (read only), TSV (read only), or delimited text files
    Relational: Tables in relational data sources
    - Data size: Any
    - How you can prepare data: Cleanse, shape, organize data with over 60 operations.  Save refined data as a new data set or update the original data.  Profile data to validate it.  Use interactive templates to manipulate data with code operations, functions, and logical operators.  Schedule recurring operations on data.
    - How you can analyze data: Identify patterns, connections, and relationships within the data in multiple visualization charts.
- **Dashboard editor**
    - Use the Dashboard editor to create a set of visualizations of analytical results on a graphical canvas.
    - Required service: Cognos Dashboard
    - Data format  Tabular: CSV files  Relational: Tables in some relational data sources
    - Data size: Any size
    - How you can analyze data: Create graphs without coding.  Include text, media, web pages, images, and shapes in your dashboard.
- **SPSS Modeler**
    - Use SPSS Modeler to create a flow to prepare data and build and train a model with a flow editor on a graphical canvas.
    - Required services: SPSS Modeler Watson Machine Learning
    - Data formats: Relational: Tables in relational data sources  Tabular: Excel files (.xls or .xlsx), CSV files, or SPSS Statistics files (.sav)  Textual: In the supported relational tables or files
    - Data size: Any
    - How you can prepare data: Use automatic data preparation functions.  Write SQL statements to manipulate data.  Cleanse, shape, sample, sort, and derive data.
    - How you can analyze data  Visualize data with over 40 graphs.  Identify the natural language of a text field.
    - How you can build models: 
        - Build predictive models: Choose from over 40 modeling algorithms. 
        - Use automatic modeling functions: Model time series or geospatial data
        - Classify textual data: Identify relationships between the concepts in textual data.
    - Get started: To create an SPSS Modeler flow, click Add to project > Modeler flow and then choose IBM SPSS Modeler.
- **Decision Optimization model builder**
    - Use Decision Optimization to build and run optimization models in the Decision Optimization modeler or in a Jupyter notebook.
    - Required service: Decision Optimization
    - Data formats: Tabular: CSV files
    - Data size: Any
    - How you can prepare data: Import relevant data into a scenario and edit it.
    - How you can build models: Build prescriptive decision optimization models.  Create, import and edit models in Python DOcplex, OPL or with natural language expressions. Create, import and edit models in notebooks.
    - How you can solve models: Run and solve decision optimization models using CPLEX engines. Investigate and compare solutions for multiple scenarios.  Create tables, charts and notes to visualize data and solutions for one or more scenarios.
    - Get started: To create a Decision Optimization model, click Add to project > Decision Optimization, or for notebooks click Add to project > Notebook.
- **AutoAI tool**
    - Use the AutoAI tool to automatically analyze your tabular data and generate candidate model pipelines customized for your predictive modeling problem.
    - Required service: Watson Machine Learning
    - Data format: Tabular: CSV files
    - Data size: Less than 1 GB
    - How you can prepare data: Automatically transform data, such as impute missing values.
    - How you can build models: Train a binary classification, multiclass classification, or regression model.  View a tree infographic that shows the sequences of AutoAI training stages.  Generate a leaderboard of model pipelines ranked by cross-validation scores.  Save a pipeline as a model.
    - Get started: To create an AutoAI experiment, click Add to project > AutoAI experiment.
- **Experiment builder**
    - Use the Experiment builder to build deep learning experiments and run hundreds of training runs. This method requires that you provide code to define the training run. You run, track, store, and compare the results in the Experiment Builder graphical interface, then save the best configuration as a model.
    - Required service: Watson Machine Learning
    - Data format: Textual: CSV files with labeled textual data  Image: Image files in a PKL file. For example, a model testing signatures uses images resized to 32×32 pixels and stored as numpy arrays in a pickled format.
    - Data size: Any size
    - How you can build models: Write Python code to specify metrics for training runs.  Write a training definition in Python code.  Define hyperparameters, or choose the RBFOpt method or random hyperparameter settings.  Find the optimal values for large numbers of hyperparameters by running hundreds or thousands of training runs.  Run distributed training with GPUs and specialized, powerful hardware and infrastructure.  Compare the performance of training runs.  Save a training run as a model.
    - Get started: To create an experiment, click Add to project > Experiment.
- **Federated Learning**
    - Use the Federated Learning tool to trian a common model using distributed data. The data is never combined or share, preserving data integrity while providing all participating parties with a model based on the aggregated data.
    - Required service: Watson Machine Learning
    - Data format: Any
    - Data size: Any size
    - How you can build models: Choose a training framework.  Configure the common model.  Configure a file for training the common model.  Have remote parties train their data.  Deploy the common model.
    - Get started: To create an experiment, click Add to project > Federated Learning experiment.
- **Metadata import**
    - Use the metadata import tool to automatically discover and import technical and process metadata for data assets into a project or a catalog.
    - Required service: Watson Knowledge Catalog
    - Data format: Any
    - Data size: Any size
    - How you can prepare data: Import data assets from a connection to a data source.
    - Get started: To import metadata, click Add to project > Metadata import.
- **IBM Match 360 with Watson**
    - Use IBM Match 360 with Watson to create master data entities that represent digital twins of your customers. Model and map your data, then run the matching algorithm to create master data entities. Customize and tune your matching algorithm to meet your organization's requirements.
    - Required services: 
        - IBM Match 360 with Watson
        - IBM Watson Knowledge Catalog
    - Data size: Any
    - How you can prepare data: Model and map data from sources across your organization.  Run the customizable matching algorithm to create master data entities.  View and edit master data entities and their associated records.
    - Get started: To create an IBM Match 360 configuration asset, click Add to project > Master data configuration.
- **RStudio IDE**
    - Use RStudio IDE to analyze data or create Shiny applications by writing R code. RStudio can be integrated with a Git repository which must be associated with the project.
    - Required service: RStudio
    - Data format: Any
    - Data size: Any size
    - How you can prepare data, analyze data, and build models: Write code in R.  Create Shiny apps.  Use open source libraries and packages.  Include rich text and media with your code.  Prepare data.  Visualize data.  Discover insights from data.  Build and train a model using open source libraries.  Share your Shiny app in a Git repository.
    - Get started: To use RStudio, click Launch IDE > RStudio.
- **JupyterLab**
    - Use the JupyterLab IDE to create a notebook or Python script in which you run code to prepare, visualize, and analyze data, or build and train a model. JupyterLab is integrated with a Git repository which must be associated with the project.
    - Data format: Any
    - Data size: Any
    - How you can prepare data, analyze data, or build models: Write code in Python.
    Include rich text and media with your code.  Work with any kind of data in any way you want.  Use preinstalled or install other open source and IBM libraries and packages.  Import a notebook from a file.  Share your notebook or script in a Git repository.
    - Get started: To use JupyterLab, click Launch IDE > JupyterLab.
- **Masking flows**
    - Use the masking flows tool to prepare masked copies or masked subsets of data from the catalog. Data is de-identified using advanced masking options with data protection rules.
    - Required service: Watson Knowledge Catalog
    - Data format: Relational: Tables in relational data sources
    - Data size: Any size
    - How you can prepare data, analyze data, or build models: Import data assets from governed catalog to project.  Create masking flow job definitions to specify what data to mask with data protection rules.  Optionally subset data to reduce size of copied data.  Run masking flow jobs to load masked copies to target database connections.
    - Get started:   Ensure that pre-requisite steps in Watson Knowledge Catalog are completed. To privatize data, do one of the following tasks: Click Add to project > Masking flow.


## 2.4 Identify and explain how to build and deploy ML/AI algorithms in Cloud Pak for data 
- see ModelOps Use Case above
- Deployment: Using IBM Watson Machine Learning, you can deploy models, scripts, and functions, manage your deployments, and prepare your assets to put into production to generate predictions and insights.
![steps](/images/steps.png)
![three](/images/three.png)
- Integrating externally developed models in Watson Studio is only partially possible – e.g. python and R Code cannot. However other models created outside of Watson Studio can be monitored in Watson Openscale.

## 2.5 Map business opportunities into a Data Science use case 
![use_cases](/images/use_cases.png)
- Please also see the [Industry Accelerators](https://community.ibm.com/accelerators/?context=analytics)



# Section 3 - Machine Learning Operations 

[Back to top](#outline)

## 3.1 Describe the key considerations when selecting a platform for model deployment 

### 3.1.1. Model Operationalizing requirements
![complete](/images/complete.jpg)
TODO: add requirements. 
### 3.1.2. Describe the benefits of a machine learning pipeline: 
- More machine learning models need to be deployed in production in a faster, repeatable, and consistent manner -- and with the right governance. Kubeflow became a leading solution to address MLOps needs. Kubeflow is an end-to-end machine learning platform that is focused on distributed training, hyperparameter optimization, production model serving and management, and machine learning pipelines with metadata and lineage tracking.
- Needless to say, Kubeflow Pipelines became a primary vehicle to address the needs of both DevOps engineers and data scientists.
    - For DevOps folks, Kubeflow taps into the Kubernetes ecosystem, leveraging its scalability and containerization principles
    - For Data Scientists, Kubeflow Pipelines offers a Python interface to define and deploy Pipelines, enabling metadata collection and lineage tracking
    - For DataOps folks, Kubeflow Pipelines brings in ETL bindings to participate more fully in collaboration with peers by providing support for multiple ETL components and use cases.
![mlops](/images/mlops.png)

### 3.1.3. Operationalize Machine Learning Models build by data scientists
![model_to](/images/deploy_to.png)
TODO: add description. 

## 3.2 Explain the workflow of deploying and monitoring models 

### 3.2.1. Define the importance of ML lifecycle
![crips](/images/crisp.jpg)

### 3.2.2. Collaborative Platform - Watson Studio
Options to collaborate (I remember this was asked in the exam!). 
- Option 1: local collaboration (no git):
![git_1](/images/git_1.jpg)
- Option 2: Collaboration via Git for all assets **with the exception of JupyterLab**:
![git_2](/images/git_2.jpg)
- Option 3: JupyterLab collaboration with Git: 
![git_3](/images/git_3.jpg)

## 3.3 Monitor deployed models inside Cloud Pak for Data 
-> OpenScale: https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=functions-validating-monitoring-ai-models-watson-openscale 
- TODO: summarize information found in link. 

## 3.4 Monitor machine learning models running on an external platform 
The Watson OpenScale service supports the following machine learning engines. Each runtime supports models that are created in the following frameworks:
- IBM Watson Machine Learning: You can use IBM Watson Machine Learning to perform payload logging, feedback logging, and to measure performance accuracy, runtime bias detection, explainability, and auto-debias function as part of your model evaluation.
- Azure ML Studio: You can use Microsoft Azure ML Studio to perform payload logging, feedback logging, and to measure performance accuracy, runtime bias detection, explainability, and auto-debias function as part of your model evaluation.
- Azure ML Service: You can use Microsoft Azure ML Service to perform payload logging, feedback logging, and to measure performance accuracy, runtime bias detection, explainability, and auto-debias function as part of your model evaluation}.
- AWS SageMaker: You can use Amazon SageMaker to perform payload logging, feedback logging, and to measure performance accuracy, runtime bias detection, explainability, and auto-debias function as part of your model evaluation.
- Custom: You can use your custom machine learning framework to perform payload logging, feedback logging, and to measure performance accuracy, runtime bias detection, explainability, and auto-debias function as part of your model evaluation. The custom machine learning framework must have equivalency to IBM Watson Machine Learning.
- SPSS C&DS (only available in IBM Watson OpenScale for IBM Cloud Pak for Data): You can use IBM SPSS C&DS to perform payload logging, feedback logging, and to measure performance accuracy, runtime bias detection, explainability, and auto-debias function as part of your model evaluation.

## Manage risk and regulatory compliance using Open Pages
IBM OpenPages with Watson offers you the capability to deploy domain-targeted product modules to meet specific risk and compliance challenges. Choose the product modules you need within a single integrated environment.
- IBM OpenPages Operational Risk Management: Automate the process of identifying, measuring, monitoring, analyzing, and managing operational risks.
- IBM OpenPages Regulatory Compliance Management: Drive efficient end-to-end regulatory compliance management.
- IBM OpenPages Model Risk Governance: Demonstrate strong model governance, reporting and compliance.
- IBM OpenPages IT Governance: Obtain a holistic view of IT risks and map them to business processes.
- IBM OpenPages Internal Audit Management: Automate and manage internal audits and conduct broader risk and compliance management activities.
- IBM OpenPages Business Continuity Management: Prepare your enterprise for business continuity and protect employees in the face of disruptive events.
- IBM OpenPages Third Party Risk Management: Mitigate risks and improve business results with each of your vendors.
- IBM OpenPages Policy Management: Keep your policies and procedures up to date with your internal and external obligations.
- IBM OpenPages Financial Controls Management: Reduce costs and complexity of complying with Sarbanes-Oxley and similar financial reporting regulations.
- IBM OpenPages Data Privacy Management: Break down silos between IT and compliance for complete data privacy and governance.

# Section 4 - Analytics

[Back to top](#outline)

## 4.1 Explain the difference between Descriptive, Prescriptive, Predictive, Diagnostic, and Cognitive Analytics 
![differences](/images/differences.png)
- **Descriptive Analytics**: -> What happened: still accounts for the majority of all business analytics today, helps organizations to understand past performance by mining historical data to look for the reasons behind past success or failure. 
IBM Services: primarily Cognos Analytics, but also Planning Analytics
- **Diagnostic Analytics**: This is the process of gathering and interpreting different data sets to identify anomalies, detect patters, and determine relationships. IBM services: primarily Cognos Analytics, but also Planning Analytics
- **Predictive Analytics**: -> What is likely to happen: his is when historical data is combined with rules, algorithms, and occasionally external data to determine the probable future outcome of an event or the likelihood of a situation occurring. Predictive analytics, broadly speaking, is a category of business intelligence that uses descriptive and predictive variables from the past to analyze and identify the likelihood of an unknown future outcome. At this stage you are no longer just asking what happened, but why it happened, and what could happen in the future. IBM services: SPSS Modeler, Watson Studio / WML, but presumably Planning Analytics as well. 
- **Prescriptive Analytics**:  Prescriptive analytics is a combination of data, mathematical models, and various business rules to infer actions to influence future desired outcomes. Prescriptive analytics is the next step in the progression of analytics where we take: 
    - The data we gathered in the descriptive stage that told us what happened,
    - Combine it with the diagnostic analytics that told us why it happened,
    - Combine those with the predictive analytics that told us when it may occur again.
Prescriptive analytics goes beyond predicting future outcomes by also suggesting actions to benefit from the predictions and showing the implications of each decision option. 
IBM Services: Decision Optimization is described as *the* prescriptive analytics services, but Planning Analytics and Cognos Analytics and SPSS also have such capabilities.  
- **Cognitive Analytics**: Cognitive analytics brings together a number of intelligent technologies to accomplish this, including semantics, artificial intelligence algorithms and a number of learning techniques such as deep learning and machine learning. 
![analytics](/images/analytics.png)

## 4.2 Describe the capabilities of AI for financial operations in Cloud Pak for Data 
-> financial operations == Planning Analytics.
With the IBM® Planning Analytics service, you can identify and understand patterns and relationships in your business data.
Within the Planning Analytics service, Planning Analytics Workspace is a web-based interface that provides full modeling, reporting, planning, and administrative capabilities. 

![pa](/images/pa_workspace.png)

In addition to Planning Analytics Workspace, the Planning Analytics service provides access to these additional Planning Analytics components.
- Planning Analytics for Microsoft Excel is an Excel-based tool that you can use to build sophisticated reports in a familiar spreadsheet environment.
- Planning Analytics TM1 Web is as a web-based client that extends the analytical power of Planning Analytics. With TM1 Web you can view, analyze, edit, and chart your IBM TM1 data in a web browser. Administrators can also use TM1 Web to perform some administration tasks specific to TM1 Web.

### 4.2.1. List the capabilities of Planning Analytics (rpts, models, cubes) 
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSD29G_2.0.0/main/welcome.html?pos=20.

### 4.2.2. List the benefits of running Planning Analytics in Cloud Pak for Data (single UI) 
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSD29G_2.0.0/main/welcome.html?pos=20.

### 4.2.3. List the components to access data on the TM1 database 
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSD29G_2.0.0/main/welcome.html?pos=20.

### 4.2.4. Identify considerations when managing users in Planning Analytics  
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSD29G_2.0.0/main/welcome.html?pos=20.

### 4.2.5. Describe the use cases for using Planning Analytics
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSD29G_2.0.0/main/welcome.html?pos=20.

## 4.3 Describe the capabilities of business intelligence in Cloud Pak for Data
-> business intelligence == Cognos Analytics.
With the IBM Cognos® Analytics service, you can easily create compelling visualizations and dashboards without needing a data science background.

With the Cognos Analytics service in IBM Cloud Pak for Data, line-of-business users can unearth hidden insights with a personalized analytics experience that is driven by AI. IBM Cognos Analytics is a proven, self-service, dependable analytics solution that provides scalability and analytics governance.

![cognos](/images/cognos.png)

Cognos Analytics includes an AI Assistant (left), and a Details pane (right), to help interpret the chart that you are viewing. The Assistant supports natural language exploration, while the Details pane provides system-generated plain-language information to augment the chart.

![cognos_1](/images/cognos_explore.png)

The Explore feature reduces the guesswork that is associated with data exploration by finding the strongest relationships in your data. The relationships are displayed in the relationship diagram, and suggested starting points are offered for more data exploration.
### 4.3.1. Identify how Natural language processing can be used in business reporting.
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSEP7J_11.1.0

### 4.3.2. Describe the benefits of using Cognos Analytics for Cloud Pak for Data (access Data sources with DV/WKC that Cognos doesn’t support natively, scalability, containerized) 
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSEP7J_11.1.0

### 4.3.3. Describe self-service analytics (using Cognos) 
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSEP7J_11.1.0

### 4.3.4. List options for report distribution (using Cognos) 
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSEP7J_11.1.0

### 4.3.5. Explain Data Explorer capabilities (using Cognos) 
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSEP7J_11.1.0

### 4.3.6. Contrast the Business Intelligence options in Cloud Pak for Data (dashboard / full Cognos) 
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSEP7J_11.1.0

### 4.3.7. Describe the security feature in Cognos Analytics for Cloud Pak for Data (rolebased)
TODO: add summary, from https://www.ibm.com/support/knowledgecenter/SSEP7J_11.1.0

## 4.4 Map business opportunities into an Analytics use case 
### 4.4.1. Identify a use case for Planning Analytics 
Examples: AI for Financial Operations
### 4.4.2. Identify a use case for Cognos Analytics 
Examples: Business Reporting 
### 4.4.3. Describe a use case for Decision Optimization 
Example: Intelligent maintenance Industry accelerators


# Section 5 - Data Governance 

[Back to top](#outline)

## 5.1 Describe the capabilities of a data fabric topology 
- A data fabric is an architectural pattern for managing highly distributed and disparate data. 
- Because it is designed for hybrid and multi-cloud data environments, a data fabric supports the decoupling of data storage, data processing, and data use. 
- With the intelligent knowledge catalog capabilities, you can elevate data into enterprise assets that are governed globally regardless of where the data is stored, processed, or used. Catalog assets are automatically assigned metadata that describes logical connections between data sources and enriches them with semantics so that you can provide business-ready data for your applications, services, and users.

![data_fabric](/images/data_fabric.png)

TODO: add information about Data Virtualization. 

## 5.2 Define the Governance structure
Watson Knowledge Catalog provides a secure enterprise catalog management platform that is supported by a data governance framework. A catalog connects people to the data and knowledge that they need. The data governance framework ensures that data access and data quality are compliant with your business rules and standards. Watson Knowledge Catalog provides fine-grain control of which users can perform which tasks through a combination of user roles and permissions and collaborator roles that control what actions users can perform.
![wkc](/images/wkc.png)
![wkc_1](/images/wkc_1.png)
The data governance framework is composed of governance artifacts that enrich data assets and protect sensitive data from unauthorized access. Governance artifacts are organized in categories and subject to workflow. Data Stewards and Data Quality Analysts who are collaborators in categories and have the required roles can create governance artifacts, import artifacts from files, or import artifacts' from Knowledge Accelerators.
- A **catalog** is how you share assets across your enterprise («private community for your organization; collaborative workspaces»):
    - it’s a way to organize resources for many data science projects: data assets, operational assets, and the users who need to use the assets
    - Collaborators in a catalog have access to data assets without needing separate credentials or being able to see the credentials.
    - An asset in a catalog consists of metadata about data, including how to access the data, the data format, the classification of the asset, which collaborators can access the data and other types of metadata that describe the data. Data assets can include both relational data and unstructured data, such as PDF or Microsoft Office documents.
    - A catalog can be governed so that policies that enforce data protection rules can control access to data or mask sensitive data.
- The default catalog is created automatically after you install the Watson Knowledge Catalog service.
- **Governance Artifacts**: 
- You use governance artifacts for these purposes:
    - Enrichment: Artifacts can add knowledge and meaning to assets.
    - Control access: Artifacts can control who sees what data or which artifacts.
    - Identification: Artifacts can act as criteria to identify assets or data for other artifacts.
    - Quality: Artifacts can be used to analyze data quality dimensions.
- **Governance items**: 
    - **Categories**: Categories organize governance artifacts in a hierarchical structure similar to folders.
    You can use category roles to define ownership of artifacts, control their authoring, and restrict their visibility. Examples: Business Performance Indicators, Business Scopes
    - **Business terms**: Business terms implement a common enterprise vocabulary to describe the meaning of data.
    You create business terms to ensure clarity and compatibility among departments, projects, or products. Business terms are the core of your governance framework and typically form the bulk of your governance artifacts. You can manually assign business terms to data columns, tables, or files or automatically assign them during metadata enrichment. You can use business terms in governance rules and enforceable rules to identify the affected data. Examples: Customer lifetime value, Work phone number
    - **Data classes**: Data classes classify data based on the structure, format, and range of values of the data.
    Data classes are automatically assigned to matching data columns during profiling and metadata enrichment. You can create data classes by defining matching criteria with an expression or a reference data set. You can create relationships between data classes and business terms to link data format with business meaning. Related business terms are automatically assigned to data along with their related data classes. How well columns conform to their data class criteria contributes to data quality analysis. Before you have a robust set of business terms, you can use data classes in enforceable rules to identify the affected data. Examples: Phone number, Email address
    - **Reference data sets**: Reference data sets define standard values for specific types of data to classify data and measure consistency.
    Reference data sets act as lookup tables that map codes and values. You can include a reference data set in the definition of a data class as part of the data matching criteria. Some reference data sets are standardized by organizations, such as the International Organization for Standardization (ISO). Reference data can be hierarchical or mapped across related sets. Example: Country codes
    - **Classifications**: Classifications describe specific characteristics of the meaning of data. Predefined classifications describe the sensitivity of the data. You can create classifications to describe other characteristics of data or other governance items. For example, Knowledge Accelerators use classifications to classify categories and business terms. You can use classifications to construct governance policies and rules. Typically, you relate multiple business terms to each classification and then data is indirectly classified through its assigned business terms. You can also manually assign a classification to a data asset. Example: Sensitive Personal Information
    - **Policies**: Policies describe how to manage and protect data assets.
    You create policies by combining rules and subpolicies. You can include data protection rules and data location rules in policies to control and manage data. However, policies do not affect the enforcement of data protection rules and data location rules. You can include governance rules in policies to document standards and procedures. Example: Data sharing agreement
    - **Governance Rules**: Governance rules describe how to apply a policy.
    Governance rules provide a natural-language description of the criteria that are used to determine whether data assets are compliant with business objectives. Governance rules are not enforced by Watson Knowledge Catalog. However, you can relate governance rules to enforceable rules, such as data protection rules and data quality rules. Example: Customer name must not be null
    - **Data protection rules**: Data protection rules control access to data based on users and asset properties and assigned governance artifacts. Data protection rules control who can see what data. Within data protection rules, you can include classifications, data classes, business terms, or tags to identify the data to control. You specify to deny access to data or to mask sensitive data values. Data protection rules are automatically enforced in all governed catalogs. Data protection rules are not organized or controlled by categories.
    Example: Mask columns that are assigned the Passport Identifier business term.

## 5.3 Use smart ingestion for auto cataloging 
Note from the author: No idea what is meant by that 😊 
- Automatic term assignment (WKC): Automatic term assignment is the process of automatically mapping business terms to data assets and asset columns. Terms are automatically assigned to assets and columns as a part of column analysis, automated discovery, and quick scan.
- Terms are assigned automatically based on the confidence level. Initially these associations are represented as candidates which domain experts and stewards can review and assign manually. When the confidence level matches or exceeds 50%, terms are suggested to be assigned. When the confidence level matches or exceeds 80%, candidates are automatically assigned.
- Assignments can be added manually and they can be generated by methods. Suggestions are generated only by methods.
- When workflow is enabled, only published terms are assigned.

## 5.4 Understand how workflow is used in Cloud Pak for Data 
- You can use workflows to manage business processes. A workflow defines the sequence of steps that must be completed and the decisions that must be made to support a specific process.
- For example, you can use workflows to ensure that:
    - Purchase requests are reviewed by the right decision-makers.
    - Change requests are carefully considered before they are implemented or rejected.
    - Contracts are thoroughly reviewed in a timely manner
- Needs WKC
- Custom workflows: two kinds (custom governance artifact workflow, custom request workflow)

## 5.5 Explain the use of Guardium in auditing and monitoring data 
- IBM® Guardium® safeguards your sensitive information by auditing what is happening in your sensitive-data environments, such as your databases, data warehouses, file systems, or Big Data environments.
- Needs WKC
- One way that you can protect PII is by ensuring that you have security measures in place to prevent unauthorized access to your data. But in the event of a data security breach, it's also important to ensure that you have an audit trail so that you know who accessed the data, when they accessed it, where they accessed it, and what data they accessed.
- You can use the data governance features in IBM Cloud Pak for Data to identify sensitive data, including data that resides on Hadoop systems.
- High-level process to integrate CPD and Guardium
![guardium](/images/guardium.png)

## 5.6 Leverage the platform to understand data flow and usage 
TODO: add summary. 

## 5.7 Explain the concepts of Knowledge Accelerators 
- Align concepts from industry regulations and standards with your business data to accelerate regulatory compliance. It is now included in Watson Knowledge Catalog at no extra cost.
- Healthcare, Energy and utilities, Insurance, Financial services, Cross-industry
- Features: 
    - Extensive central vocabulary and KPIs: Supports enterprise data governance and auto-classification.
    - Out-of-the-box compliance support: Onboards and aligns multiple regulations and industry standards.
    - Importable business scopes: Uses separately importable business scopes for a quick start for specific business topics.

## 5.8 Map business opportunities into a data governance use case 
TODO



# Section 6 - Integration, Implementation, Deployment, and Scaling

[Back to top](#outline)

## 6.1 Develop an appropriate process to take a Data and AI solution from inception to production

### 6.1.1. Describe the characteristics of a viable pilot project

![garage](/images/garage.png)

## 6.2 Develop a strategy to monitor the Data and AI platform

Important terms: 
- An *event* is the report of the state of an entity such as a pod, persistent volume claim (PVC), or other resource. The following event types are delivered with Cloud Pak for Data.
- The *severity* of the event indicates the criticality of the event. The severity of an event can be: critical, warning, or info. Each type of event includes metadata for the event, including a description and steps to resolve the event.
    - critical - Monitored resources are unstable. Alerting is essential if this state persists.
    - warning - Monitored resources have reached a warning threshold. Immediate alerting might not be required.
    - info - Monitored resources behave as expected. Informational messages only.
- An *alert* is an event that indicates an issue or potential issue. Alerts can be sent by using either traps (SNMP) or email (SMTP). Each alert type can be associated with different alert rules. For example, an alert type might alert immediately or wait for an event to occur a specified number of times before the alert forwarder sends an alert.
- A *quota* for a resource, such as vCPUs and memory, is a target that determines the severity of an alert. If resource usage exceeds a quota, the event is considered critical. If resource usage exceeds the percentage of the quota that is defined by the alert threshold, the event is considered a warning.
- A *monitor* is a script whose purpose is to check the state of an entity periodically and generate events. A single monitor can register events for different purposes. For example, the diagnostics monitor that comes with Cloud Pak for Data generates events to check the status of persistent volume claims, stateful sets, and deployments.
- A *watchdog alert manager (WAM)* monitors all monitors to ensure that they run on schedule. The WAM also exposes an API that listens to events generated by the monitors. These events persist in Metastore for generating alerts when the alerting rules are met. The persisted events can also be used to study historic patterns. For more information, see Alerting APIs.
- An *alert profile* defines the setup for alerting. The default profile enables SMTP and SNMP.
- An *alert forwarder* is the service that is responsible for sending the alerts and traps. After the watchdog alert manager identifies a possible alert, it invokes the alert forwarder to forward them to the customer environment.

### 6.2.1. Describe the ability to provide metrics regarding compute and memory usage and trends. 
-> Monitoring page in the admin panel
- From the *Monitoring* page, you can:
    - See the current resource use (vCPU and memory) for the platform. If you click View status and use data on the Platform resource overview card, you can see a breakdown by services, service instances, environments, and pods.
    - Review the platform resource use for the last 12 hours. If you click View historical data on the Platform resource use card, you can see a breakdown by services, service instances, environments, and pods. You can also view historical data beyond 12 hours. By default, the platform stores up to 30 days of data. However, you can adjust the length of time that data is retained.
    - Access at-a-glance platform monitoring (Services, service instances, environments, pods) 
    - View events and alerts (From the Monitoring page, you can see: The number of critical alerts, The number of critical events, The number of warning alerts, The number of warning events)
    - Configure and enforce quotas (A quota is a way for you to specify the maximum amount of memory and vCPU you want the platform or a specific service to use. A quota is a target against which you can measure your actual memory and vCPU use. A quota acts as a benchmark to let you know when your vCPU or memory use is approaching or surpassing your target use. Setting and enforcing quotas: Important: To use quota enforcement, you must install the scheduling service.)

### 6.2.2. Describe the ability to alert at usage thresholds. 
TODO: add summary. 

### 6.2.3. Identify the types of alert notification protocols supported 
TODO: add summary. 

### 6.2.4. Identify how you can extend existing dashboard monitoring
- Developers can set up custom monitors using the alerting framework.
- Monitors can be registered into Cloud Pak for Data through an extension configmap. The configmap has all the details that are needed to create a cron job, including the details of the script, the image to be used, the schedule for the cron job, and any environment variables. This ensures that the alerting framework has all the necessary information to create a cron job, monitor events frequently, and trigger alerts if and when needed.

## 6.3 Accelerate the solution using Industry Accelerators and External Data sets 
- https://community.ibm.com/accelerators/?context=analytics 
- An industry accelerator is a set of artifacts that help you address common business needs. For example, you might use the Financial Markets Customer Attrition Prediction accelerator, which uses Cloud Pak for Data with Watson Knowledge Catalog, Watson Studio, and Watson Machine Learning to help you to predict the customers that might leave. You can browse the Accelerators catalog for the Cloud Pak for Data industry accelerators and download the ones that you want to use.

## 6.4 Integrating Business Applications using Cloud Pak for Data
TODO: add summary. 

### 6.4.1. Identify options of exposing a Machine learning model API 
TODO: add summary. 

### 6.4.2. Describe best practices when exposing APIs for external applications usage 
TODO: add summary. 

### 6.4.3. Describe use cases when a business application would integrate with Cloud Pak for Data
TODO: add summary. 


