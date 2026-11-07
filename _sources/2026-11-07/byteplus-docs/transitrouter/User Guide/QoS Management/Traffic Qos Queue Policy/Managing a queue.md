---
title: "Managing a queue"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Managing-queues-of-a-qos-queue-policy"
---

## Scenarios

After a traffic queue policy is created, you can add or delete queues as needed and modify the configuration of existing queues.

> **tip**

> If the modified bandwidth is insufficient for actual business requirements, normal service forwarding may be impacted.​

## Instructions

* A traffic queue policy consists of 1 default queue and additionally supports up to 64 custom queues.​

* The default queue does not support modifying its bandwidth allocation or being deleted.

## Add a queue

1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Traffic queue policy** tab.

4. Click the name of the target traffic queue policy.

5. Click **Add traffic queue**, and configure the parameters based on [Creating a traffic queue policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-qos-queue-policy#.5pON5L2c5q2l6aqk).

6. Click **Create** to complete the action.

## Modify a queue

1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Traffic queue policy** tab.

4. Click the name of the target traffic queue policy.

5. Click **Edit** to the right of the target traffic queue policy, and modify the queue configuration based on [Creating a traffic marking policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-qos-queue-policy#.5pON5L2c5q2l6aqk).

   > The queue priority cannot be modified.

6. Click **OK** to complete the action.

## Delete queue

1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Traffic queue policy** tab.

4. Click the name of the target traffic queue policy.

5. Click **Delete** to the right of the target queue.

6. Click **Delete** to complete the action.

## Related documentation

* [CreateTransitRouterTrafficQosQueueEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosQueueEntry): Add a queue to a traffic queue policy.

* [DeleteTransitRouterTrafficQosQueueEntry](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosQueueEntry): Delete a queue from a traffic queue policy.
