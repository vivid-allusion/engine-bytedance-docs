---
title: "Creating a flow log"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-a-flow-log"
---

## Instructions

A single account in a single region can create up to 10 flow logs.

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Flow Log**.

3. In the top menu bar, select the target project and region.

4. Activate Torch Log Service (TLS). If you have activated TLS, skip this step.

   1. Click **Authorize** to access the Cross\-Service Access Request page.

   2. Click **Authorize** to enable TLS.

5. Click **Create Flow Log**.

6. Configure relevant parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Billing method |Currently only support Pay\-as\-you\-go. |Pay\-as\-you\-go |
   |Name |Enter the name of flow log. |flowlog\-1 |
   |Resource Type |Select the resource type for flow log recording, which defines the scope of flow log collection.<br><br><br>* Virtual Private Cloud (VPC): Collects the traffic of all network interfaces within the VPC.<br><br>* Subnet: Collects the traffic of all network interfaces within the subnet.<br><br>* Network interface: Collects the traffic of a specified network interface. |VPC |
   |Resource |Based on the selected resource type, select the target resource to collect from the dropdown list. |VPC\-01 |
   |Traffic type |Select the traffic type, i.e., the type of traffic to be recorded in the flow logs.<br><br><br>* All Traffic: Collects all inbound and outbound traffic of the Network Interface.<br><br>* Permitted Traffic: Collects traffic allowed by security groups and network ACLs.<br><br>* Rejected Traffic: Collects traffic rejected by security groups and network ACLs. |Total traffic |
   |Sampling interval |Select the sampling interval for the flow log. The sampling interval is the time interval at which the VPC delivers flow log data to the Torch Log Service (TLS). For connections with continuous data packets, sampling interval also represents the maximum aggregation time for traffic data to be aggregated into a single log entry.<br><br><br>* 10 minutes: The flow log samples every 10 minutes, storing the traffic data within these 10 minutes to the Torch Log Service.<br><br>* 5 minutes: The flow log samples every 5 minutes, storing the traffic data within these 5 minutes to the Torch Log Service.<br><br>* 1 minute: The flow log samples every 1 minute, storing the traffic data within this 1 minute to the Torch Log Service. |10 minutes |
   |Version selection |Select the flow log version.<br><br><br>* Supports Version 1, Version 2, Version 3, and Version 4.<br><br>* Higher versions are backward compatible with all fields from lower versions and add new fields on top of them.<br><br>* For more details, see [Flow log overview](https://docs.byteplus.com/en/docs/vpc/Flow-log-overview). |Version1 |
   |Log project |Select a Log Project. A Log Project is the fundamental resource management unit in the TLS, used for tenant resource isolation and access control.<br><br><br>* Create a Log Project: Create a new log project by entering a name for it.<br><br>* Select Existing: Select an existing log project.  |New log project<br><br>vpc\-flowlog\-project\-1 |
   |Log topic |Select a Log Topic for the logs. A Log Topic is the fundamental unit in Log Service for log management (e.g., collection, storage, query, and analysis).<br><br><br>* Create New Log Topic: Create a new log topic. And automaticallyenable Automatic sharding. This Log Topic is managed by VPC Flow Logs. It can only be modified or deleted after the associated VPC Flow Logs are deleted.<br><br>* Use Existing: Select an existing log topic. If the existing log topic does not have automatically split log partitions enabled, exceeding the capacity of existing partitions may lead to data loss. Therefore, it is recommended to enable Automatic sharding.  |New log topic<br><br>vpc\-flowlog\-topic\-1 |
   |Enable index |Select Enable Indexing Indexes are used for searching and analyzing data. Flow Logs must be configured with indexes before you can perform search and analysis.<br><br><br>* When selected, the system will automatically configure key\-value indexing [based on flow log fields](https://docs.byteplus.com/en/docs/vpc/Flow-log-overview#.5rWB5pel5b-X5a2X5q61) within the log topic.<br><br>* If not selected, you must configure indexes for the flow logs in the log topic and enable field analytics Before analyzing the flow logs. See [Configure Index](https://docs.byteplus.com/en/docs/vpc/Configuring-an-index) for instructions. |**Check** |
   |Project |Select the project to which the flow log belongs. [Learn more](https://docs.byteplus.com/en/docs/vpc/Managing-projects) |default |
   |Tags |Add one or more custom tags to the flow log as needed.<br><br>A tag consists of a Tag Key and a Tag Value, and is used to categorize and organize flow logs. [Learn more](https://docs.byteplus.com/en/docs/vpc/Managing-tags) |flowlog:v1 |

7. View the configuration details in the upper right corner. Follow the console guidance to review and confirm the Legal.

8. Click **Buy now** to complete creation.

Flow Logs are automatically started after creation.

## What to do next

When creating a flow log, if the option to automatically create an index is not selected, you need to manually Configure index. After the configuration is complete, you can analyze the flow log. If selected, you can directly analyze the flow logs. See [Analyzing a flow log](https://docs.byteplus.com/en/docs/vpc/Analyzing-a-flow-log) for detailed operations.

## Related documents

[CreateFlowLog](https://docs.byteplus.com/en/docs/vpc/CreateFlowLog)
