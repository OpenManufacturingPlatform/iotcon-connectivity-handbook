[< Chapter 4.2: Application View](04_2_application_view.md)

### 4.3 Operational View
Since applications in the manufacturing sector have special requirements in terms of stability and automation, an integrated operational approach for the edge nodes is essential. This chapter focuses on the functions that are important to manage the edge node through its lifecycle.

As described in chapter 4.1, it is possible to host the edge node either in the plant data center or on a computing unit on the shop floor next to the production asset. From an operational point of view, both options have their own challenges.

<img width="854" alt="image" src="https://user-images.githubusercontent.com/3258579/124182717-18a93e80-da6c-11eb-9fd0-691b935a2106.png">

An edge node also goes through the characteristic device lifecycle phases described in [OMP IOTCON 2020]<sup>1</sup>. Each lifecycle phase has specific requirements for successful execution. These requirements are generally met with additional cloud services. The predominant supporting cloud services are the Edge Node Management & Onboarding Service, the Monitoring Service, the Security Service, and the Edge Node Twin.

**Management & Onboarding Service**: Generally, this cloud service has the task of fetching the current or setting the desired state of connected edge nodes.

In the _provision phase_, the service onboards new edge nodes. The first step is to create digital identities. The digital identity can originate from existing asset management systems. The service can also save and manage target configurations of edge nodes.

The Management & Onboarding Service provides an endpoint where edge nodes initiate a connection. For this, a basic setup of the edge node must be performed. Example actions are installing the operating system, provisioning the agents, and providing security credentials.

After the initial connection is complete, the edge node offers basic self-describing characteristics (state). A few examples are the firmware version and node settings. The node state is compared with the target configuration from the service. If deviations occur, a state update is sent down to the edge node. State updates can be security or policy updates, changed configurations, and application versions (containers). In our reference use case, a configuration would be the thresholds to identify anomalous energy consumption patterns.

State updates resulting in edge node downtime that interfere with production are not possible at any time. Therefore, careful consideration should be given to scheduling the updates at an appropriate time.

Customized parameters are required to adapt the installed application to the specific use case. These parameters are pushed to the edge node and applied to the application in the _configuration phase_. An example can be a configuration file that is loaded onto the storage (e.g., hard drive) and fetched by the containers on startup. This is the same when updates occur in the _operations phase_ (see Edge Node Twin).

The final phase is _retirement_. On _physical_ edge nodes, a retirement is initiated by a hardware failure or an upgrade cycle. The hardware is exchanged, and the existing identity with its state is transferred to the new device. To reduce downtime in manufacturing scenarios, this relocation must be done by the service as seamlessly (i.e., automatically) as possible. On virtual edge nodes, a failure results in starting a new edge node and in the transferal of the digital identity.

If the edge node can be fully retired, the digital identity is removed from the edge node management service to prevent further access, both in physical or virtual edge node cases.

The **Cloud Monitoring Service** collects all log and metric information from edge nodes. Information can originate from the host system as well as from the running container applications. Therefore, the edge runtime and the applications must support this mechanism.

Via the service, it is possible to create alerting mechanisms (e.g., on allocated memory) which are applied as stream analysis on the incoming data. In the _provisioning phase_, the edge node establishes a connection to the monitoring service. Afterwards, alerts, as well as logs and metrics, can be used throughout the following _configuration_ and _operations phase_. They are used to determine the system’s health and perform incident traceability.

To obtain meaningful results, the log messages must have a defined format. Common components are message origin, severity, content, UTC timestamp, and correlation id to ensure better traceability.

The **Security Service** is responsible for managing the secure entities of the edge node and its applications. In the _provisioning phase_, the edge node connects to the cloud service the first time, and they exchange their trust entities. In a scenario of large-scale installation of physical edge nodes, a default certificate could be provided, which is valid for the first connection. After the connection to the service, it gets exchanged by the security service. For this, the service needs access to the relevant certificate authorities (CAs).

A second task is policy enforcement. This is done by a comparison of a target state with the current device state. Examples are updating the host system and the application of security rules, like disabling ports.

In the _configuration phase_, the security service supports the edge application configuration by handling security-related tasks, e.g., installing certificates to connect to third-party services. Also, edge applications can manage their secrets in a secure manner through this service. In the _operations phase_, continuous monitoring of vulnerability databases is performed. Any findings can result in potential updates of the target states. In the _retirement phase_, the revocation of the security entities of an edge node takes place.

Another relevant service is the **Edge Node Twin**. Its job is to synchronize application parameters between the cloud service and the edge nodes. Therefore, its main use is in the _operations phase_. Possible configuration parameters are stored in an “edge node twin” representation in the service. Changes made on the twin’s parameters are synchronized via the Device Management Service. A possible example is the adoption of a threshold value inside an application.

The parameter is generally reflected as hierarchically organized key-value-pairs. As a prerequisite, the edge container runtime has to be able to receive these parameters and provide them to the container applications. The container applications themselves need to be able to interpret them and change dynamically based on the given values from the twin service.

In our case, the process specialist analyzes the visualized data in the cloud dashboard and then sets new values in the Edge Node Twin to reduce the energy consumption.

[Chapter 5: Outlook >](05_outlook.md)