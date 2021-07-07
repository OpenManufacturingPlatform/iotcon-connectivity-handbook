[< Chapter 4.1: Infrastructural View](04_1_Views_on_Edge_Computing.md/#4_1_Infrastructural_View)

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
* Components for communication within an edge node and between distributed edge nodes
* Data (pre-)processing
* Data aggregation
* Semantic enrichment
* Components with specific business logic (e.g., edge analytics, machine learning)

<img width="874" alt="image" src="https://user-images.githubusercontent.com/3258579/124180919-b4857b00-da69-11eb-8bfe-8edd3788a4e5.png">

Basic connectivity and communication are fundamental for any edge application. The need to implement data pre-processing, aggregation and semantic enrichment functionalities typically scales with the size and complexity of the entire IoT solution (i.e., number and types of data sources, data volume, number of IoT applications, etc.).

The following needs to be considered to give an appropriate answer to the questions listed above:

* Message broker or API gateway to create loosely coupled architectures between edge applications and between edge nodes
* Synchronous and asynchronous communication patterns, dependingon the use case
* Defined, flexible payload formats for telemetry and command data
* Information models for semantic enrichment of the data
* Offline scenarios and data buffering capability
* Training of complex machine learning models where computing power is abundant (mostly cloud) and utilized at a level with sufficient access to the data flow while also taking bandwidth constraints into consideration (mostly edge)

In the reference use case, the Product Asset Connector retrieves the energy data from the PLC and forwards it to a message broker. The message broker ensures the exchange of messages between the different edge applications and connectors. The energy analysis component implements a custom-built business logic to recognize anomalies in the collected data. Therefore, the application receives the energy data from the message broker, performs the analyses, and publishes the result on the message broker. The cloud connector transfers the analysis results to the enterprise bus. The reference use case describes that a parameter is also changed on the PLC. The cloud connector and production asset connector transmit the new parameter from the enterprise bus to the PLC via the message broker.

<img width="506" alt="image" src="https://user-images.githubusercontent.com/3258579/124182569-df70ce80-da6b-11eb-9cd7-9a402bd754b2.png">

[Chapter 4.3: Operational View >](04_3_Operational_View.md)
