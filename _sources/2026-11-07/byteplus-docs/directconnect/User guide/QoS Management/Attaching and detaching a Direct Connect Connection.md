---
title: "Attaching and detaching a Direct Connect Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Attaching_and_detaching_DC_Connection"
---

After a QoS policy is created, it must be associated with a Direct Connect (DC) Connection. Only then will the outbound traffic of the associated DC Connection be scheduled according to that QoS policy. When the QoS policy is no longer needed, it can be disassociated from the DC Connection.

<span id=".UW9T562W55Wl5YWz6IGU54mp55CG5LiT57q_"></span>
## Attach a QoS policy a DC Connection

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* An available dedicated DC Connection is required. For specific operations, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1).

* The QoS policy has been created, and the Region of the QoS policy matches that of the DC Connection to be attached. For detailed actions, see [Creating QoS policy](https://docs.byteplus.com/en/docs/directconnect/Creating_a_QoS_Policy).

* A single DC Connection can be associated with only one QoS policy. A single QoS policy can be associated with multiple DC Connections.

* QoS policies cannot be associated with shared DC Connections or dedicated DC Connections in an abnormal state.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In all the subsequent descriptions related to the QoS policy, unless otherwise emphasized, DC Connection refers to a dedicated DC Connection.   </div>
   

* A QoS policy will not take effect if any of the following conditions exist:

   * The line bandwidth of the dedicated DC Connection is less than its port specification.

   * A DC virtual interface created using this dedicated DC Connection has bandwidth limit enabled.

* If multiple DC virtual interfaces are created using the same DC Gateway and multiple dedicated DC Connections, it is recommended to associate a QoS policy with all dedicated DC Connections, and ideally, associate them with the same QoS policy. If only some DC Connections are associated with the same QoS policy, traffic on the DC Connections without an associated QoS policy will be scheduled according to the default QoS policy. If congestion occurs on those DC Connections, the unpredictable bandwidth limit may result.


<span id=".5pON5L2c6K-05piO"></span>
### Instructions

When attaching a QoS policy to a DC Connection, the platform will recommend you simultaneously attach other DC Connections that use the same DC Gateway to create virtual interfaces. The specific logic is illustrated in the figure below, and you can attach these relevant DC Connections based on your actual needs

Taking the figure below as an example, different operations result in different outcomes


* **DC Connection\-01** and **DC Connection\-02** are both associated with the same QoS policy. All service traffic passing through **DC Gateway\-01** enters **DC Connection\-01** and **DC Connection\-02** respectively and is scheduled according to the associated QoS policy.

* Only **DC Connection\-01** is associated with a QoS policy; **DC Connection\-02** is not:

   * The QoS policy attached to **DC Connection\-01** does not configure DSCP remarking. All service traffic passing through **DC Gateway\-01** enters **DC Connection\-01** and **DC Connection\-02** respectively. Traffic entering **DC Connection\-01** is scheduled according to its associated QoS policy. Traffic entering **DC Connection\-02** is scheduled according to the system's default QoS policy.

   * The QoS policy attached to **DC Connection\-01** does configure DSCP remarking. All service traffic passing through **DC Gateway\-01** enters **DC Connection\-01** and **DC Connection\-02** respectively. Traffic entering **DC Connection\-01** is scheduled according to its associated QoS policy (including DSCP remarking). Traffic entering **DC Connection\-02** is scheduled according to the system's default QoS policy, but the DSCP value of this traffic will be rewritten based on the QoS policy associated with **DC Connection\-01**.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection). In the left navigation pane, select **QoS Policy**.

2. In the top menu bar, select the region where the target QoS Policy is located.

3. In the QoS policy list, click **Attach DC Connection** in the **Actions** column of the target QoS policy.

4. Select the target DC Connection. Multiple DC Connections can be selected simultaneously.

5. After completion, click **Attach**.


<span id=".UW9T562W55Wl6Kej57uR6Kej57uR54mp55CG5LiT57q_"></span>
## Detach a QoS policy from a DC Connection

<span id=".5pON5L2c6K-05piO"></span>
### Instructions

Operation instruction\nAfter the DC Connection is disassociated from the QoS policy, the business traffic in the outbound direction through the DC Connection will no longer be scheduled according to the QoS policy.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection). In the left navigation pane, select **QoS Policy**.

2. In the top navigation bar, select the target region.

3. In the QoS policy list, click **Disassociate DC Connection** in the **Actions** column of the target QoS policy.

4. In the pop\-up dialog box, click **Enable** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[ModifyDirectConnectTrafficQosPolicyAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectTrafficQosPolicyAttributes): Modify the information of a specified QoS policy, including attaching or detaching a QoS policy to/from a DC Connection.
