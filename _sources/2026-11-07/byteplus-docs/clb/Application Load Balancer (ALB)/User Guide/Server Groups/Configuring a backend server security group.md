---
title: "Configuring a backend server security group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Allowing-ALB-to-access-back-end-servers"
---

ALB uses the private IP range 100.64.0.0/10 to communicate with backend servers. All requests sent from the ALB instance to the backend servers originate from this CIDR block. These requests include both client requests forwarded by the ALB instance and health check requests initiated by it.

You need to configure the security group rules for your backend servers to allow traffic from the 100.64.0.0/10 CIDR block.

### Configuration instructions

Configure an inbound rule in the security group to allow traffic with the following characteristics: source address 100.64.0.0/10, protocol TCP, and destination port being the service port of the backend server.

### Configuration examples

|**Strategy** |**Protocol type** |**Port range** |**Source** |**Description** |
|---|---|---|---|---|
|Allow |TCP |The service port of your backend server (e.g., 80) |100.64.0.0/10 |Receive both client requests forwarded by the ALB instance and health check requests initiated by it |

### Configuration procedures

1. Navigate to the Security group page.

2. In the top menu bar, select the project and region.

3. In the security group list, locate the target security group and click **Configure rule** in the **Actions** column.

4. On the **Inbound rule** tab, click **Add rule**.

5. In the pop\-up dialog box, configure the relevant parameters. For a detailed explanation of these parameters, see [Adding a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).
