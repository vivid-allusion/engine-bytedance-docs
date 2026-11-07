---
title: "Configuring inbound policies for internal firewall"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Configuring-inbound-policies-for-internal-firewall"
---

The internal firewall controls traffic flowing between Elastic Compute Service (ECS) instances, restricting unauthorized access. Upon publication, an access control policy for the internal firewall will be automatically synchronized with relevant ECS security groups and take effect. The Cloud Firewall console allows you to centrally manage security group policies, without the need to switch between the regions where the ECS instances are located. This topic introduces how to configure the internal firewall.

<span id="Safety group overview"></span>
## Safety group overview

Security groups are collections of security rules that provide stateful inspection and packet filtering capabilities. They can be used to segment a network in the cloud into security domains, serving as an essential means of network isolation.

Once a security group is created, you can configure outbound and inbound policies for it. These policies will control the outbound and inbound traffic of ECS instances within it. Configured access policies will also be automatically applied to new ECS instances as they are added to it.

<span id="08425665"></span>
## Steps


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Access control** \> **Internal boundary**.

3. Click **Add security group**, then fill in the parameters for the security group.

   
   |**Parameter** |**Description** |
   |---|---|
   |Security group name |Name the security group. Up to 128 characters. |
   |Description |Provide information about the security group, such as its purpose. Up to 255 characters. |
   |Region |Select the region where the Virtual Private Cloud (VPC) is located. |
   |VPC |Select the VPC that the security group belongs to. |
   |Access control rule |Configure inbound and outbound policies for the security group as needed. |
   


<span id="Associating network interfaces with the security group"></span>
## Optional action

After the security group is created, you can associate network interfaces with it to enable it to protect the ECS instances where the network interfaces are located.


1. On the **Internal boundary firewall** screen, click **Details** to the right of the target security group list.

2. In the **Associated NIC** tab, click **Add NIC**.

3. Check the network interface(s) to be associated with, then click **OK**.
