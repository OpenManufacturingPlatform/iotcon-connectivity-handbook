[< Chapter 3: Principles for a Successful Connectivity Solution](03_Principles_for_a_Successful_Connectivity_Solution.md)

## 4 Type of Communication
The three different communication categories required to solve connectivity challenges are telemetry, control, and (device) management. Each one has unique properties, and the applicability of each varies according to individual solutions and level of communication within the network topography.

Each communication category can occur between the production assets & edge or edge & cloud (see Figure 3). We define this as the asset-edge interface or edge-cloud interface.

<figure>
	<img src="images/communication.png" alt="Communication">
	<figcaption>Figure 3: Three general communication types across three levels</figcaption>
</figure>


The most common and prolific category is telemetry, which is the sending of raw data from the shop floor into the cloud. Examples include vibration readings in the range of milliseconds, pressure readings twice per minute, and device state status every 5 minutes. The messages typically contain data (e.g., current temperature) and metadata such as device ID and a timestamp.

Control data are product job information, recipe settings, or process parameters from central or regional servers or cloud hosts. Often control data originates and stays in the production asset level because of time criticality. However, hybrid edge and cloud architectures are being used to enable manufacturing use cases that were impossible prior to these new techniques, for example, automating control actions that previously required specially trained personnel.

Management data can be bidirectional and helps to control devices or machines. This typically includes metadata with the purpose of ensuring the entire system is operating correctly. Machine-to-machine communication is monitored, and information is utilized to ensure smooth operation. Examples include heartbeat monitoring as well as checking communication packets and their completeness.

[Chapter 5.1: Implementation - Production Asset Level >](05a_Implementation_ProductionAssetLevel.md)
