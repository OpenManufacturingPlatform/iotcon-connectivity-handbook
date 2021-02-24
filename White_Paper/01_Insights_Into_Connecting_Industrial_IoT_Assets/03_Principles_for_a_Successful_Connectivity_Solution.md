[< Chapter 2: Breadth and Depth](02_Breadth_and_Depth.md)

## 3 Principles for a Successful Connectivity Solution
### 3.1 Leveraging the Cloud
Compute, storage, analytics, and other cloud services are secure, feature-rich, and highly scalable from essentially anywhere in the world. In today’s globally integrated networks of factories and supply chains, these features enable OT and IT managers to build, deploy, and grow solutions quickly and at low costs. These efficiencies are coupled with the tradeoff of control or freedom. Careful architectural planning (e.g., defining a business domain model) and the application of cloud principles, such as containerization, enable a technology manager to realize the benefits while minimizing the tradeoffs.

### 3.2	Building with Open Standards
Open standards have been used in the manufacturing sector for decades, providing functionality such as field and controller level communications and controller level operations. This approach has helped avoid some vendor lock-in, but there is room for increased proliferation and further leveraging of open standards. This is precisely the mission of the Open Manufacturing Platform.

### 3.3	Implementing a Platform Approach
As factories are both idiosyncratic and standardized along many different dimensions, any technology solution must account for the differences while leveraging the similarities. Devising a technology platform approach up-front enables rapid, consistent solution building and deployment while also allowing custom solutions that leverage a common core. Platforms are open for extension but closed for modification, thus providing scalability while minimizing breakage. They favor standard features and functionality over specifics tuned to one line or site. With stable, open, and well-documented APIs (Application Program Interface), provide a framework in which clients can implement their extensions with confidence and ensure interoperability. Additionally, security reviews of the core services can be centrally managed, and policies can be applied one-time, at platform design and deployment. From then on, any application or service that utilizes the platform automatically benefits from the security policies already being put in place.

### 3.4	Leveraging Machine Learning and Artificial Intelligence
Manufacturing professionals have been optimizing operations and processes along the value chain for a long time. Traditionally, experts possessing intimate, proprietary knowledge of their particular machines, production cells, and assembly lines performed this optimization. In this people-centric analog environment, cross-domain orchestration and optimization is complex and typically does not scale to other production sites. With the connection of OT assets and the introduction of artificial intelligence (AI) and machine learning (ML) capabilities from the cloud, data can be used from one site to train ML models, and additional sites can take advantage of the resulting learnings. As new sites are connected and leveraged through algorithms and ML models, new data from those locations enhance the data set. Feedback communication is sent from the cloud-based models back down to the shop floor to implement changes based on these learnings. As ML models become trained and their results gain reliability, insights from the cloud trigger actions on the shop floor. Closed feedback loops generate virtuous cycles of learning, adapting, and efficiencies.

### 3.5	Consistent Device Management
A uniform approach to device management over the entire life cycle is required to ensure efficient administration of the many devices on the shop floor. The device lifecycle can be thought of as five discrete phases, each with its own requirements and goals.

<br>
<b>

<figure>
	<img src="images/lifecycle.png" alt="Lifecycle">
	<figcaption>Figure 2: Typical Device Lifecycle</figcaption>
</figure>
</b>

<br>
<br>

The planning phase includes developing an understanding of the expected use cases that drive the device capability requirements and is critical to both the individual device level and the system or solution level. This phase also includes elements of cost estimates, procurement, inventory, and implementation planning. Cataloging the devices in both brownfield and greenfield scenarios is an essential and very company-specific task with many dependencies needing consideration (e.g., network architecture and design, existing protocols, number of connected devices). Embracing open standards and automatic device discovery can be good solutions for speeding up this process.

Provisioning is the process of getting the hardware ready for deployment, including physical installation, integration into device management software, testing, and basic setup with other supporting systems such as an edge node.

Next, a device needs to be configured by setting different parameters to manage the software operations. This enables bulk updates, such as to the firmware, management of security, and ongoing operations.

* Download of software 
* Setting the software parameter, e.g., parameters like endpoints, selection of data points, sampling, and publishing intervals 
* Prepare interface on OT device, e.g., information model, data model, and message model
* Establish a connection to the device and cloud level

Operating the device includes collecting device telemetry, performing ongoing maintenance and management, and ensuring optimal performance. Holistic device and system monitoring are necessary to guarantee the greatest possible operational stability. In case of failure, it is essential to carry out an analysis with the help of a monitoring service. The flexibility to exchange hardware and software and update, reconfigure, and restore the connectivity solution with the help of a provisioning service is also fundamental.

The final stage is retirement, which is typically initiated by the end of the device service life, a device failure, or an upgrade cycle. Depending on the scenario, it will end up in a replacement or termination. In case of replacement, the faulty device should be replaced as soon as possible to avoid downtimes. Therefore, the device management service needs to configure the device automatically. In the event of device termination, information must be removed from the device management service, and firewall rules must be deactivated.

[Chapter 4: Type of Communication >](04_Type_of_Communication.md)
