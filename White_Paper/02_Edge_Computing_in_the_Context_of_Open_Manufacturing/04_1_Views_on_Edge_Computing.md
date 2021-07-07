[< Chapter 3: Reference Use Case](03_reference_use_case.md)

## 4 Views on Edge Computing
This chapter will have three different views on edge computing: an _infras-tructural_, an _application_, and an _operational view_.

### 4.1 Infrastructural View
In general, an edge node consists of a compute node and a guest system. Part of the compute node is the physical hardware, operating system, and hypervisor. It allows running independent guest systems. A guest system consists of the container runtime as well as the containerized software itself.

<img width="514" alt="image" src="https://user-images.githubusercontent.com/3258579/124178437-67ec7080-da66-11eb-951c-f71a9881189e.png">

The first defining characteristic for edge nodes, from an infrastructural perspective, is the capability to run and manage containerized software.Therefore, the edge container runtime provides lightweight virtualization,i.e., no virtual machines with their own operating systems.The second defining characteristic is the ability to connect bidirectional the edge node to the cloud level and production asset level. This means,that a compliant edge infrastructure needs to handle direct or indirect connectivity to the cloud, e.g., through different network layers, and must deal with temporary offline situations. It is essential to point out that cloud connectivity needs to be achieved in a secure manner. Rather than undermining the security architecture that relies on strict network separation (aka perimeter), future platforms need to be aware of the users, data, services, and devices that are each a vital part of manufacturing platforms. In general, there are two major hosting solutions for edge nodes: virtualized in the plant data center or physical as an edge device on the shop floor level. Datacenter deployments predominantly use container orchestration and have the following benefits over edge devices:

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

[Chapter 4.2: Application View >](04_2_application_view.md)