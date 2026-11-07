---
title: "Querying and handling events"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events"
---

You can query and handle events through the ECS console or OpenAPI, or query event information on the Cloud Monitor console. You can also use event subscription and alert notification capabilities to receive event notifications in a timely manner. For details, see [Subscribing to message center notifications](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications#2iPm0nJi) and[ Configuring Cloud Monitor notifications](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications#.5LqR55uR5o6n6YCa55-l).

When a [scheduled O&M event](https://docs.byteplus.com/en/docs/ecs/Event-type-overview#.6K6h5YiS5YaF6L-Q57u05LqL5Lu2) is generated and BytePlus has not obtained the permission for conducting O&M operations, the event will be automatically canceled when there are changes to the host (such as manual hot or cold migration, evacuation, type changes, power\-on, and restart). This is an automatic O&M process.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The automatic cancellation (automatic O&M) is triggered only for instances of General\-purpose, Compute\-optimized, Memory\-optimized, and High Frequency families. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">the instance type list</a>.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">During the O&M period, operations such as <strong>configuration modification</strong>, <strong>shutdown</strong>, and <strong>restart </strong>are performed on your instance, which may impact your business. Please select an appropriate O&M time.</div>



<span id="357f1vk5"></span>
## Query and handle events in the ECS console

You can query and handle all events in the ECS console. To avoid impacting your business operations, please promptly view and address the issue upon receiving the event notification.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Redeploying instances will affect data stored on local volumes. Please back up data in advance to prevent data loss. You can back up data using <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-volume?lang=zh">volumes</a>, <a href="https://docs.byteplus.com/en/docs/tos/docs-what-is-tos?lang=zh">TOS</a>, or other methods.</div>


<span id="AfsKY1xG"></span>
### Event level


|Event level |Description |
|---|---|
|Severe |The impact is significant. Handle the issue promptly, or it may cause the instance to be unusable. For example, "instance redeployment due to system errors" and "instance exception due to operating system errors" events. |
|Warning |There is a certain impact. We recommend that you monitor the issue during the impact period or choose an appropriate time to address it. For example, the "spot instance interruption, instance release" event **.**  |
|Information |You can select whether to follow events like instance status change events. |


<span id="PZcCz1ZH"></span>
### Usage notes


|Event |Description |
|---|---|
|SystemMaintenance.Redeploy (Instance redeployment due to system maintenance) |Authorized O&M and automatic O&M are available for your choice.<br><br><br>* **Authorize O&M**: Select an O&M time or time range based on your business needs. After the authorization, the O&M personnel will redeploy the instance. Manual and automatic authorization are supported.<br><br>   * **Manual authorization**<br><br>      After an event occurs, you need to manually select an O&M time or time period for the target event and authorize BytePlus. BytePlus then redeploys your instance based on the maintenance time you set.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The O&M time includes "Execute now" and "Schedule", with the default setting being "Execute now".       </div><br>      <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Execute now: The instance will be redeployed immediately.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Schedule: The instance will be redeployed at a scheduled time. You can select an appropriate O&M period on the authorization page.      </div><br>      <br><br>   * **Automatic authorization**<br><br>      You can enable automatic authorization by [creating a scheduled maintenance window](https://docs.byteplus.com/en/docs/ecs/Creating_scheduled_maintenance_windows). After an event occurs within the specified time period, BytePlus will default to redeploying your instance based on the maintenance time you set.<br><br>* **Automatic O&M**: Actions like instance resizing, starting, or restarting trigger automatic O&M.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have not made O&M authorization, or have made O&M authorization with a scheduled execution time that has not yet arrived, the action of resizing, starting, or restarting the instance will trigger automatic O&M.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, the automatic O&M capability is available only for instances of <a href="https://docs.byteplus.com/en/docs/ecs/General-purpose">General\-purpose</a>, <a href="https://docs.byteplus.com/en/docs/ecs/Computing-optimized">Compute\-optimized</a>, <a href="https://docs.byteplus.com/en/docs/ecs/Memory-optimized">Memory\-optimized</a> families.   </div><br>    |
|InfrastructureUpgrade.Redeploy (Instance redeployment due to infrastructure upgrade) ||
|Other events<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Events other than SystemMaintenance.Redeploy (Instance redeployment due to system maintenance) and</div><br><br><br><div data-tips="true" data-tips-type="tip">InfrastructureUpgrade.Redeploy (Instance redeployment due to infrastructure upgrade). For details, see the <a href="https://docs.byteplus.com/en/docs/ecs/Event-type-overview">Event type overview</a>.</div><br> |For other events, your authorization is required before the O&M procedure is performed. You need to select an O&M time based on your business needs. After the authorization, the O&M personnel will redeploy the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The O&M time includes "Execute now" and "Schedule", with the default setting being "Execute now".</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Execute now: The instance will be redeployed immediately.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Schedule: The instance will be redeployed at a scheduled time. You can select an appropriate O&M period on the authorization page.</div><br> |


<span id="HfIP6hXR"></span>
### On the instance details page


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the resource that has triggered the event.

4. Find the target instance, and click the instance name to go to the instance details page.

5. Click the "System Events" tab, here you can filter event information based on a time range or event ID and take actions.

   * **View details**: In the "Actions" column of the target event, click the "Details" button to view information such as the event occurrence time, type, and associated instance.

   * **Maintenance operations**: In the "Actions" column of the target event, click the "Maintenance operation" button. Then, select the required authorization action (such as replacement of a faulty hard disk), authorize and notify the platform maintenance personnel to perform the maintenance.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If there is no "O&M" button, it indicates that no action is required for this event.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After the authorization, the "Authorize" button in the Actions column will be disabled to avoid repeated authorization.      </div>
      

   * **Authorize redeployment: ** In the "Actions" column of the target event, click the "Authorize redeployment" button to authorize and notify the platform for maintenance operations.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After the authorization, the "Authorize redeployment" button in the Actions column will be disabled to avoid repeated authorization.      </div>
      

   * **Diagnose root cause of exception**: In the "Actions" column of the target event, click the "Find the root cause for instance exception" button to [perform a health diagnosis](https://docs.byteplus.com/en/docs/ecs/Diagnose_instance_health_status) on the instance based on your needs.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Root cause analysis can be made only for instance events that occurred within the past 7 days and are classified as "InstanceFailure (instance exception due to operating system errors)", "InstanceOOM (instance memory OOM)", and "InstanceDiskStalled (severe damage to instance disk performance)" events.      </div>
      

   * **Restart the instance:**  In the "Actions" column of the target event, click the "Restart instance" button. On the page that appears, select "Determine Restart Selected Instances". Then, click the "OK" button.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the "Restart instance" button is not available for your event, it indicates that the event does not require recovery through instance restart.      </div>
      

<span id="cgRTCXTN"></span>
### On the System Events page

<span id="OVI1nQx9"></span>
#### Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events".

3. In the top menu bar, select the project and region of the resource that has triggered the event.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Event information will be displayed by the project to which the triggering resource (such as an ECS instance) belongs. Your account needs to have the permission to manage the corresponding project. Otherwise, you can not view the event information.    </div>
   

4. Based on event type, you need to select a tab among the "Scheduled operations events", "Unexpected operation and maintenance events", "Fees warning event", "Status change event", or "Task status class event" tab. For details, see the [Event type overview](https://docs.byteplus.com/en/docs/ecs/Event-type-overview?LibVersion=markdown备份版本).

5. On the System Events page, you can filter event information based on a time range, event ID, or instance ID, and handle them accordingly.

   * **View details**: In the "Actions" column of the target event, click the "Details" button to view information such as the event occurrence time, type, associated instance, and event details.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can view event details only for scheduled operation events and unexpected operation events.      </div>
      

   * **Maintenance operation**: In the "Actions" column of the target event, click the "Maintenance operation" button. Then, select the required authorization action (such as replacement of a faulty hard disk), authorize and notify the BytePlus maintenance personnel to perform the maintenance.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If there is no "Maintenance operation" button, it indicates that no action is required for this event.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After the authorization, the "Authorize" button in the "Actions" column will be disabled to avoid repeated authorization.      </div>
      

   * **Authorize redeployment**: In the "Actions" column of the target event, click the "Authorize redeployment" button to authorize and notify the platform maintenance personnel for maintenance operations.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After the authorization, the "Authorize" button in the "Actions" column will be disabled to avoid repeated authorization.      </div>
      

   * **View and change maintenance time:**  In the "Actions" column of the target event, click the "Modify maintenance time" button. Authorize and notify the platform to perform maintenance operations. For specific steps, refer to [Viewing and changing maintenance time](https://docs.byteplus.com/en/docs/ecs/View_and_modify_maintenance_time).

   * **Diagnose root cause of exception**: In the "Actions" column of the target event, click the "Find the root cause for instance exception" button to [perform a health diagnosis](https://docs.byteplus.com/en/docs/ecs/Diagnose_instance_health_status) on the instance based on your needs.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Root cause analysis can be made only for instance events that occurred within the past 7 days and are classified as "InstanceFailure (instance exception due to operating system errors)", "InstanceOOM (instance memory OOM)", and "InstanceDiskStalled (severe damage to instance disk performance)" events.      </div>
      

   * **Restart the instance:**  In the "Actions" column of the target event, click the "Restart instance" button. On the page that appears, select "Determine Restart Selected Instances". Then, click the "OK" button.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the "Restart instance" button is not available for your event, it indicates that the event does not require recovery through instance restart.      </div>
      

<span id="cdXEuM6q"></span>
#### Subsequent steps


* If you need to authorize the replacement of the hard disk, please refer to [Resolving local volume failures by replacing faulty volumes](https://docs.byteplus.com/en/docs/ecs/Isolating-local-volumes).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For events occurring on HPC\-optimized instances, you can not resolve local volume failures by replacing faulty volumes.   </div>
   

* If you need to redeploy the instance, please refer to [Resolving local volume failures by authorizing instance redeployment](https://docs.byteplus.com/en/docs/ecs/Redeploying-instances).


<span id="OAE6yhP5"></span>
## Query events in the Cloud Monitor console

You can query all ECS events on the Cloud Product Events page.


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor). 

2. In the left\-side navigation pane, select "Event Center \> Cloud Service Event".

3. On the "Cloud Service Event" page, you can filter event information by time period, cloud service, and event type.

   Select the "ECS" product to view ECS\-related events.

4. To view details of an event, click the "Details" button in the "Actions" column of the event.

   > The event details will be displayed in JSON format.
