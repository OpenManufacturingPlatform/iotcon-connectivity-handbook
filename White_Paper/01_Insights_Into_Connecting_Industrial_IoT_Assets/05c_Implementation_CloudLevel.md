[< Chapter 5.2: Implementation - Edge Level](https://github.com/ChiaraK20/iot_connectivity/blob/proposal/Technical_Specification/1_Introduction/05b_Implementation_EdgeLevel.md)

## 5 Implementation
### 5.3	Cloud Level
Cloud services make use of flexibility, high computing power, and large storage capacities. In order to connect these services to shop floor equipment, a service is necessary that acts as the interface for receiving and sending messages to and from the lower levels. Thereby the data can be analyzed, visualized, and longtime stored. For example, cloud computing power can be used to train machine learning models based on data from the shop floor.

The Cloud Integration Hub is the cloud endpoint for any data receiving and sending to the lower levels, independent of the communication type. For security reasons, no upper level should actively establish a connection to a lower level. That’s why the Cloud Integration Hub is a passive service. Edge nodes or OT devices can connect to the service and get authorized by providing credentials. The Cloud Integration Hub doesn’t have to be one component. It might also be feasible that there are different components for different purposes and communication types.

For telemetry messages, a streaming-based solution optimized for high data throughput is recommended. Simple integration interfaces for other cloud services and an ability to distribute the data to different services should be supported.

As control data flows are bidirectional, two interfaces are necessary for sending and receiving control messages. The reliable transmission of the messages should be the focus.

Management data is received, sent, and stored by the Device Management Service. The Service provides provisioning, operating, and monitoring functionality for edge nodes and OT devices. It can install and update the firmware, manage the edge container, and supervise the security status of the devices. In addition, it stores all device-related information like device name, IP (Internet Protocol) address, configurations, installed edge container, and firmware status. If a device exchange is necessary, the information can be transferred to a new device.

From a security point of view, the cloud level provides centralized certificate management as well as identity and access control (IAC). Certificate management is essential to secure communication. The management needs to provide creation, renewal, revocation, and updated for all devices over the whole device lifecycle. The IAC is protected from unwanted modifications and can be used in combination with audit logs. As a best practice, the IAC should provide service principles to allow device management in unattended mode (e.g., to renew device certificates).

[Chapter 5.4: Implementation - Interface btw. Production Asset and Edge Level >](https://github.com/ChiaraK20/iot_connectivity/blob/proposal/Technical_Specification/1_Introduction/05d_Implementation_InterfaceProdEdge.md)
