---
title: "Configuring a backend server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-03"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Create a backend server group, and add the created backend servers to provide services through port 80.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<span id=".5q2l6aqk5LiA77ya5Yib5bu65ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Step 1: Create backend server group


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target CLB instance name, and select the Server Group tab.

4. Click **Create Server Group** and configure the backend server group according to the table below.

   
   |Name |Explanation |Example Value |
   |---|---|---|
   |Name |Enter the name of backend server group. |group01 |
   |Topic |Select the server group type. |Server type |
   |IP version |Protocol type for the backend server's private IP address. |IPv4 |
   |Tags |Add tags to the backend server group. |Do not add tags |
   

5. Click **Create** to complete the action.


<span id=".5q2l6aqk5LqM77ya5re75Yqg5ZCO56uv5pyN5Yqh5Zmo"></span>
### Step 2: Add backend server


1. Click the name of the created backend server group to go to the details page.

2. Click **Add server**.

3. Select the basic mode (without enabling Advanced Mode), and select the existing Elastic Compute Service (ECS) instances.

4. Click Next.

5. Configure the port and weight for the added ECS instances.

   In this example, the port is set to 80 and the weight is set to 100.

6. Click **Add** to complete the action.


<span id=".5q2l6aqk5LiJ77ya6YWN572u5LqR5pyN5Yqh5Zmo55qE5a6J5YWo57uE"></span>
### Step 3: Configure ECS security group

Allow CLB traffic through the ECS security group.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This document uses the example of an IPv4 Server Group (server type) attached to a TCP listener. For configuring security group rules in other scenarios, please refer to Server group security group configuration.</div>



1. Log in to the [security group console](https://console.byteplus.com/vpc/securityGroup).

2. In the top menu bar, select the target project and region.

3. On the left side of the target security group, click Edit Rule to access the rule details page.

4. Click Add Rule to access the page to add rules in the inbound direction.

5. See the table below to configure Security group rules.

   
   |No. |Strategy |Protocol type |Port range |Source IP address |Description |
   |---|---|---|---|---|---|
   |1 |Allow |TCP |Port provided by the ECS service (80 in this example) |Client address (e.g., 0.0.0.0/0) |Receive IPv4 client requests forwarded by the CLB |
   |2 |Allow |TCP |Ports provided by ECS service (80 in this example) |100.64.0.0/10 |Receive health check request |
   

6. Click **Confirm** to complete the action.
