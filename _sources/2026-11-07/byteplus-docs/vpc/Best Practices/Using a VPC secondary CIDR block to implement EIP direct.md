---
title: "Using a VPC secondary CIDR block to implement EIP direct"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Using_a_VPC_secondary_CIDR_block_to_implement_EIP_direct"
---

<span id="UP8U9Xz3"></span>
## Scenarios

For business scenarios with strong requirements for EIP direct connection, you can follow the guidance in this document to create a dedicated subnet separately, facilitating subsequent unified operations and management.

<span id="2vsfXCGw"></span>
## Preparations


* Please contact your account manager to enable the following invite\-only beta features in advance:

   * Secondary CIDR supports being in a different major segment from the primary CIDR block

   * VPC supports internet CIDR blocks

   * EIP address pool

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can directly use an EIP or an EIP address pool, simply ensure that the VPC CIDR block includes the CIDR block of the EIP or EIP address pool. <strong>It is recommended to prioritize using an EIP address pool, as this method supports using multiple EIPs simultaneously</strong>.      </div>
      

* If you do not use the default VPC, create a VPC in advance. For the steps, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).


<span id="YA6EQNJH"></span>
## Procedures

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The following section only covers essential parameters and their recommended values. For all parameters not explicitly discussed, retain the default settings unless otherwise required by your specific use case.</div>


<span id="X5Gx9sUs"></span>
### Step 1: Create EIP address pool


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select a target region and project.

3. In the left navigation tree, select **Access to Internet \> IP Address Pool**.

4. Click **Create IP Address Pool** and configure the relevant parameters.

   
   |Parameters |Notes |Example |
   |---|---|---|
   |**Basic information** |||
   |Billing method |Currently only Pay\-as\-you\-go is supported. |Pay\-as\-you\-go |
   |Region |Select the region of the IP address pool. VPCs are isolated across regions by default. Select a region closer to your business operations to reduce network latency and improve access speed. |China (Beijing) |
   |Name |Enter the name of the IP address pool. |IPpool01 |
   |**Line configuration** |||
   |ISP |Select the ISP of the IP address pool. |BGP (multi\-line) |
   |Add CIDR block |Enable the Add CIDR block feature. |Enable |
   |CIDR block allocation |Two allocation methods are supported: **mask** and **CIDR block**.<br><br><br>* Mask: Select the mask for the IP address; the system automatically allocates the IP address CIDR block. Value range: 24~28.<br><br>* CIDR block: Enter IP CIDR block. Currently only IPv4 CIDR blocks can be added. Cannot start with 0. Mask range: 23 to 30.<br><br>   > When selecting the "CIDR block" method, it is recommended that you first communicate with your account manager about the IP address CIDR block to be added; otherwise, allocation may fail. |Mask: /28 |
   

5. Follow the console guidance to review and accept the legal terms.

6. Click **Buy now** to complete the action.


On the list page, view the CIDR block of the IP address pool, such as `120.XX.XX.48/28`.

<span id="AYM11lPU"></span>
### Step 2: Apply for EIP


1. In the left navigation tree, select **Access to Internet \> EIP**.

2. Click **Apply for EIP**.

3. Configure parameters based on the table below.

   
   |Parameters |Notes |Sample value |
   |---|---|---|
   |Billing method |This topic selects pay\-as\-you\-go. |Pay\-as\-you\-go |
   |Region |Select a region for the EIP. |China (Beijing) |
   |Name |Type in a name for the EIP. |eip\-1 |
   |Security protection |Select the protection type for the EIP. |default |
   |ISP |Select an ISP for the EIP. BGP (multi\-ISP) is recommended. |BGP (multi\-line) |
   |Metering method |When the billing method is **Pay\-as\-you\-go**, you can choose between two billing modes: **Pay\-by\-bandwidth** or **Pay\-by\-data\-transfer**. |Pay\-by\-data\-transfer |
   |Bandwidth Package |If the billing method is **Pay\-as\-you\-go**, check Add EIP to Bandwidth Package as needed.<br><br>After being added to the Bandwidth Package, the EIP invalidates the billing method and maximum bandwidth, and shares the bandwidth of the Bandwidth Package. |No |
   |IP Address Pool |Only Pay\-as\-you\-go EIPs can enable IP address pool. After enabled, EIP gets an IP address from the specified IP address pool, and no longer incurs IP config fee. |Enable |
   |Maximum bandwidth |Set the maximum bandwidth for the EIP. |1 Mbps |
   |Quantity |Type the number of EIPs applied. |1 |
   

4. Follow the console guidance to review and accept the legal terms.

5. Click **Agree and buy** to complete the action.


The IP address of the EIP is `120.XX.XX.50`.

<span id="H1uZUVxn"></span>
### Step 3: Add secondary CIDR

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic adopts the method of adding a secondary CIDR to the VPC. You can also directly create a VPC that uses an internet CIDR block as the primary CIDR, using the internet CIDR block directly as the VPC's primary CIDR block.</div>



