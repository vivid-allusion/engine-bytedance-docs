---
title: "Configuring a backend server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-03"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Create a backend server group and add the created backend servers to allow the server group to provide services through port 443.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<span id=".5q2l6aqk5LiA77ya5Yib5bu65ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Step 1: Create backend server group

Perform the following steps to create two backend server groups group01 and group02:


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target instance name. On the instance details page, select the Server Group tab.

4. Click **Create Server Group** and configure the backend server group according to the table below.

   
   |Name |Explanation |Example Value one |The value is 2 in this document |
   |---|---|---|---|
   |Name |Enter the name of backend server group. |group01 |group02 |
   |Topic |Select the type of backend server group. |Server type |Server type |
   |IP version |Protocol type for the backend server's private IP address. |IPv4 |IPv4 |
   |Tags |Add tags to the backend server group. |No tags added |No tags added |
   

5. Click **Create** to complete the action.


<span id=".5q2l6aqk5LqM77ya5re75Yqg5ZCO56uv5pyN5Yqh5Zmo"></span>
### Step 2: Add backend server

Perform the following steps to add two Elastic Compute Service (ECS) instances to group01 and group02:


1. Click the name of the created backend server group to enter the details page.

2. Click **Add server**.

3. Select common mode, then check the created cloud server instances.

4. Click Next step to configure ports and weights for the added ECS instance.

   In this example, the port is set to 443 and the weight is set to 100.

5. Click **Add** to complete the action.


<span id=".5q2l6aqk5LiJ77ya6YWN572u5LqR5pyN5Yqh5Zmo55qE5a6J5YWo57uE"></span>
### Step 3: Configure security group of ECS instances

Allow CLB traffic in the security group of the Elastic Compute Service instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This article uses the example of associating an IPv4 backend server group (server type) with an HTTPS listener. For other scenarios involving security group configuration, see <a href="https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group">Configuring a backend server security group</a>.</div>



1. Log in to the [Security Group Console](https://console.byteplus.com/vpc/securityGroup).

2. In the top menu bar, select the project and region of your target resource.

3. On the left side of the target security group, click Edit Rule to access the rule details page.

4. Click Add Rule to access the page to add rules in the inbound direction.

5. See the table below to configure security group rules.

   
   |No. |Strategy |Protocol type |Port range |Source IP address |Description |
   |---|---|---|---|---|---|
   |1 |Allow |TCP |Port provided by ECS service (443 in this example) |100.64.0.0/10 |Receive health check requests and IPv4 client requests forwarded by CLB |
   

6. Click **Confirm** to complete the action.
