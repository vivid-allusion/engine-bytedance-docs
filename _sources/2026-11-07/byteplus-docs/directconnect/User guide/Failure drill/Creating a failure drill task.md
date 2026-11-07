---
title: "Creating a failure drill task"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Creating_a_failure_drill_task"
---

<span id="TwK745Oe"></span>
## Scenarios

In a scenario where a new Direct Connect (DC) link accesses the data center, you can perform a failure drill to verify the reliability of the DC Connection and BGP Peer redundancy failover.

<span id="RDz7IvTT"></span>
## Prerequisites


* You have completed networking between your on\-premises data center and the Virtual Private Cloud (VPC). For procedure, see [Quick start for Direct Connect](https://docs.byteplus.com/en/docs/directconnect/Quick-start).

* You have completed redundancy configuration for related drill objects.

   * DC Connection: For dual\-link redundancy disaster recovery solutions, see [Best Practices: Redundant-link access](https://docs.byteplus.com/en/docs/directconnect/best-practices-overview#.5LiT57q_6L-e5o6l6K6_6Zeu5LqR5LiKVlBD).

   * BGP Peer: Configure multiple BGP Peers for the DC Virtual Interface based on [Adding a BGP Peer](https://docs.byteplus.com/en/docs/directconnect/Adding-a-BGP-peer).

* You have configured relevant event monitoring for the DC Connection in Cloud Monitor. [Learn more](https://docs.byteplus.com/en/docs/directconnect/Configuring-event-monitoring-alerts)


<span id="RDz7IvTT"></span>
## Procedure


1. Log in to [the Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the left\-side navigation pane, select **Failure Drill**.

3. Click **Create task** and configure the parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Regions |Select the region to which the failure drill object belongs.<br><br>Private networks in different regions are isolated. We recommend selecting a region closest to your business for lower network delays and faster access. |China (Beijing) |
   |Name |Set the failure drill name. |Fault\-test\-dc\-01 |
   |**Task configuration** |||
   |Drill object |You can only add resources whose status is **Available** as drill objects. When the failure drill task runs, the system sets the drill object's status to Faulty or Unavailable.<br><br><br>* DC Connection: DC Connections associated with cross\-account resources do not support failure drills.<br><br>* BGP Peer: Only BGP peers whose session status is **Up** support failure drills. |DC Connection \| dc\-01 |
   |Drill now |* Enable drill now: The failure drill task starts immediately after creation.<br><br>* Disable drill now: The failure drill task will be in **Drill pending** status after creation. You can [modify the failure drill task](https://docs.byteplus.com/en/docs/directconnect/Managing_a_failure_drill_task#8NYUJd3p) and manually [start the drill](https://docs.byteplus.com/en/docs/directconnect/Managing_a_failure_drill_task#HogfY6qS) at any time.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Ensure you have completed redundancy configuration. Otherwise, the failure drill may cause service disruption.</div><br> |Disable |
   |Drill duration |Set the failure drill duration. Set at least 1 minute, and at most 72 hours (4320 minutes). |180 minutes |
   

4. Click **Create** to complete the action.


<span id="8gFruXT1"></span>
## What to do next


* (Optional) [Start a failure drill](https://docs.byteplus.com/en/docs/directconnect/Managing_a_failure_drill_task#HogfY6qS): For a failure drill task without Drill now enabled, you need to start the failure drill manually.

* [View event monitoring](https://docs.byteplus.com/en/docs/directconnect/Configuring-event-monitoring-alerts#.5p-l6K-i5bey5Y-R55Sf5LqL5Lu2): After the failure drill ends, you can review DC event alarms to confirm that the redundancy failover was triggered and executed successfully in the failure scenario. If you receive a DC\-related alarm from Cloud Monitor, it means the drill object cannot switch lines/routes as expected. Check the relevant configuration.


<span id="oN19hMlP"></span>
## Related documents

[CreateFailoverJob](https://docs.byteplus.com/en/docs/directconnect/CreateFailoverJob): Create a failure drill task.
