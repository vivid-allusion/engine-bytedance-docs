---
title: "Viewing instance health states"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Viewing-instance-health-status"
---

Instance health monitoring enables automatic detection of software and hardware running and collection of instance health data. This feature helps you check the health status of your instances on the console, making it easy for you to check and address issues.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* You can view the health states only for instances in the **Running** status.

* The system automatically checks the instance health states every 30 seconds, and will send you the exception details via event messages if the instance has an exception.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the top menu bar, select the region and project where the target instance resides.

3. In the left\-side navigation pane, select "Instances & Images \> Instances" to go to the Instances page.

4. Find the target instance by the instance name/ID.

5. In the "Instance name/ID" column, you can view the health status of the target instance, as shown in the table:

   
   |Status |Description |
   |---|---|
   |​No information displayed |If no exception is displayed in the "Instance name/ID" column of an instance in the **Running** status, this means that no exception within this instance is detected. |
   |Abnormal |Running issues are detected inside the instance or on the host (physical machine) of the instance. |
   


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps


* If your instance has an **exception**, BytePlus will send you the exception details via event notifications. For notification details, refer to [Receiving ECS event notifications](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications).

* To handle the exception yourself, refer to [Event type overview](https://docs.byteplus.com/en/docs/ecs/Event-type-overview).
