---
title: "Viewing and changing the maintenance time"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/View_and_modify_maintenance_time"
---

You can view and change the maintenance time for SystemMaintenance.Redeploy (instance redeployment due to system maintenance) events. This can reduce the maintenance impact on your current business.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="0">warning</div>


<div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">There is a risk of data loss during instance redeployment. Please back up data in advance to prevent data loss. You can back up data using <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-volume?lang=zh">volumes</a>, <a href="https://docs.byteplus.com/en/docs/tos/docs-what-is-tos?lang=zh">TOS</a>, or other methods.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|Limits |Description |
|---|---|
|Event |Currently, you can change the scheduled maintenance time only for SystemMaintenance.Redeploy (instance redeployment due to system maintenance) events. Additionally, you have specified the maintenance time for these events.   |
|Time range |You can change the maintenance time only if the next half\-hour point from the current time is earlier than the scheduled start time.<br><br><br>* Next half\-hour point from the current time: The nearest 30\-minute time point that comes after the current time.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Methods to calculate the next half\-hour point from the current time:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the minutes of the current time are less than 30, the next half\-hour point stays in the same hour, with minutes set to 30. For example, if the current time is 8:10, the next half\-hour point is 8:30.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the minutes of the current time are 30 or more, the next half\-hour point moves to the next hour, with minutes set to 30. For example, if the current time is 9:45, the next half\-hour point is 10:30.   </div><br>   <br><br>* Scheduled start time: The start time you originally reserved when you authorized BytePlus to redeploy the instance. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events" or "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the resource that has triggered the event.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Event information will be displayed by the project to which the triggering resource (such as an ECS instance) belongs. Your account needs to have the permission to manage the corresponding project. Otherwise, you can not view the event information.    </div>
   

4. Click the name of the target instance to go to the instance details page, and click the "System Events" tab. Or, click the "Scheduled operations events" tab.

5. In the "Actions" column of the target event, click the "Modify maintenance time" button to view or change the maintenance time.

   * **View the maintenance time**: The current maintenance time for the target event is displayed, including the start time, end time, and other information.

   * **Change the maintenance time**: You need to select the maintenance time for instance redeployment by selecting "Execute now" or rescheduling the time under "Schedule" button. After this, agree to the maintenance authorization.

      * Execute now: The instance will be redeployed immediately.

      * Schedule: The instance will be redeployed at a scheduled time.

6. Click the "Confirm" button to complete the operation.

   * After authorization is complete, the "Authorize redeployment" button in the "Actions" column of the target event is disabled.

   * After authorization is complete,Bytepluswill redeploy the instance based on the maintenance time you set. After the deployment is complete, the event state is **Succeeded**.
