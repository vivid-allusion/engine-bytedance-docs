---
title: "Managing a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Managing-listeners"
---

You can manage listeners on the BytePlus ALB console. In addition to [adding listeners](https://docs.byteplus.com/docs/clb/Creating-HTTP-listener), you can perform management operations such as deleting, searching, viewing, modifying, stopping, and starting listeners.

<span id=".5Yig6Zmk55uR5ZCs5Zmo"></span>
## Delete listener

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* There are no **non\-default forwarding rules** under the listener. For detailed operations, see [Forwarding rule](https://docs.byteplus.com/docs/clb/Forwarding-rule-Overview).

* The status of listener is **Stopped**. For instructions on how to disable a listener, see [Disabling a listener](https://docs.byteplus.com/docs/clb/Managing-listeners#.5YGc5q2i55uR5ZCs5Zmo).


<span id="EC3106Bl"></span>
### Action description

After deleting a listener, the following impacts will occur. Please proceed with caution.


* The forwarding rules configured for this listener will also be deleted and cannot be recovered.

* The deleted listener itself cannot be restored.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. Click **Listener** to the right of the target ALB instance.

4. On the **Listener information** tab, click ··· \> **Delete**.

5. Click **Delete** to complete the action.


<span id=".5YGc5q2i55uR5ZCs5Zmo"></span>
## Start/Stop listener

You can stop a running listener or start a stopped listener by following the operations below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After a listener is stopped, it no longer accepts user requests but can be started again.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. Click **Listener** to the right of the target ALB instance.

4. On the **Listener information** tab, click **Start** or **Stop** to the right of the target listener to complete the operation.


<span id=".5p-l5om-55uR5ZCs5Zmo"></span>
## Find listener

The ALB console provides a quick search function for listeners. On the **Instance** page, under the **Listener information** tab, you can search for a specific listener by its name or ID.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. Click **Listener** to the right of the target ALB instance.

4. On the **Listener information** tab, select a query dimension, enter a keyword, then click **Search**.


<span id=".5p-l55yL55uR5ZCs5Zmo"></span>
## View listener

You can view the detailed configuration information of a specific listener on the ALB console.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. Click **Listener** to the right of the target ALB instance.

4. View information about a listener on the **Listener information** tab. This includes basic information such as the listener name, status, protocol and port used, health check status, whether HTTP/2 is enabled, whether QUIC is enabled, and the associated server group.

5. In the **Name/ID** column, click the listener name to view the detailed configuration information of the listener. Listener status descriptions:

   
   |Listener status |Status trigger |Limitations |
   |---|---|---|
   |Creating |Indicates the listener is being created, which is a transient status. |Modification or deletion of this listener is not allowed. |
   |Running |Indicates the listener is operating normally. |Cannot be restarted. |
   |Modifying |Indicates the listener's configuration is being updated. This is a transient status. For example, this status appears when you modify the listener or change forwarding rules. |Modification or deletion of this listener is not allowed. |
   |Stopped |Indicates the listener has stopped. Listeners in this state do not accept user requests. |Not allowed to perform the stop operation again. |
   |Deleting |Indicates the listener is being deleted, which is a transient status. |Not allowed to perform the delete operation again. |
   


<span id=".5L-u5pS555uR5ZCs5Zmo"></span>
## Modify listener

You can manage added listeners on the ALB console. Depending on the listener protocol, the configurable content is as follows:


|Listener |Modifiable content |
|---|---|
|HTTP Listener |* Modify listener name and listener tag<br><br>* Modify the default server group associated with the listener<br><br>* Enable or disable access control<br><br>* Modify custom configuration |
|HTTPS listener |* Modify listener name and listener tag<br><br>* Modify server certificate<br><br>* Enable or disable advanced protocol<br><br>   * HTTP/2<br><br>   * QUIC<br><br>* Enable or disable mutual authentication<br><br>* Modify the default server group associated with the listener<br><br>* Enable or disable access control<br><br>* Modify custom configuration |


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. On the **Instance** page, locate the ALB instance with the listener to be modified.

3. In the **Actions** column, click **Listener**.

4. On the **Listener information** tab, click the name of the listener to be modified in the listener list.

5. On the **Listener details** tab, see the table below for the procedure of different modification types.

   
   |Modifiable content ||Procedures |
   |---|---|---|
   |Modify listener name and listener tag ||* Click the edit icon next to **Basic Information \> Name**, change the name, click **OK** to complete the modification.<br><br>* Click the edit icon next to **Basic Information \> Tag**, change the name, click **Save** to complete the modification. |
   |Modify the default server group associated with the listener ||Click the Edit icon next to **Default server group**, on the **Edit default backend server group** tab, select a server group from the dropdown, and click **Save** to complete the modification of the default server group associated with the listener. |
   |Edit access control ||* Enable: Click edit icon next to **Access control**, and set the **Status** switch to on. After completing the following configurations, click **Save** to enable the access control feature.<br><br>   * Denylists and Allowlists are mutually exclusive and cannot be configured simultaneously.<br><br>      * Denylist: IP addresses within the selected policy group will be denied access to the listener.<br><br>      * Allowlist: Only IP addresses within the selected policy group will be permitted access to the listener.<br><br>   * Policy group: You can set up to 5 policy groups, with each group containing a maximum of 300 IP address entries. Each IP address entry can be a single IP address or a CIDR block. For more information about policy groups, see [Access Control](https://docs.byteplus.com/docs/clb/Access-control).<br><br>* Modify: Click edit icon next to **Access control**, configure the Denylist/Allowlist and policy groups, then click **Save** to complete the modification.<br><br>* Disable: Click edit icon next to **Access control**, and set the **Status** switch to off. And complete the action to disable the access control feature. |
   |Edit custom configuration ||* Enable: Click the edit icon next to **Custom configuration** and set the **Status** switch to on. Select a custom configuration policy from the dropdown, then click **Save** to complete enabling customization.<br><br>* Modify: Click the edit icon next to **Custom configuration**, select a custom configuration policy from the dropdown, then click **Save** to complete modifying customization.<br><br>* Disable: Click edit icon next to **Custom configuration**, and set the **Status** switch to off. And complete the action to disable the custom configuration feature. |
   |Modify server certificate ||Click the edit icon next to **Basic Information \> Server certificate**, select **Certificate source**, choose a server certificate from the dropdown, and click **Save** to complete the modification. |
   |Enable or disable advanced protocol |HTTP/2 |Enable: Turn on the **Advanced protocol \> HTTP/2** switch to enable HTTP/2 protocol.<br><br>Disable: Turn off the **Advanced protocol \> HTTP/2** switch to disable HTTP/2 protocol.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the listener is already associated with a backend server group that has gRPC enabled, you cannot disable the HTTP/2 protocol.</div><br> |
   ||QUIC |Enable: Turn on the **Advanced protocol \> QUIC** switch to enable the QUIC protocol.<br><br>Disable: Turn off the **Advanced protocol \> QUIC** switch to disable the QUIC protocol. |
   |Edit Mutual Authentication ||* Enable: Click the Edit icon next to **Mutual authentication**, set the **Status** switch to On, select a CA certificate from the dropdown, and click **Save** to complete enabling the mutual authentication function.<br><br>* Modify: Click the Edit icon next to **Mutual authentication**, select a CA certificate from the dropdown, and click **Save** to complete replacing the CA certificate for mutual authentication.<br><br>* Disable: Click edit icon next to **Mutual authentication**, and set the **Status** switch to off. And complete the action to disable the mutual authentication feature. |
   


&nbsp;
