---
title: "Authorizing shutdown repair"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/File-system-exception-shutdown-repair-operation-and-maintenance-description"
---

This topic describes how to authorize shutdown repair when the file system of a volume (system volume) is damaged.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Repairing the file system of a volume (system volume) causes the loss of all data stored on the original system volume. Please proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">If you do need to repair the file system, we recommend that you back up the volume (system volume) data in advance with the <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot">snapshot</a> feature to prevent any data loss.</div>


* <div data-tips="true" data-tips-type="warning">Currently, you can only authorize shutdown repairs for Windows instances.</div>



<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

When you receive an InstanceFileSystemFailure.StopAndRepair (downtime repair due to file system exception) event, you can authorize BytePlus to perform the shutdown repair to restore normal operations of the instance. For details, refer to [File system exception repair instructions of Byteplus](https://docs.byteplus.com/en/docs/ecs/File_system_exception_repair_instructions).

> File system exceptions may cause issues such as instance start failure, connection failure, and other issues.


<span id=".5pON5L2c5q2l6aqk"></span>
## Usage notes


* After you authorize the shutdown repair, the instance status is **MAINTENING**. Additionally, you can not start the instance, replace the system volume, initialize the system volume, or change the specification for it.

* BytePlus automatic repair capability requires the instance to be in a stopped status. We recommend that you [stop the instance](https://docs.byteplus.com/en/docs/ecs/Stopping-instances) first. If the instance is not in a **Stopped** status, BytePlus will forcibly stop it.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events" to go to the Events page.

3. In the top menu bar, select the region and project of your business.

4. On the Events page, you can search the shutdown repair event due to the file system exception based on the time range, event ID, or instance ID.

5. Click the "Authorize shutdown repair" button in the "Actions" column of the target event.

6. Select to execute the shutdown repair now and agree to maintenance authorization.

7. Click "Disassociate" to complete the operation.

   * After the authorization, the "Authorize shutdown repair" button in the "Actions" column of the target event is disabled.

   * After the shutdown repair is complete, BytePlus will send you an InstanceFileSystemFailure.StopAndRepair:Succeeded event. After receiving the notification, you can [log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1) to check whether the instance runs normally.
