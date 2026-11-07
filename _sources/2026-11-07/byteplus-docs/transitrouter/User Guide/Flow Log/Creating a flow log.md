---
title: "Creating a flow log"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Creating-a-flow-log"
---

<span id="9eJbKvYh"></span>
## Prerequisites

Please ensure that you have activated the Torch Log Service (TLS).

<span id="XDM5GnEm"></span>
## Instructions


* Within the same Transit Router (TR) instance, only one flow log can be configured per inter\-region attachment.

* Exceeding quotas for log projects and log topics in Torch Log Service (TLS) may cause inability to create TR flow logs. For quota details, see [Apply for resource quota](https://docs.byteplus.com/en/docs/tls/Apply_for_resource_quota).

* TR flow logs do not consume your network bandwidth. Feel free to use them.

* TR flow logs support statistics for fragmented packets.


<span id="TIupgKpe"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Flow Log** tab.

4. Click **Create Flow Log** and complete the parameter configuration based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Name |Enter the name of flow log. |trflowlog\-01 |
   |**Logging** |||
   |TR |Fixed to the TR instance you selected, no manual configuration required. |tr\-01 |
   |Logged resources |Select the inter\-region attachment for which you want to log traffic. |Inter\-Region Attachment \| attach\-CrossRegion |
   |Logging cycle |Select the interval for traffic collection. Supports 1 minute and 10 minutes. |1 minute |
   |Log format |Select fields to be included in the log. For the specific meaning of each field, see [Flow log fields](https://docs.byteplus.com/en/docs/transitrouter/Flow-log-overview#HTxSE84Z).<br><br><br>* **TR default format**: System\-default selected fields.<br><br>* **Custom format**: After selecting this format type, you can add or delete fields as needed, except for required fields. |TR default format \| ${srcaddr}${dstaddr}${srcport}${dstport}${protocol}${bytes}${tr\-id}${src\-region\-id}${dst\-region\-id}${tr\-attachment\-id}${packets}${start}${end}${packets\-lost\-no\-route}${packets\-lost\-blackhole}${direction} |
   |**Log storage** |||
   |Log project |Select the log project to store TR flow logs. Whether you create a new one or select an existing one, the associated log project will be managed by TR after the TR flow log is created successfully. It can only be deleted after the TR flow log is deleted.<br><br><br>* **Create a log project**: Enter the name for the new log project. Select this option to create a new one or if no log project is available.<br><br>* **Select an existing project**: Select this option if you have already created a log project. |Create a log project, tr\-log |
   |Log topic |Select the log topic to store TR flow logs. Whether you create a new one or select an existing one, the associated log project will be managed by TR after the TR flow log is created successfully. It can only be deleted after the TR flow log is deleted.<br><br><br>* **Create a log topic**: Enter the name for the new log topic. Select this option to create a new one, or if no log topic exists under an existing log project.<br><br>* **Select an existing topic**: Log topics managed by other cloud services cannot be selected, such as log topics used by VPC flow logs. |Create a log topic, tr\-log\-topic |
   |**Advanced option** |||
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Tags)<br><br>Click Add tag, then type a tag key and a tag value to add a tag to the flow log. |* Tag key: trflowlog\-k1<br><br>* Tag value: trflowlog\-v1 |
   

5. Click **OK** to complete the action.


<span id="HN1nzn38"></span>
## What to do next


* After the flow log is successfully created, the Transit Router (TR) collects and reports log information to the Torch Log Service (TLS) according to the specified collection interval. After this interval, you can see [Searching and analyzing flow logs](https://docs.byteplus.com/en/docs/transitrouter/Analyzing-a-flow-log) to view log information.

* After the flow log is successfully created, you can click the **edit** icon in **Logging cycle** column to select a new collection interval.


<span id="hve2Gaj8"></span>
## Related documentation


* [CreateTransitRouterFlowLog](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterFlowLog): Create a flow log for a TR attachment.

* [ModifyTransitRouterFlowLogAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterFlowLogAttributes): Modify the name, description, or collection period of a TR flow log.
