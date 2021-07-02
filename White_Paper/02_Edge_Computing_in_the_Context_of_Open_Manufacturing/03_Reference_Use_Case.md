[< Chapter 2: Definition of Edge Computing](02_Definition_of_Edge_Computing.md)

## 3 Reference Use Case
To analyze the different aspects of edge computing, we define a reference use case used in the subsequent chapters to describe different technological viewpoints.

In our use case, a company wants to analyze the energy data of a drive and send anomalies to a cloud dashboard. Also, the analysis results are stored in a cloud storage service.

On the production asset level, a PLC<sup>2</sup> is connected to the drive through a real-time ethernet bus. The PLC monitors the high-frequency energy data and is able to publish them for other systems.

Since the amount of data generated is too large to be sent to the cloud without aggregation, a preprocessing must be done. This is executed on the _edge level_. An edge node consumes the energy data from the PLC via a modern protocol (e.g., OPC UA<sup>3</sup>).

The edge node provides two key application features:

1. _Communication_: The edge node acts as a two-way gateway. It establishes a secure connection southbound to the PLC and northbound to the cloud.

> <sup>2</sup> programmable logic controller

> <sup>3</sup> https://opcfoundation.org/

2. _Parameter analysis_: The edge node has a custom-defined business logic to recognize energy consumption-related anomalies of the drive. The analysis results are pushed to the communication module and sent to the cloud for visualization and further processing. The analysis logic can be a simple threshold detection or a more sophisticated machine learning model.

The edge node can be a device residing near the production floor or a virtual edge node in a plant data center.

On the _cloud level_, the aggregated data is distributed via an enterprise bus to a dashboard for user visualization purposes (hot path). In addition, it is stored in long-term storage (cold path). A process specialist interprets the results from the visualization and sets new parameters for the drive to reduce occurring energy spikes. These are published on the enterprise bus and received by the communication software on the edge device. Afterward, the parameters are set on the PLC and transferred to the drive.

As data accumulates in cloud storage, it is applied to train the machine learning model. New models are pushed down to the edge device at regular intervals to update the parameter analysis.

![image](https://user-images.githubusercontent.com/3258579/123733518-8711b500-d850-11eb-9f4c-b4c5c407b4c4.png)

[Chapter 4: Views on Edge Computing >](04_Views_on_Edge_Computing.md)