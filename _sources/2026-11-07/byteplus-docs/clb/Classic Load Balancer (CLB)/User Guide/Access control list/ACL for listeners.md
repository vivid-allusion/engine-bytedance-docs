---
title: "ACL for listeners"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-access-control-for-a-listener"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Operation scenario

To allow or deny requests of some IP addresses to access a CLB instance through the listening port, configure an Access Control List (ACL) for this listener.

You can **Configure ACLs when creating a listener** or **Configure ACLs while a listener is running**.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions

If the listener of a CLB instance is an IPv4 listener, the added IPv6 entries do not take effect after the ACL is associated with the listener.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="X6mCxYXxLH" title="Configuring an ACL when creating a listener">
<TabTitle>Configuring an ACL when creating a listener</TabTitle>

When [Creating a listener](https://docs.byteplus.com/en/docs/clb/Creating-a-TCP-listener), The first step requires configuring **Protocol & Listener** settings, Enabling access control, and selecting both the control method and policy group.


|**Name** |**Explaination** |**Sample Value** |
|---|---|---|
|Control mode |After enabling the ACL feature, select an access control mode:<br><br><br>* Blocklist: Denies access from the IPs in the selected policy group to the CLB instance.<br><br>* Allowlist: Only allows access from the IPs in the selected policy group to the CLB instance. Please set with caution.<br><br><br>After the access control mode is changed, the associated ACL will be cleared. |blocklist |
|Affiliated project |Select the project to which the ACL belongs. By default, all projects are selected. |All |
|ACL name |Select one or more ACLs. IPs in the ACLs will be added to the deny list or allow list. You can select up to five ACLs. If no policy group exists yet, click **Create access control policy group** in the selection box and refer to [Creating a policy group](https://docs.byteplus.com/en/docs/clb/Managing-access-control-policy-groups). |\- |



</Tab>
<Tab zoneid="xia40U686I" title="Configuring access control while the listener is running">
<TabTitle>Configuring access control while the listener is running</TabTitle>

1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target region and target project.

3. Click **Configure Listener** on the right side of the target CLB instance.

4. Click  **...**  on the right side of the target listener list. Click  **\> Edit access control**.

5. Refer to [Creating listener](https://docs.byteplus.com/en/docs/clb/Creating-a-Listener) For parameter descriptions to reconfigure IAM.

6. Click **OK** to complete the action.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[ModifyListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyListenerAttributes)
