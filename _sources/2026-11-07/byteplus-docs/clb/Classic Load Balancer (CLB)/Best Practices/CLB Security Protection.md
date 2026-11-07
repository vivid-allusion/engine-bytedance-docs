---
title: "CLB Security Protection"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-security-defense"
---

This section describes how to implement traffic security in the Classic Load Balancer (CLB) service.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

While distributing the Internet traffic and Virtual Private Cloud (VPC) traffic, the CLB service can also control the inbound traffic of the CLB instances using the **Access Control List (ACL)**  feature. In addition, CLB integrates the **Network ACL** and **Security Group** features of the VPC to control inbound traffic of backend servers.

When combined with network ACL and security group, Access Control helps establish triple\-layer filtering between internal/external user traffic and backend server groups, safeguarding secure access to backend servers.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1941a52ff7770b39cd7785a8dc7116f9.png) </span>

&nbsp;

<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Term |Explaination |
|---|---|
|IAM |The CLB service supports the listener\-level ACLs. To allow or deny requests of some IP addresses to access a CLB instance through the listening port, you can configure an ACL for this listener. For more information, refer to [ACL Overview](https://docs.byteplus.com/en/docs/clb/Access-control-list-01). |
|Network ACL |The network ACL is a subnet\-based security layer provided by the VPC. It implements more accurate and flexible secure access policies. ACL entries are configured to control the inbound and outbound traffic of a subnet. All backend servers in a subnet that is associated with a network ACL entry are protected by this network ACL entry. For more information, refer to [Network ACL Overview](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview). |
|Security group |A security group is a logical group and an important network isolation measure. The security group rules control the inbound and outbound traffic of backend servers, and backend servers that join a security group are protected by the security group rules. For more information, refer to [Security Group Overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview). |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You are advised to plan the ACL entries for each layer of filtering in advance, and later update the entries according to service changes. The ACL entries take effect in real time.


* **Identity and Access Management (IAM)** : To use the ACL feature, you must create at least one ACL for centralized management of IP addresses. The ACL itself does not restrict the access control mode and access control is implemented by the listener either by means of the allowlist or denylist.

   Therefore, you must put IPs or IP segments with the same access control requirements in the same ACL, and choose the control mode when associating the ACL with a listener.

* **Network ACL**: The Network ACL feature applies to the subnet. Therefore, you only need to plan Identity and Access Management (IAM) rules for the respective subnet and add them to the Network ACL associated with the subnet.

* **Security Group**: The security group feature applies to the network interface. Therefore, you must plan ACL entries for each backend server (primary or secondary network interface) separately and add them to the security group associated with the backend server.


<span id=".6aaW5qyh5Yib5bu6"></span>
## Initial configuration

<span id=".56ys5LiA5q2l77ya5Yib5bu66K6_6Zeu5o6n5Yi2562W55Wl57uE"></span>
### Step 1: Create an Identity and Access Management (IAM) policy group


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target project and target region.

3. In the left\-side navigation pane, click **IAM**.

4. Click **Create access control policy group**. On the ACL creation page, configure the ACL name and IP entries.

   
   |Name |Limitations |Sample Value |
   |---|---|---|
   |Term |Configure the name of the ACL. |policy\-1 |
   |Affiliated project |Select the project to which the ACL belongs. |default |
   |IP entry |Consists of an IP address/address segment + remarks, with each line including one entry, formatted as "x.x.x.x\|remarks" or "x.x.x.0/x\|remarks", with remarks being optional. |180.184.66.168 10.0.2.0/24 |
   

5. Click **Confirm** to complete the actions.


<span id=".56ys5LqM5q2l77ya5Yib5bu6572R57ucQUNM5bm25YWz6IGU5a2Q572R"></span>
### Second step: Creating a network ACL and associating it with the subnet


1. Log in to[ the Network ACL console](https://console.byteplus.com/vpc/acl).

2. In the top menu bar, select the project and region of the target resource.

3. Click **Create Network ACL** to configure the network ACL by referring to the table below.

   
   |Name |Explaination |Sample Values |
   |---|---|---|
   |Term |Configure the name of the network ACL. |acl\-01 |
   |Virtual Private Cloud |Select the VPC to which the network ACL belongs. |vpc\-02 |
   

4. Click **Confirm** to complete the Network ACL creation.

5. In the network ACL list, click **Edit Rule** on the right of the network ACL acl\-01.

6. Configure the inbound and outbound entries for the network ACL based on planning.

7. After configuration, click **Save** to complete the rule setup.

8. In the network ACL list, click **Associate Subnet** on the right of the network ACL acl\-01.

9. In the **Associate Subnet** zone, click **Add Association**.

10. Select the subnet to associate with, then click **Confirm** to complete the actions.


<span id=".56ys5LiJ5q2l77ya5Yib5bu65a6J5YWo57uE6KeE5YiZ5bm257uR5a6a572R5Y2h"></span>
### Step 3: Creating a security group rule and binding it to a network interface


1. Log in to[ the Security Group console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/securityGroup). 

2. In the top menu bar, select the target project and target region.

3. Click **Create Security Group**, and configure the security group by referring to the table below.

   
   |Name |Explaination |Sample Values |
   |---|---|---|
   |Term |Set the name of the new security group. |sg\-01 |
   |Virtual Private Cloud |Select the VPC to which the security group belongs. |vpc\-02 |
   |Access rules |Configure the inbound and outbound security group rules based on planning. For more information on the rules, refer to [Security Group Overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview). |\- |
   

4. Click **Confirm** to complete the actions.

5. In the security group list, click **Associate Network Interface** to the right of security group sg\-01.

6. On the **Associate Network Interface** tab, click the **Associate Network Interface** button.

7. Select the network interfaces to associate with, and click **OK** to complete the action.


<span id=".56ys5Zub5q2l77ya5Yib5bu65ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Step 4: Create Server Group

Select the network interface bound in the previous step and create a backend server group by referring to [Creating a Server Group](https://docs.byteplus.com/en/docs/clb/Creating-a-server-group).

<span id=".56ys5LqU5q2l77ya5Yib5bu655uR5ZCs5Zmo6YWN572u6K6_6Zeu5o6n5Yi244CB5bm25YWz6IGU5ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Step 5: create listener configuration Identity and Access Management (IAM), and attach Server Group


1. When [Creating a listener](https://docs.byteplus.com/en/docs/clb/Creating-a-TCP-listener), configure **Protocol & Listener** in the first step to enable Identity and Access Management (IAM), select control methods, and policy groups.

   
   |Name |Explaination |Sample Value |
   |---|---|---|
   |Control mode |Enable the ACL feature, and select an access control mode. |blocklist |
   |ACL name |Select an ACL. IPs in the ACL will be added to the denylist. |policy\-1 |
   

2. Associate the listener with the backend server group.

   * For a Layer\-4 listener, associate the listener with a backend server group at Step 2: **Server Group**.

   * For a Layer\-7 listener, either associate a **Default backend server group** during Step 2 of [Creating a listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-listener), or reference and [Add forwarding a rule](https://docs.byteplus.com/en/docs/clb/Adding-a-forwarding-rule) to associate backend server groups.


<span id=".5pu05pS56YWN572u"></span>
## Configuration modification


<Tabs>
<Tab zoneid="D8guWp5fdb" title="Adding or deleting an IP entry in the ACL">
<TabTitle>Adding or deleting an IP entry in the ACL</TabTitle>

1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target region and target project.

3. In the left\-side navigation pane, select **Access Control** to view the ACL page.

4. In the policy group list, click **Manage IP Entry** to the right of the policy group policy\-1.

5. Click **Add IP Entry** to add a new IP entry, then click **OK** to complete the action.

6. Click **Delete** to the right of the target IP entry to delete the entry.


</Tab>
<Tab zoneid="kSeK3o9vOP" title="Adding or deleting a network ACL entry">
<TabTitle>Adding or deleting a network ACL entry</TabTitle>

1. Log in to[ the Network ACL console](https://console.byteplus.com/vpc/acl). 

2. In the top menu bar, select the target region and target project.

3. In the network ACL list, click **Edit Rule** on the right of the network ACL.

4. Switch to the Outbound/Inbound rules tab, and click either **Edit Inbound Rule** or **Edit Outbound Rule** button.

5. Click **Add Rule** at the lower left, and configure the inbound and outbound rules separately.

6. Click **Save** to complete the addition of inbound and outbound rules.

7. Click **Delete** on the right of the target rule to complete the operation.


</Tab>
<Tab zoneid="eSz44z1UKn" title="Adding or deleting a security group rule">
<TabTitle>Adding or deleting a security group rule</TabTitle>

1. Log in to[ the Security Group console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/securityGroup). 

2. In the top menu bar, select the target project and target region.

3. In the security group list, click **Edit Rule** on the right of the security group sg\-01.

4. Click **Add Rule**, and configure an outbound or inbound security group rule.

5. Click **OK** to add the rule.

6. Click **Delete** on the right of the target security group to complete the action.


</Tab>
<Tab zoneid="XJQZJIgrMy" title="Enabling the ACL feature when the listener is running">
<TabTitle>Enabling the ACL feature when the listener is running</TabTitle>

1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target region and target project.

3. Click **Configure Listener** on the right side of the target CLB instance list.

4. On the right of the target listener list, Click  **···**   **\> Edit IAM**.

5. Re\-configure the ACL.

6. Click **Confirm** to complete the actions.


</Tab>
</Tabs>
