---
title: "Failure Drill overview"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Failure_Drill_overview"
---

<span id="LjM9J0nZ"></span>
## What is Failure Drill

Direct Connect (DC) Failure Drill simulates failure scenarios to test the reliability of disaster recovery configurations between cloud and on\-premises. After connecting a new DC link to the data center, you can run a failure drill task to securely test and verify whether the networking reliability between the on\-premises data center and the cloud meets expectations in an isolated simulated failure scenario.

<div data-tips="true" data-tips-type="default">Tip</div>


<div data-tips="true" data-tips-type="default">The failure drill feature is in the beta stage. If you need a trial, please contact your account manager.</div>


<span id="V4DdgZVz"></span>
## Terms


|Name |Description |
|---|---|
|Failure drill task |A failure drill task is a task that injects simulated faults into the specified DC resources. A failure drill task can have multiple resources as drill objects concurrently. |
|Drill object |It refers to the execution target of the failure drill task. When the failure drill task runs, the system sets the drill object's status to Faulty or Unavailable. After the failure drill task finishes, the drill object's status restores Available. You need to complete redundancy configuration for drill objects before starting a drill task.<br><br>Supported drill object resources include **DC Connection** and **BGP Peer**:<br><br><br>* DC Connection: Simulate a failure in a [redundant-link](https://docs.byteplus.com/en/docs/directconnect/best-practices-overview#.5LiT57q_6L-e5o6l6K6_6Zeu5LqR5LiKVlBD) networking scenario where one DC Connection fails, validating whether network traffic automatically switches to another DC Connection.<br><br>* BGP Peer: Simulate a failure in a scenario with [redundant BGP Peers](https://docs.byteplus.com/en/docs/directconnect/Adding-a-BGP-peer), validating whether the Virtual Interface automatically switches routes between configured peers. |


<span id="V4DdgZVz"></span>
## Notes


* Each account supports concurrently running only one failure drill task per region.

* Each drill object supports being added to only one unfinished failure drill task.

* Each drill task supports adding only **Available** drill objects (DC Connections or BGP Peers).

* Failure drill tasks with drill objects as **DC Connection** do not support adding Shared Line instances.

* Accounts that have enabled the DC partner and Shared Virtual Interface features do not support the failure drill feature. For more usage limits on DC failure drills, see [Limits](https://docs.byteplus.com/en/docs/directconnect/Limits).


<span id="E4dUGv9R"></span>
## Usage process


<Tabs>
<Tab zoneid="LZBy28sCtA" title="Drill now">
<TabTitle>Drill now</TabTitle>

1. [Create a failure drill task](https://docs.byteplus.com/en/docs/directconnect/Creating_a_failure_drill_task) (Enable drill now).

2. [View DC event alarms](https://docs.byteplus.com/en/docs/directconnect/Configuring-event-monitoring-alerts).


</Tab>
<Tab zoneid="dHOjYl5STP" title="Manual start">
<TabTitle>Manual start</TabTitle>

1. [Create a failure drill task](https://docs.byteplus.com/en/docs/directconnect/Creating_a_failure_drill_task) (Disable drill now).

2. [Start the failure drill](https://docs.byteplus.com/en/docs/directconnect/Managing_a_failure_drill_task#HogfY6qS).

3. [View DC event alarms](https://docs.byteplus.com/en/docs/directconnect/Configuring-event-monitoring-alerts).


</Tab>
</Tabs>
