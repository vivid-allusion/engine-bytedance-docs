---
title: "Managing a QoS policy"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Managing_QoS_policy"
---

This topic introduces common actions related to QoS policies. After a QoS policy is created, you can perform the following actions based on your actual business needs: add or remove traffic queues for the QoS policy; add or delete traffic rules for a traffic queue; disassociate a QoS policy from a Direct Connect Connection; or delete a QoS policy.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* The number of traffic queues that can be added to each QoS policy and the number of traffic rules that can be added to each traffic queue are both subject to quota limits. If the quota is exceeded, you will be unable to add new traffic queues or traffic rules.

   * For specific quota quantities, see [Limits](https://docs.byteplus.com/en/docs/directconnect/Limits).

   * To increase the quota, [create a quota change application](https://docs.byteplus.com/en/docs/directconnect/Quota_management).

* Adding or removing traffic queues or traffic rules may affect traffic marking. Please ensure that the bandwidth of the traffic queue is not less than the actual business requirements.

* To delete a traffic queue, you must first delete all manually added traffic rules within that queue.

* Default traffic queues cannot be deleted. In general, the queue named **Default** and described as **Default Queue** in the traffic queue list is the default traffic queue.


<span id=".566h55CG5rWB6Zif5YiX"></span>
## Manage a traffic queue


1. Log in to the [Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection). In the left navigation pane, select **QoS Policy**.

2. In the top menu bar, select the target region.

3. In the QoS policy list, click the name of the target QoS policy.

4. Select the **Traffic Queue** tab and choose the desired actions based on your needs.

   
   <Tabs>
   <Tab zoneid="w3dpVj5sHX" title="Add new traffic queue">
   <TabTitle>Add new traffic queue</TabTitle>
   
   1. Click **Add traffic queue**.
   
   2. To complete parameter configuration, see [Creating a QoS policy](https://docs.byteplus.com/en/docs/directconnect/Creating_a_QoS_Policy).
   
   3. Click **Add** to complete the action.
   
   
   </Tab>
   <Tab zoneid="cZN8gncu9Y" title="Delete existing traffic queue">
   <TabTitle>Delete existing traffic queue</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">The flow queue pending deletion has no traffic rules. If it has any, delete them first. For details, see <a href="https://docs.byteplus.com/en/docs/directconnect/Managing_QoS_policy#.566h55CG5rWB5YiG57G76KeE5YiZ">Manage a traffic rule</a>.</div>
   
   
   
   1. In the Traffic queue list, click **Delete** in the **Actions** column of the target flow queue.
   
   2. In the pop\-up dialog box, click **Delete** to complete the action.
   
   
   </Tab>
   </Tabs>
   


<span id=".566h55CG5rWB5YiG57G76KeE5YiZ"></span>
## Manage a traffic rule


1. Log in to the [Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection). In the left navigation pane, select **QoS Policy**.

2. In the top menu bar, select the target region.

3. In the QoS policy list, click the name of the target QoS policy.

4. Select the **Traffic Queue** tab, and click the name of the target traffic queue.

5. Select the corresponding action based on your needs.

   
   <Tabs>
   <Tab zoneid="fnO69amx0t" title="Add new traffic rule">
   <TabTitle>Add new traffic rule</TabTitle>
   
   1. Click **Add traffic rules**.
   
   2. To complete parameter configuration, see [Creating a QoS policy](https://docs.byteplus.com/en/docs/directconnect/Creating_a_QoS_Policy).
   
   3. Click **Add** to complete the action.
   
   
   </Tab>
   <Tab zoneid="slCIPQEenp" title="Remove existing traffic rule">
   <TabTitle>Remove existing traffic rule</TabTitle>
   
   1. In the traffic rule list, click **Delete** in the **Actions** column of the target traffic rule.
   
   2. In the pop\-up dialog box, click **OK** to complete the action.
   
   
   </Tab>
   </Tabs>
   


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [CreateDirectConnectTrafficQosQueue](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosQueue): Add a traffic queue to a QoS policy.

* [DeleteDirectConnectTrafficQosPolicy](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosPolicy): Delete a specified traffic queue.

* [CreateDirectConnectTrafficQosRule](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosRule): Add a traffic rule to a traffic queue.

* [DeleteDirectConnectTrafficQosQueue](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosQueue): Delete a specified traffic rule.
