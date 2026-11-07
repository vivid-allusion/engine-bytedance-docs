---
title: "Events"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/event-center"
---

Cache for Redis provides events function, supporting software, hardware, or network upgrades on the physical machines that run instances. These operations are performed as planned events to ensure the stability and sustainability of database cloud services. This topic contains information related to planned events, including event types and definitions, supported operations and their impacts, event notification time, and time limits for execution postponement.

<span id=".5LqL5Lu257G75Z6L5Y-K5pON5L2c5b2x5ZON"></span>
## Event types and operation impact

Cache for Redis currently supports two types of planned events: **system maintenance** and **user action**. The event operations supported by these two types of events are different, and so are the outcomes of the operations and postponement time limits.


|Event type |System maintenance |User action |
|---|---|---|
|Event definition |To continuously improve product performance and stability, the system performs software and hardware or network upgrades on the instance's machine. |If you choose to execute certain tasks within the maintenance period, these pending tasks will automatically become planned events and be added to the planned event list. |
|Supported event operations |* Upgrade kernel version<br><br>* Maintenance (such as machine software/hardware and network upgrades) |* [Restart instance](https://docs.byteplus.com/en/docs/redis/restart-instance)<br><br>* Modifying instance specifications (including [Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec), [Modifying number of node](https://docs.byteplus.com/en/docs/redis/modify-node-number), [Modifying number of shard](https://docs.byteplus.com/en/docs/redis/modify-shard--number), [Enabling sharding cluster](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config), [Switching to primary-secondary instance](https://docs.byteplus.com/en/docs/redis/switch_to_high_availability_instance))<br><br>* [Modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az)<br><br>* [Upgrading minor version](https://docs.byteplus.com/en/docs/redis/upgrade-minor-version) |
|Operation impact |* The status of a planned event changes to **In progress** once execution starts. Instance node switchover may occur during the maintenance event execution process, which may result in second\-long non\-writability or temporary disconnections. Please ensure that your services operate with an automatic reconnection mechanism.<br><br>* Performing system maintenance\-related operations (such as upgrading kernel versions, machine software and hardware, networks, etc.) will cause data flashback to be **automatically disabled**. After the data flashback feature is disabled, previous flashback points will no longer be retained. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback). |* The status of a planned event changes to **In progress** once execution starts. Instance node switchover may occur during the execution process, which may result in second\-long non\-writability or temporary disconnections. Ensure that your services operate with an automatic reconnection mechanism. For more information on the outcomes of the operations, refer to the relevant documentation.<br><br>* Performing [modifying instance specifications](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification) or [modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az) operation will cause data flashback to be **automatically disabled**. After the data flashback feature is disabled, previous flashback points will no longer be retained. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback). |
|Event notification time |The system notifies you of pending planned events at least 3 days in advance via voice, email, internal message, or console events. |You will not receive notification messages for event operations initiated by yourself via the console. You can directly check in the [Events](https://console.byteplus.com/db/region:db+ap-southeast-1/redis/eventCenter) of the Redis console. |
|Change execution time |* Only events that meet all the following requirements support changing execution time:<br><br>   * The event type is **System maintenance**.<br><br>   * The event status is **Waiting for execution**.<br><br>   * The event's **The latest deferred time** indicates a specific time point, rather than **Cannot be postponed**.<br><br>   * The time until the event's scheduled execution must be greater than 1 day.<br><br>* There is no limit on the number of times to modify the execution time. However, the modified execution time must be later than the end time of the original planned execution time, and earlier than the latest deferred time execution allowed. For specific procedures, refer to [Modifying execution time](https://docs.byteplus.com/en/docs/redis/postpone-execution-time). |The execution time cannot be modified. The system will execute the corresponding event within the maintainable time period you have selected. |
|Execute event Now |Supports advancing the execution time of a planned event waiting to be executed to the current time for immediate execution. For specific procedures, refer to [Executing planned event](https://docs.byteplus.com/en/docs/redis/execute-planned-event). ||
|Cancel event execution |Cannot be cancelled manually.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If special circumstances prevent maintenance events from being completed within the execution time, the system automatically cancels the current maintenance event and notifies you via email or in\-site messages. Please pay attention to relevant notifications. You can configure message reception settings in <strong>Message center</strong> page of the BytePlus console. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/message_center/Message-Subscription-and-Notification-Methods">Message subscription and notification methods</a>.</div><br> |* Only events that meet all the following requirements can be canceled:<br><br>   * The event type is **User action**.<br><br>   * The event status is **Waiting for execution**.<br><br>   * The time until the event's scheduled execution must be greater than 30 minutes.<br><br>* After cancelling the planned event, the status of the instance will be restored to **Running**. For specific procedure, refer to [Canceling planned event](https://docs.byteplus.com/en/docs/redis/cancel-planned-event). |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The status of a scheduled maintenance event changes to **In progress** once execution starts. Instance node switchover may occur during the maintenance event execution process, which may result in second\-long non\-writability or temporary disconnections. Please ensure that your services operate with an automatic reconnection mechanism. For more information on supported event operations and their impact on your services, refer to [Event types and operation impact](https://docs.byteplus.com/en/docs/redis/event-center).

* Before the scheduled maintenance event is executed, its status is shown as **Waiting for execution**. Normal data access to the database will not be affected.

* After the scheduled maintenance event is completed, the instance's address and access method remain the same as the source instance. The instance's network configuration will not change, and migration tasks will not be affected by maintenance events.

* Redis does not limit the number of operations to change the execution time, but the planned execution time after each change must be later than the end time of the previous planned execution time and earlier than the latest deferred time. For specific procedures, refer to [Modifying execution time](https://docs.byteplus.com/en/docs/redis/postpone-execution-time).

* For **system** maintenance events, if special circumstances prevent maintenance events from being completed within the execution time, the system automatically cancels the current maintenance event and notifies you via email or in\-site messages. Please pay attention to relevant notifications. You can configure message reception settings in **Message center** page of the BytePlus console. For specific procedures, refer to [Message subscription and notification methods](https://docs.byteplus.com/en/docs/message_center/Message-Subscription-and-Notification-Methods).


<span id=".55u45YWz5pON5L2c"></span>
## Related operations


* [Viewing planned event](https://docs.byteplus.com/en/docs/redis/manage-planned-event)

* [Modifying execution time](https://docs.byteplus.com/en/docs/redis/postpone-execution-time)

* [Executing planned event](https://docs.byteplus.com/en/docs/redis/execute-planned-event)

* [Canceling planned event](https://docs.byteplus.com/en/docs/redis/cancel-planned-event)
