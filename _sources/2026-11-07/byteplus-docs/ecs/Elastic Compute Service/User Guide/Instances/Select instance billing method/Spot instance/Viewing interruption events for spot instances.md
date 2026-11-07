---
title: "Viewing interruption events for spot instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/View_spot_instance_interruption_event"
---

When resource inventory is insufficient or the spot market price exceeds your bid price, the platform may reclaim your spot instance. Before being reclaimed, the instance triggers an instance interruption event. This topic describes how to view interruption events for spot instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This topic is only about spot instance interruption events. If you want to learn more about event types, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Event-type-overview">Event type overview</a>.</div>


* <div data-tips="true" data-tips-type="tip">You can <a href="https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications#.6K6i6ZiF5LqL5Lu26YCa55-l">subscribe to event notifications</a>. This allows you to receive instance release notifications via internal message, SMS, email, and other channels before the spot instance is interrupted (1 hour in advance for GPU instances and 5 minutes in advance for non\-GPU instances).</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="U11u3g3XZh" title="View on the console">
<TabTitle>View on the console</TabTitle>

**Method 1: ECS console**


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events".

3. On the "System Events" page, select the time period you want to query and view in the search bar as follows.

   * Method 1: Event type

      Specify the event type as "Spot instance was interrupted and instance was released". If an event with the "Scheduled" status exists, it indicates that the spot instance is to be interrupted. Therefore, back up your data in advance.

   * Method 2: ECS instance ID

      Enter the spot instance ID and press Enter to confirm. You can view the spot instance ID in the Instance name/ID column of the list or on the instance details page.


**Method 2: Cloud Monitor console**


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left\-side navigation pane, select "Event Center \> Cloud Service Event".

3. On the Cloud Service Event page, select the time range to query. In the left search bar, select "ecs" from the drop\-down list. In the right search bar, select the event type "Spot instance interruption, instance release: Scheduled". You can also perform a fuzzy search.

4. To view details of the target event, click the "Details" button in the "Actions" column of the event. Then, you can view event details in JSON format.


</Tab>
<Tab zoneid="i0xEE6QbeV" title="View through instance metadata">
<TabTitle>View through instance metadata</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to query instance metadata.

   * Linux instance: `curl http://100.96.0.96/latest/spot_instance_termination_time`

   * Windows example: `Invoke-RestMethod http://100.96.0.96/latest/spot_instance_termination_time`

   If the response includes a time in UTC format, such as `2023-02-23T17:35:00Z`, it indicates that the spot instance is reclaimed at that time.


For more information about instance metadata, refer to [Viewing instance metadata](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata).


</Tab>
<Tab zoneid="MlsUYbWwuB" title="View through OpenAPI">
<TabTitle>View through OpenAPI</TabTitle>

**Method 1: ECS OpenAPI**

Call [DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents) operation and set ResourceIds.N to the spot instance ID, or set Types.N to SpotInstanceInterruption_Delete, to query spot instance interruption events.

If there is a `Scheduled` (Scheduled) event, it indicates that the spot instance is about to be interrupted. Please prepare for data backup.

**Method 2: Cloud Monitor OpenAPI**

Call Cloud Monitor ListEvents operation, and specify the following parameters to query spot instance interruption events.


* Set `Source` to `ecs`.

* Set `EventType` to `ecs:Instance:SpotInstanceInterruption.Delete.Scheduled`(Scheduled).


> For more event types related to ECS instances, refer to [ECS instance events](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=event&namespace=ecs%2C%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8).


If the corresponding event type is returned, it indicates that the spot instance will be interrupted soon.


</Tab>
</Tabs>


&nbsp;
