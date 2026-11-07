---
title: "Creating a security group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The Default security group Default may not be sufficient for your requirements. You need to create custom security groups to control the inbound and outbound traffic for your network interfaces.

<span id="tRxv9Kvb"></span>
## Action description


* When a VPC is created, the system automatically creates and associates a default security group with it.

* When a security group is created manually, the system automatically adds the following rules to it:

   * Inbound

      
      |Inbound |Priority |Strategy |Agreement |Port range |Source |Description |
      |---|---|---|---|---|---|---|
      |Inbound |1 |Allow |ALL |ALL |This security group |Allow ECSs within the same security group to communicate with each other<br><br>> CIDR\-Only security groups do not have this rule. |
      

   * Outbound

      
      |Outbound |Priority |Strategy |Agreement |Port range |Destination address |Description |
      |---|---|---|---|---|---|---|
      |Outbound |100 |Allow |ALL |ALL |0.0.0.0/0 |Allow all IPv4 traffic |
      |Outbound |100 |Allow |ALL |ALL |::/0 |Allow all IPv6 traffic |
      


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the target project and region.

4. Click **Create Security Group**.

5.  Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Name |Set the name of the Security Group. |sg\-01 |
   |VPC |Select the VPC for the Security Group. |vpc01 |
   |CIDR Only |Select whether to enable CIDR Only.<br><br><br>* If not selected, a standard security group will be created.<br><br>* If selected, a CIDR\-Only Security Group will be created. Such security groups are no longer restricted by IP address quotas and are suitable for business scenarios such as automatic resource expansion and large\-scale IP address usage.<br><br><br>For the differences, see [Security group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview#7mZUOiJq). |Not selected |
   |Access rules |Configure outbound and inbound rules of the security group according to the actual scenario. For rule parameters, refer to [Creating security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules). |\- |
   |Related project |Select the security group's project. [Learn more](https://docs.byteplus.com/en/docs/vpc/Managing-projects) |default |
   |Tags<br><br> |Add one or more custom tags to the Security Group as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources<br><br>Click the add icon to add a tag. |* Tag key: sg\-key<br><br>* Tag value: sg\-v1 |
   

6. Click **Create** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateSecurityGroup](https://docs.byteplus.com/en/docs/vpc/CreateSecurityGroup)

&nbsp;

&nbsp;
