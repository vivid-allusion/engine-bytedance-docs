---
title: "Adding a security group rule"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Prerequisites

Before adding security group rules, we recommend familiarizing yourself with [security group planning](https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups) content.

<span id=".5pON5L2c5Zy65pmv"></span>
## Action description


* Within the same security group, adding two rules with identical parameters (except for the description) is not allowed.

* A single security group supports a maximum of 200 IPv4 inbound rules, 200 IPv6 inbound rules, 200 IPv4 outbound rules, and 200 IPv6 outbound rules. If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to increase the corresponding quota.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Changes to security group rules (including adding, modifying, copying, or deleting rules) take effect immediately. These rules control both existing connections and any new connections established by the associated network interfaces. Please thoroughly evaluate the potential impact on live services and proceed with extreme caution.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the target project and region.

4. Click **Configure** on the right side of the target security group.

5. On the **Inbound rule** or **Outbound rule** tab, click **Add rule**.

6. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Priority |Set the priority of security group rules, ranging from 1 to 100, where the default value 1 represents the highest precedence.​​ |1 |
   |Strategy |Allow or deny traffic. When priorities are equal, the deny policy takes precedence over the allow policy. |Allow |
   |Protocol type |Supports ALL, TCP, UDP, ICMP, ICMPV6, GRE. |TCP |
   |Port range |Limit the port range based on different protocol types. Supports the following methods:<br><br><br>* Enter a single port number, such as 80.<br><br>* Enter a port range, e.g., 20\-25 or 1\-65535.<br><br>* You can also enter multiple port numbers or ranges and separate different port numbers or ranges by half\-width commas ( , ). This way, multiple security group rules with the same parameters except the port range are added. For example. `80, 90-100`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the protocol type is ALL, ICMP, ICMPV6 and GRE, only ALL is supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Ports 25, 135, 139, 444, 445, 5800, and 5900 are flagged as high\-risk by some Line Operators. Even if these ports are allowed in your security group, access for restricted users may still be blocked. Therefore, we strongly recommend using alternative, non\-restricted ports.</div><br> |80\-81 |
   |Source/destination address |* **Source Address**: This parameter applies only to inbound rules. It specifies the resources that are permitted or denied to initiate access to the ENIs within this security group.<br><br>* **Destination Address**: This parameter applies only to outbound rules. It specifies the destination resources that the ENIs within this security group are permitted or denied to access.<br><br>* The source/destination address can be set in the following ways:<br><br>   * Security Group: Select a security group from the dropdown. This uses the IP addresses of all ENIs within the selected security group as the source/destination. However, note that CIDR\-Only security groups do not support this method.<br><br>   * CIDR: Enter a CIDR block. All IP addresses within this network segment will be used as the source/destination.<br><br>   * Prefix List: Select a prefix list from the dropdown. All IP addresses in the prefix list will be used as the source/destination.<br><br>      A prefix list is a collection of CIDR blocks. For more details, see [Prefix List Overview](https://docs.byteplus.com/en/docs/vpc/Prefix-list-overview).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The number of inbound security group rules that can still be added to the current security group is not less than the maximum number of entries in the prefix list.   </div><br>    |10.XX.XX.12/32 |
   

7. Click **Add rule** to add multiple inbound or outbound rules sequentially.

8. Click **Confirm** to complete the action.


<span id="PbAA8anJ"></span>
## Example Use Cases

If you only need to temporarily allow all inbound and outbound traffic for functional testing, you can refer to the following security group configuration example:


|Direction |Priority |Strategy |Protocol type |Port range |Source/destination address |Description |
|---|---|---|---|---|---|---|
|Inbound |1 |Allow |ALL |ALL |Source address: 0.0.0.0/0 |Inbound Traffic: Allow All |
|Outbound |1 |Allow |ALL |ALL |Destination: 0.0.0.0/0 |Outbound Traffic: Allow All |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The above example should be used solely for testing and validation purposes. It poses security risks and must be implemented with extreme caution.</div>


For more examples, see [Security Group Use Cases](https://docs.byteplus.com/en/docs/vpc/Security-group-use-cases).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AuthorizeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupIngress)

* [AuthorizeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupEgress)