1. Log in to [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select the target project and region.

3. Click the name of the target VPC.

4. On the **CIDR Block Management** tab, click **Add secondary IPv4 CIDR**.

5. Enter the CIDR block of the IP address pool, such as `120.XX.XX.48/28`.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When selecting a secondary CIDR, note the following:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The subnet CIDR block must belong to the VPC CIDR block, and the subnet mask length must be larger than the VPC mask length; it is recommended to choose a larger CIDR block when planning the VPC to facilitate splitting into multiple subnets later.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After creating a subnet, the first two and the last IP addresses in the CIDR block are reserved by the system for network address, gateway address, and broadcast address respectively, and cannot be assigned to business instances.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you need all IPs in the example CIDR block <code>120.XX.XX.48/28</code> to be usable, you can plan the VPC CIDR block as <code>120.XX.XX.0/24</code> and the subnet CIDR block as <code>120.XX.XX.0/25</code>.   </div>
   

6. Click **OK** to complete the action.


<span id="tTfGJZl8"></span>
### Step 4: Create subnet for secondary CIDR


1. Log in to [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation tree, select **Subnet**.

3. In the top menu bar, select the target project and region.

4. Click **Create Subnet**.

5. Configure parameters based on the table below.

   
   |Parameters |Notes |Sample value |
   |---|---|---|
   |VPC |Select the VPC for the subnet. |vpc\-01\|192.168.0.0/16 |
   |CIDR |Select the secondary CIDR block. |120.XX.XX.48/28 (secondary CIDR block) |
   |Zone |Availability Zones (AZs) are physically isolated locations within the same region, with independent power and network infrastructure. Within the same VPC, availability zones can communicate over the private network. |AZ\-A |
   |Name |Type in the name of the subnet. |subnet\-cidr |
   |IPv4 CIDR |Enter a subset of the IP address pool CIDR block. |120.XX.XX.48/29 |
   

6. Click the add icon (+), then enter the tag key and value to assign tags to the newly created subnet(s), facilitating subnet categorization and search.

7. Click **Create** to complete the configuration.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If other VPCs need to access resources within this VPC's secondary CIDR over private networks via products such as CEN or TR, you need to <a href="https://docs.byteplus.com/en/docs/vpc/Configuring-a-user-CIDR-block">Add user CIDR block</a> in the accessing VPC and set that user CIDR block to this VPC's secondary CIDR block.</div>


<span id="ykXgxmO3"></span>
### Step 5: Create ECS


1. In the left\-side navigation pane, click **Quick Links \> ECS**.

2. Click **Create instance** to begin configuring your ECS instance.

3. Follow the interface prompts to complete ECS configuration step\-by\-step, including base configuration, network & security, and advanced settings. Specific configurations are detailed in the table below.

   
   |Parameters |Notes |Sample value |
   |---|---|---|
   |Billing method |ECS billing method. |Pay\-as\-you\-go |
   |Region and AZ |Select the region and availability zone for the ECS. The region must match the VPC region, and the availability zone must match the subnet's availability zone. |China (Beijing) Availability Zone A |
   |Image |Images provide ECSs with pre\-configured operating systems and essential application data. |CentOS 7.9 |
   |VPC |Select the created VPC. |vpc\-01\|192.168.0.0/16 |
   |Subnet |Select the subnet of the secondary CIDR, and manually assign an IP address to the network interface; the IP address should be the EIP address applied for above. |subnet\-cidr\|120.XX.XX.48/29<br><br>Custom\-assign IP<br><br>120.XX.XX.50 |
   |EIP |Do not enable. |Do not enable |
   |Security group |This topic selects the default security group "Default" in vpc\-01 to control inbound and outbound traffic for the primary network interface of ECSs. |Default |
   

4. Click **Next: Confirm**.

5. Follow the console guidance to review and accept the legal terms.

6. Click **Buy now** to redirect to the purchase submitted page.

7. Click **Go to console** to redirect to the Instances page and view the new instance.


<span id="VHPGWy6U"></span>
## Step 6: Associate EIP


1. On the ECS list page.

2. Click **Associate** under the **Primary IPv4 address** column to the right of ECS\-A.

3. Select the EIP Address `120.XX.XX.50` applied above, click **Attach** to complete the action.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When implementing EIP direct connection through a secondary CIDR, the private IP address of the ECS must be the same as the bound EIP address.</div>


<span id="s7v2BRWW"></span>
### Step 7: View/Allow security group

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


<span id="TwHjHEug"></span>
## Verify


1. Remotely log in to ECS\-A.

2. Execute the `ping 8.8.8.8` command in the command line. Successful ping indicates access to the internet.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fcba3bf711e346482e905c915392e7c6.png) </span>

3. Execute the following command to check the IP address. If it is an EIP address, it indicates EIP direct.

   `ip addr`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e30290f4ed4c44e0ee6cd9c92bf0c875.png) </span>


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
