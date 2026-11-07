---
title: "Starting or restarting instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Starting-or-restarting-an-instance"
---

After installing the cloud assistant Agent for an instance, you need to start or restart the instance before the cloud assistant Agent can take effect.

> If you install the cloud assistant Agent manually by executing scripts or via OpenAPI, you do not need to start or restart the instance.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [installed the cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5ZCv5Yqo5a6e5L6L"></span>
### Run instances

When the Agent of an instance is in a **To start** state, you can start the corresponding instance on the Agent management page and run the cloud assistant Agent.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Agent management" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Select the target instance, and start the instance, as well as the cloud assistant Agent.

   * **Start multiple instances at one time**

      1. On the Agent list page, select target instances that you need to start.

         > You can select up to 50 instances at a time.         
         

      1. Click the "Start" button below the list.

      2.  Confirm whether you can start selected instances. If you can not start some selected instances, click the "Disallow start instance" tab to resolve issues as instructed, and then restart instances. Or, you can ignore instances on the "Disallow start instance" tab first and click the "Confirm" button to start instances on the "Allow start instance" tab.

   * **Start one instance**

      1. Search for or query information about the target instance from the instance list.

      2. Click the "Start" button in the "Action" column on the right side of the target instance.

      3. After you confirm the information, click the "Confirm" button.

4. After the instance starts, the Agent status changes to **In service**.


<span id=".6YeN5ZCv5a6e5L6L"></span>
### Restart instances

When the Agent of an instance is in a **To restart** or **error** status, you can restart the corresponding instance on the Agent management page quickly. After this, the cloud assistant Agent can take effect.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Agent management" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Select the target instance to restart.

   * **Restart multiple instances at the same time**

      1. On the Agent list page, select the target instances that you need to restart.

         > You can select up to 50 instances at a time.         
         

      2. Click the "Restart" button below the list.

      3. Confirm whether you can restart selected instances. If you can not restart some selected instances, click the "Disallow restart instance" tab to resolve issues as instructed, and then restart instances. Or, you can ignore instances on the "Disallow restart instance" tab first and click the "Confirm" button to restart instances on the "Allow restart instance" tab. 

   * **Restart one instance**

      1. Search for or query information about the target instance from the instance list.

      2. Click the "Restart" button in the "Action" column on the right of the target instance.

      3. Click "Confirm" to complete the operation.

4. After the instance restarts, the Agent status changes to **In service**.
