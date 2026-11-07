---
title: "Building an IPv4 VPC"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

This topic describes how to quickly configure and use an IPv4 network.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ba4c2690b9af2f02c74487681cf743eb.png) </span>

<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following section only covers essential parameters and their recommended values. For all parameters not explicitly discussed, retain the default settings unless otherwise required by your specific use case.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu6VlBD5Y-K5a2Q572R"></span>
### Step 1: Create the VPC and subnet

You can refer to the following operations to create one VPC and two subnets.


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select your target region.

3. Click **Create VPC**.

4. Configure parameters based on the table below.

   
   |Parameters |Notes |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region of the VPC. |China (Beijing) |
   |Name |Enter the name of the VPC. |vpc\-01 |
   |**CIDR block** |||
   |IPv4 CIDR |Set the VPC's IPv4 CIDR block.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After creation, the CIDR block of the VPC cannot be modified.</div><br> |192.168.0.0/16 |
   |**Subnet** |||
   |Zone |Select an Availability Zone. |AZ\-A |
   |Name |Type in the name of the subnet. |Subnet\-A |
   |IPv4 CIDR |Configure the subnet CIDR block, which must fall within the VPC’s address range.<br><br><div data-tips="true" data-tips-type="warning">Be cautious:</div><br><br><br><div data-tips="true" data-tips-type="warning">After creation, the CIDR block of the subnet cannot be modified.</div><br> |192.168.1.0/24 |
   

5. Click **Create** to complete the action.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65LqR5pyN5Yqh5Zmo5bm257uR5a6a5YWs572RSVA="></span>
### Step 2: Create ECS and associate an EIP

You can follow these steps to create ECS\-A.


1. In the left\-side navigation pane, click **Quick Links \> ECS**.

2. Click **Create instance** to begin configuring your ECS instance.

3. Follow the interface prompts to complete ECS configuration step\-by\-step, including base configuration, network & security, and advanced settings. Specific configurations are detailed in the table below.

   
   |Parameters |Notes |Sample value |
   |---|---|---|
   |Billing method |ECS billing method. |Pay\-as\-you\-go |
   |Region and AZ |Select the region and availability zone for the ECS. The region must match the VPC region, and the availability zone must match the subnet's availability zone. |China (Beijing) Availability Zone A |
   |Image |Images provide ECSs with pre\-configured operating systems and essential application data. |CentOS 7.9 |
   |VPC |Select the created VPC. |vpc\-01\|192.168.0.0/16 |
   |Subnet |Choose a subnet under the selected VPC. |Subnet\-A \| 192.168.1.0/24 |
   |EIP |Enable this option to automatically assign an EIP during ECS creation, providing Internet access capabilities.<br><br><br>* ISP: Supports BGP (Multi\-ISP).<br><br>* Metering method: The EIP Metering method is the same as that of the ECS instance. In this example, it is **Pay\-as\-you\-go**. Pay\-as\-you\-go EIP addresses support billing by bandwidth cap and pay\-by\-data\-transfer.<br><br>* Bandwidth cap: The maximum bandwidth for EIP, measured in Mbps. |* ISP: BGP (Multi\-ISP)<br><br>* Billing method: Pay\-by\-data\-transfer<br><br>* Bandwidth cap: 5Mbps |
   |Security group |This topic selects the default security group "Default" in vpc\-01 to control inbound and outbound traffic for the primary network interface of ECSs. |Default |
   

4. Click **Next: Confirm**.

5. Follow the console guidance to review and accept the legal terms.

6. Click **Buy now** to redirect to the purchase submitted page.

7. Click **Go to console** to redirect to the Instances page and view the new instance.


ECS is now successfully created with an EIP assigned by default, enabling bidirectional internet access.

<span id=".5q2l6aqk5LiJ77ya5p-l55yLL-aUvumAmuWuieWFqOe7hA=="></span>
### Step 3: View/Allow security group

View the ECS's security group and allow required traffic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default security group automatically allows private network communication between ECSs within the same group and outbound internet access. For demonstration purposes, this topic uses inbound port 80 access as an example. Please adjust configurations according to your actual requirements.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select your target region.

3. In the left\-side navigation pane, click **Instances**.

4. Click the name of ECS\-A.

5. On the **Security Group** tab, you can view the current rule status.

6. Click **Configure** on the right side of the target security group.

7. On the **Inbound rule** tab, click **Add rule**. Configure the relevant parameters according to the table below.

   
   |Parameters |Notes |Sample value |
   |---|---|---|
   |Priority |Set the priority of security group rules. |1 |
   |Policy |Select the Security Group policy. |Allow |
   |Protocol type |Select the protocol for the security group. |TCP |
   |Port range |Limit the port range based on different protocol types. |80 |
   |Source |Type in the IP address or CIDR block allowed to access ECSs within the security group.​​ |0.0.0.0/0 |
   

8. Click **Confirm** to complete the action.


<span id=".6aqM6K-B"></span>
## Verify


1. Remotely log in to ECS\-A.

2. Execute the `ping 8.8.8.8` command in the command line.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fcba3bf711e346482e905c915392e7c6.png) </span>
