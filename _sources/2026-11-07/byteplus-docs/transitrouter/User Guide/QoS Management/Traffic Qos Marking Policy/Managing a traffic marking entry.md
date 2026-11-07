---
title: "Managing a traffic marking entry"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Managing-entries-of-qos-marking-policy"
---

## Scenarios

After creating the traffic marking policy, you can add or delete marking entries as needed.

## Instructions

* A traffic marking policy supports a maximum of 100 entries by default.​ If the quota is insufficient, [create a quota modification application](https://docs.byteplus.com/en/docs/6837/129542) to request a quota increase.

* Adding or deleting marking entries affects data transfer marking. If the bandwidth of the dispatch queue matched by the data transfer marking is less than the actual business needs, it will affect normal forwarding.

## Add a traffic marking entry

1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. Select the **Traffic marking policy** tab under **Basic information**.

4. Click the target traffic marking policy name.

5. Click **Add traffic marking entry**, and configure parameters as per [Creating a traffic marking policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-qos-marking-policy#.5pON5L2c5q2l6aqk).

6. Click **Create** to complete the action.

## Modify a traffic marking entry

1. Log in to the [Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Traffic marking policy** tab.

4. Click the name of the target traffic marking policy.

5. Click **Edit** to the right of the target traffic marking policy, and modify the entry configuration based on [Creating a traffic marking policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-qos-marking-policy).

   > The entry priority cannot be modified.

6. Click **OK** to complete the action.

## Delete a traffic marking entry

1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. Select the **Traffic marking policy** tab under **Basic information**.

4. Click the name of the target traffic marking policy.

5. Click **Delete** to the right of the target marking entry.

6. Click **Delete** to complete the action.

## Related documentation

* [CreateTransitRouterTrafficQosMarkingEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosMarkingEntry): Add a marking entry to a traffic marking policy.

* [DeleteTransitRouterTrafficQosMarkingEntry](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosMarkingEntry): Delete a marking entry from a traffic marking policy.
