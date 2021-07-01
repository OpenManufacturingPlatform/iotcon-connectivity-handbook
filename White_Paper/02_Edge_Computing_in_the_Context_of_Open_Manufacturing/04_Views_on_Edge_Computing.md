[< Chapter 03: Reference Use Case >](03_Reference_Use_Case.md)

## 4 Views on Edge Computing
This chapter will have three different views on edge computing: an _infras-tructural_, an _application_, and an _operational view_.

### 4.1 Infrastructural View
In general, an edge node consists of a compute node and a guest system.Part of the compute node is the physical hardware, operating system, andhypervisor. It allows running independent guest systems. A guest systemconsists of the container runtime as well as the containerized softwareitself.

<img width="514" alt="image" src="https://user-images.githubusercontent.com/3258579/124178437-67ec7080-da66-11eb-951c-f71a9881189e.png">

The first defining characteristic for edge nodes, from an infrastructuralperspective, is the capability to run and manage containerized software.Therefore, the edge container runtime provides lightweight virtualization,i.e., no virtual machines with their own operating systems.The second defining characteristic is the ability to connect bidirectionalthe edge node to the cloud level and production asset level. This means,that a compliant edge infrastructure needs to handle direct or indirect connectivity to the cloud, e.g., through different network layers, and must deal with temporary offline situations. It is essential to point out that cloud connectivity needs to be achieved in a secure manner. Rather than undermining the security architecture that relies on strict network separation (aka perimeter), future platforms need to be aware of the users, data, services, and devices that are each a vital part of manufacturing platforms. In general, there are two major hosting solutions for edge nodes: virtualized in the plant data center or physical as an edge device on the shop floor level. Datacenter deployments predominantly use container orchestration and have the following benefits over edge devices:

* Higher availability
* Better scalability
* Lower costs for operations (for large scale)
* No additional hardware and wiring in the cell required

Nevertheless, there are also many scenarios where physical edge devices are needed. Examples are:

* Data preprocessing (e.g.,filtering, aggregation) in the production cell because network load needs to be reduced
* Run AI-based control loops to achieve lower latency
* The connection of additional peripheral hardware is required
* Offline scenarios (without data center connectivity)
* Translation of non-secure protocol to secured ones
* Low costs and time to usage for initial proof of concept implementations

Possible edge node realizations can be Industrial PCs, Edge Gateways or PLCs.

As a general rule, the hosting level (_cloud, data center, device_) should be chosen as “high” as possible and as “low” as required by the use case and desired functionality.

Looking at the reference use case, a defining feature that can drive the hosting decision is the large amount of data being pre-processed. If raw data from multiple drives is published on the network, this can lead to bandwidth issues. Therefore local preprocessing on the edge device is beneficial.
On the other hand, the processing power and scalability of the solution must also be considered when an excessive amount of resources are needed for analyzing the data. This may lead to an edge node hosted in the data center and potentially require specific network requirements for throughput optimization.

### 4.2 Application View
The application view describes functional components deployed on an edge node that are required to fulfill the OT and IT application requirements. The functional components come as containerized software to match architecture and infrastructure requirements as described in the requisite sections.

Typical questions from an application perspective are:

* How can standardized communication within a distributed edge environment up to the cloud be enabled and managed?
* How can diverse data sources be standardized and transformed to move the entire solution towards a common semantic modeling approach?
* How can custom business logic components be integrated with standardized connectivity modules?
* How can data storage between distributed edge nodes be managed?
* Where does business logic reside, and how is it managed between the edge and cloud environment?

Hence, the application view needs to include multiple components with a range of different capabilities:

* Cloud connectivity
* Production asset connectivity
* Components for communication within an edge node and between dis- tributed edge nodes
* Data (pre-)processing
* Data aggregation
* Semantic enrichment
* Components with specific business logic (e.g., edge analytics, machine learning)

<img width="874" alt="image" src="https://user-images.githubusercontent.com/3258579/124180919-b4857b00-da69-11eb-8bfe-8edd3788a4e5.png">

Basic connectivity and communication are fundamental for any edge application. The need to implement data pre-processing, aggregation and semantic enrichment functionalities typically scales with the size and com- plexity of the entire IoT solution (i.e., number and types of data sources, data volume, number of IoT applications, etc.).

The following needs to be considered to give an appropriate answer to the questions listed above:

* Message broker or API gateway to create loosely coupled architectures between edge applications and between edge nodes
* Synchronous and asynchronous communication patterns,dependingon the use case
* Defined, flexible payload formats for telemetry and command data
* Information models for semantic enrichment of the data
* Offline scenarios and data buffering capability
* Training of complex machine learning models where computing power is abundant (mostly cloud) and utilized at a level with sufficient access to the data flow while also taking bandwidth constraints into consideration (mostly edge)

In the reference use case, the Product Asset Connector retrieves the energy data from the PLC and forwards it to a message broker. The message broker ensures the exchange of messages between the different edge ap- plications and connectors. The energy analysis component implements a custom-built business logic to recognize anomalies in the collected data. Therefore, the application receives the energy data from the message broker, performs the analyses, and publishes the result on the message broker. The cloud connector transfers the analysis results to the enterprise bus. The reference use case describes that a parameter is also changed on the PLC. The cloud connector and production asset connector transmit the new parameter from the enterprise bus to the PLC via the message broker.

