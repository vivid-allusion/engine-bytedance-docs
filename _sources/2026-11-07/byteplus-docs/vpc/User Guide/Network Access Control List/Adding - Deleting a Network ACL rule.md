---
title: "Adding/Deleting a Network ACL rule"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The network ACL's [default rules](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) allow all traffic. If this does not meet your needs, refer to this document to change the network ACL rules.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Changes to network ACL rules (adding, modifying, or deleting) take effect immediately. For cloud resources within subnets associated with this network ACL, both existing and newly established cross\-subnet connections will be controlled by the network ACL rules. Please thoroughly evaluate the potential impact on live services and proceed with extreme caution.</div>


<span id=".5re75Yqg572R57ucQUNM6KeE5YiZ"></span>
## Add network ACL rule

You can add multiple inbound/outbound rules sequentially, with each rule having a lower priority than the previous one. A maximum of 20 rules per direction is supported.


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network ACL**.

3. In the top menu bar, select the target project and region.

4. Click **Configure rule** on the right side of the target Network Access Control List.

5. On the **Inbound rule** or **Outbound rule** tab, click **Edit Inbound rule** or **Edit Outbound rule**.

6. Click  **+Add rule** at the bottom left corner to add a new ACL rule to the list for configuration.

7. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Priority |The priority at which inbound/outbound rules take effect. Each priority level can only be assigned to a single rule. A smaller numerical value indicates a higher priority. When adding multiple rules sequentially, their priorities decrease in order. |2 |
   |Strategy |Select the authorized policy for inbound/outbound from the dropdown list. Supports allow and deny. |Allow |
   |Agreement |Select the transport protocol supported by the network ACL from the dropdown list.<br><br><br>* ICMP: Internet Control Message Protocol. When this protocol is selected, the destination port information cannot be filled.<br><br>* ICMPV6: Internet Control Message Protocol version 6. When this protocol is selected, the destination port information cannot be filled.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Network Access Control List IPv6 feature in Beta stage. If you need a trial, please contact your account manager.   </div><br>   <br><br>* TCP: Transmission Control Protocol.<br><br>* GRE: Generic Routing Encapsulation Protocol. When this protocol is selected, the destination port information cannot be filled.<br><br>* UDP: User Datagram Protocol.<br><br>* ALL: All supported protocols. When all protocols are selected, the destination port information cannot be filled. |TCP |
   |Source/destination address |Enter the source IP address for inbound traffic or the destination IP address for outbound traffic. 0.0.0.0/0 represents all IP addresses. |0.0.0.0/0 |
   |Destination port |Enter the destination port for inbound/outbound, value ranges from 1 to 65535. Required when selecting TCP or UDP protocol.<br><br><br>* Single port: Enter a port number, such as 22.<br><br>* Port range: Use a hyphen to connect the start port and end port (e.g., 1\-100).<br><br>* All ports: ALL (this value cannot be configured manually). |22 |
   

8. Click **Save** to complete the action.


<span id=".5Yig6Zmk572R57ucQUNM6KeE5YiZ"></span>
## Delete Network Access Control List rule


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network ACL**.

3. In the top menu bar, select the target project and region.

4. Click **Configure** on the right side of the target Network Access Control List.

5. On the **Inbound rule** or **Outbound rule** tab, find the rule to be deleted on the right, then click **Delete**.

6. Click **Delete** to complete the action.


<span id=".5YW25LuW5pON5L2c"></span>
## Other actions


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network ACL**.

3. In the top menu bar, select the target project and region.

4. Click **Configure rule** on the right side of the target Network Access Control List.

5. On the **Inbound rule** or **Outbound rule** tab, click **Edit Inbound rule** or **Edit Outbound rule**.

   * **Insert Network Access Control List rule**

      1. Click **Insert** on the right side of the target entry, and select **Insert row above** or **Insert row below**.

      2. Add inbound/outbound rules in the new row.

      3. Click **Save** to complete the action.

   * **Edit Network Access Control List rule**

      1. Modify inbound or outbound rules.

      2. Click **Save** to complete the action.

   * **Modify the priority of network ACL rules**

      1. Place the mouse on the drag icon to the left of the rule priority you want to modify and drag the rule up or down to the appropriate position.

      2. Click **Save** to complete the action.


<span id="H4Sg7Set"></span>
## Related documents

[UpdateNetworkAclEntries](https://docs.byteplus.com/en/docs/vpc/UpdateNetworkAclEntries)

&nbsp;
