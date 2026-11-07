---
title: "Deleting a QoS policy"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Deleting_a_QoS_policy"
---

You can delete QoS policies that are no longer in use.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The QoS policy pending deletion is not associated with any Direct Connect (DC) Connection, and contains no traffic queues other than the default queue (named **Default**). If it is still associated with any DC Connection or has extra traffic queues, unbind all associated connections and delete those queues first. Then delete the QoS policy. For procedure, see [Delete a DC Connection](https://docs.byteplus.com/en/docs/directconnect/Managing-Direct-Connect-connections#.5Yig6Zmk54mp55CG5LiT57q_) and [Delete existing traffic queue](https://docs.byteplus.com/en/docs/directconnect/Managing_QoS_policy#.566h55CG5rWB6Zif5YiX).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection). In the left navigation pane, select **QoS Policy**.

2. In the top menu bar, select the target region.

3. In the QoS policy list, click **Delete** in the **Actions** column of the target QoS policy.

4. In the pop\-up dialog box, click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[DeleteDirectConnectTrafficQosPolicy](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosPolicy): Deletes a specified QoS policy.