<img width="506" alt="image" src="https://user-images.githubusercontent.com/3258579/124182569-df70ce80-da6b-11eb-9cd7-9a402bd754b2.png">

### 4.3 Operational View
Since applications in the manufacturing sector have special requirements in terms of stability and automation, an integrated operational approach for the edge nodes is essential. This chapter focuses on the functions that are important to manage the edge node through its lifecycle.

As described in chapter 4.1, it is possible to host the edge node either in the plant data center or on a computing unit on the shop floor next to the production asset. From an operational point of view, both options have their own challenges.

<img width="854" alt="image" src="https://user-images.githubusercontent.com/3258579/124182717-18a93e80-da6c-11eb-9fd0-691b935a2106.png">

An edge node also goes through the characteristic device lifecycle phases described in [OMP IOTCON 2020]<sup>1</sup>. Each lifecycle phase has specific requirements for successful execution. These requirements are generally met with additional cloud services. The predominant supporting cloud services are the Edge Node Management & Onboarding Service, the Monitoring Service, the Security Service, and the Edge Node Twin.

**Management & Onboarding Service**: Generally, this cloud service has the task of fetching the current or setting the desired state of connected edge nodes.

In the _provision phase_, the service onboards new edge nodes. The first step is to create digital identities. The digital identity can originate from existing asset management systems. The service can also save and manage target configurations of edge nodes.

The Management & Onboarding Service provides an endpoint where edge nodes initiate a connection. For this, a basic setup of the edge node must be performed. Example actions are installing the operating system, provi- sioning the agents, and providing security credentials.

After the initial connection is complete, the edge node offers basic selfdescribing characteristics (state). A few examples are the firmware version and node settings. The node state is compared with the target configuration from the service. If deviations occur, a state update is sent down to the edge node. State updates can be security or policy updates, changed configurations, and application versions (containers). In our reference use case, a configuration would be the thresholds to identify anomalous energy consumption patterns.

State updates resulting in edge node downtime that interfere with production are not possible at any time. Therefore, careful consideration should be given to scheduling the updates at an appropriate time.

Customized parameters are required to adapt the installed application to the specific use case. These parameters are pushed to the edge node and applied to the application in the _configuration phase_. An example can be a configuration file that is loaded onto the storage (e.g., hard drive) and fetched by the containers on startup. This is the same when updates occur in the _operations phase_ (see Edge Node Twin).

The final phase is _retirement_. On _physical_ edge nodes, a retirement is initiated by a hardware failure or an upgrade cycle. The hardware is exchanged, and the existing identity with its state is transferred to the new device. To reduce downtime in manufacturing scenarios, this relocation must be done by the service as seamlessly (i.e., automatically) as possible. On virtual edge nodes, a failure results in starting a new edge node and in the transferal of the digital identity.

If the edge node can be fully retired, the digital identity is removed from the edge node management service to prevent further access, both in physical or virtual edge node cases.

The **Cloud Monitoring Service** collects all log and metric information from edge nodes. Information can originate from the host system as well as from the running container applications. Therefore, the edge runtime and the applications must support this mechanism.

Via the service, it is possible to create alerting mechanisms (e.g., on allocated memory) which are applied as stream analysis on the incoming data. In the _provisioning phase_, the edge node establishes a connection to the monitoring service. Afterwards, alerts, as well as logs and metrics, can be used throughout the following _configuration_ and _operations phase_. They are used to determine the system’s health and perform incident traceability.

To obtain meaningful results, the log messages must have a defined format. Common components are message origin, severity, content, UTC times- tamp, and correlation id to ensure better traceability.

The **Security Service** is responsible for managing the secure entities of the edge node and its applications. In the _provisioning phase_, the edge node connects to the cloud service the first time, and they exchange their trust entities. In a scenario of large-scale installation of physical edge nodes, a default certificate could be provided, which is valid for the first connection. After the connection to the service, it gets exchanged by the security service. For this, the service needs access to the relevant certificate au- thorities (CAs).

A second task is policy enforcement. This is done by a comparison of a target state with the current device state. Examples are updating the host system and the application of security rules, like disabling ports.

In the _configuration phase_, the security service supports the edge application configuration by handling security-related tasks, e.g., installing certificates to connect to third-party services. Also, edge applications can manage their secrets in a secure manner through this service. In the _operations phase_, continuous monitoring of vulnerability databases is performed. Any findings can result in potential updates of the target states. In the _retirement phase_, the revocation of the security entities of an edge node takes place.

Another relevant service is the **Edge Node Twin**. Its job is to synchronize application parameters between the cloud service and the edge nodes. Therefore, its main use is in the _operations phase_. Possible configuration parameters are stored in an “edge node twin” representation in the service. Changes made on the twin’s parameters are synchronized via the Device Management Service. A possible example is the adoption of a threshold value inside an application.

The parameter is generally reflected as hierarchically organized key-value-pairs. As a prerequisite, the edge container runtime has to be able to receive these parameters and provide them to the container applications. The container applications themselves need to be able to interpret them and change dynamically based on the given values from the twin service.

In our case, the process specialist analyzes the visualized data in the cloud dashboard and then sets new values in the Edge Node Twin to reduce the energy consumption.

[Chapter 05: Outlook >](05_Outlook.md)