---
title: "Configuring an IPv6 Gateway for IPv6 Internet access"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Configure_an_IPv6_gateway_to_access_the_IPv6_public_network"
---

<span id="GbiD8qSN"></span>
## Scenarios

This topic describes how to quickly configure an IPv6 Gateway to enable IPv6 traffic between an Elastic Compute Service (ECS) instance within a Virtual Private Cloud (VPC) and the internet.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id="wF4pCe0B"></span>
### Step 1: Configure IPv6 CIDR

Select a scenario based on your needs and configure the IPv6 CIDR block.


<Tabs>
<Tab zoneid="Gz5yznsMeD" title="New VPC">
<TabTitle>New VPC</TabTitle>

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select your target region.

3. Click **Create VPC** to enter the Create VPC page.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region where the VPC is deployed. |China (Beijing) |
   |Name |Type the name for the VPC. |VPC\-1 |
   |**CIDR block** |||
   |IPv4 CIDR |Set the IPv4 CIDR block. |192.168.0.0/16 |
   |IPv6 CIDR |Specify whether to enable the IPv6 CIDR block. After enabling, the following applies:<br><br><br>* ISP: Currently support BytePlus Auto\-assign (i.e., BGP multi\-ISP). If you need another ISP, please contact your account manager.<br><br>* IPv6 CIDR: The system automatically allocates the IPv6 CIDR block to the VPC based on the ISP. IPv6 addresses support intranet communication.<br><br><br>The system automatically creates an IPv6 Gateway to enable internet bandwidth for IPv6 addresses, allowing communication between the VPC's IPv6 addresses and the internet. |Enabled<br><br>BytePlus Auto\-assign<br><br>2408:XXXX:0:a600::/56 |
   |**Subnet** |||
   |Availability zone |Within the same VPC, intranets between availability zones interconnect. |Availability zone A |
   |Name |Type the name of the subnet. |Subnet\-1 |
   |IPv4 CIDR |Set the IPv4 CIDR block. |192.168.1.0/24 |
   |IPv6 CIDR |Specify whether to enable the IPv6 CIDR block for the subnet. After enabling, you can type a decimal number from 0\-255 to define a `/64` subnet IPv6 CIDR block. |Enabled<br><br>2408:XXXX:0:a60**<ins>1</ins>**::/64 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more parameter details, see <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC">Creating a VPC</a>.   </div>
   

5. Click **Create** to complete the action.


After creation, the system automatically adds a route entry with Destination CIDR as ::/0 and Next Hop as IPv6 Gateway to the system route table. If the subnet of IPv6 address is associated with a custom route table, manually add a route entry to that route table with Destination CIDR as ::/0 and Next Hop set as IPv6 Gateway. For procedure, see [Add a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry)


</Tab>
<Tab zoneid="AADx3iOAcO" title="Existing VPC without IPv6 enabled">
<TabTitle>Existing VPC without IPv6 enabled</TabTitle>

1. **Enable IPv6 for a VPC**

   1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

   2. In the top menu bar, select the target project and region.

   3. Click **Enable IPv6** to the right of your target VPC. A dialog box appears to confirm enabling.

   4. Select the ISP from the dropdown menu to automatically assign an IPv6 CIDR block of that type to the VPC, such as 2408:XXXX:0:a600::/56.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Currently, ISP supports BytePlus Auto\-assign (i.e., BGP multi\-ISP). If you need another ISP, please contact your account manager.      </div>
      

   5. Click **Enable** to complete the action.

2. **Enable IPv6 for a subnet**

   1. Click the name of target VPC to enter the details page.

   2. Click **Subnet** to enter the Subnet page.

   3. Click **Enable IPv6** to the right of the target subnet to open the Enable IPv6 dialog box.

   4. Select the target IPv6 CIDR block from the dropdown. Enter decimal numbers ranging from 0 to 255. Define the subnet IPv6 CIDR block with a default mask of `/64`, such as 2408:XXXX:0:a60**<ins>1</ins>**::/64.

   5. Click **Enable** to complete the action.


After configuration, the system automatically adds a route entry with Destination CIDR as ::/0 and Next Hop as IPv6 Gateway to the system route table. If the subnet of IPv6 address is associated with a custom route table, manually add a route entry to that route table. Set the Destination CIDR as ::/0 and Next Hop to IPv6 Gateway. For procedure, see [Add a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).


</Tab>
<Tab zoneid="bbZPJrotWK" title="Existing VPC with IPv6 enabled">
<TabTitle>Existing VPC with IPv6 enabled</TabTitle>

Add a new IPv6 CIDR block to a VPC that has enabled IPv6.


1. **Add secondary IPv6 CIDR**

   1. Log in to VPC console or VPC console.

   2. In the top menu bar, select the target project and region.

   3. Click **Add secondary CIDR** to the right of the target VPC. In the IPv6 field, select the ISP type from the dropdown. The system automatically assigns an IPv6 CIDR block of that type to the VPC, such as 2408:XXXX:0:a600::/56.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Currently, ISP supports BytePlus Auto\-assign (i.e., BGP multi\-ISP). If you need another ISP, please contact your account manager.      </div>
      

   4. Click **Add** to complete the action.

2. **Enable IPv6 for a subnet**

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If all existing subnets have IPv6 enabled, you can disable IPv6 for the target subnet and re\-enable with a new IPv6 CIDR block, or <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet">create a new subnet</a> with the new IPv6 CIDR block.   </div>
   

   1. Click the name of target VPC to enter the details page.

   2. Click **Subnet** to enter the Subnet page.

   3. Click **Enable IPv6** to the right of the target subnet to open the Enable IPv6 window.

   4. Select the target IPv6 CIDR block from the dropdown, enter decimal numbers 0–255, and define the default mask as `/64` for the subnet IPv6 CIDR block, such as 2408:XXXX:0:a60**<ins>1</ins>**::/64.

   5. Click **Enable** to complete the action.


</Tab>
</Tabs>


<span id=".5q2l6aqk5LqM77ya5Yib5bu65LqR5pyN5Yqh5Zmo"></span>
### Step 2: Create an ECS instance


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. Click **Create instance** to purchase an ECS instance.

3. Configure relevant parameters based on the table below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This section only covers essential parameters and their recommended values. Other parameters remain with default configurations. For more details, see <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances">Purchasing an ECS instance</a>.   </div>
   

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic configuration** |||
   |Region and AZ |Select the region and availability zone for the ECS instance. Its region must match the region of the VPC. |China (Beijing), Availability Zone A |
   |Mirror image |Select the image for the ECS. |Public image. CentOS 7.9. |
   |**Network & Security** |||
   |VPC |Select an existing VPC. |VPC\-1 |
   |Subnet |Select the subnet under the created VPC (vpc\-1). |Subnet\-1. Automatic IP assignment. |
   |IPv6 |Select whether to check **Free IPv6 addresses**. |Check |
   |EIP |Select whether to check **Assign Elastic IP (EIP)** . |Not check |
   |**Advanced settings** |||
   |Login credentials |Login credentials for accessing the target ECS instance. |Password |
   |Login name |Fixed as root. |root |
   |Login password |Password to log in to the ECS instance. Store it securely. |Ecs\*\*\*\*\*01 |
   |Confirm password |Re\-enter the login password. |Ecs\*\*\*\*\*01 |
   |Instance name |Name of the ECS instance. |ECS\-1 |
   

4. Click **Next** to verify selected configuration, purchase information, and fees.

5. After confirming no errors, follow the console guidance to review and accept the Legal.

6. Click **Buy now** to be redirected to the purchase submission page.

7. Click **Go to the console** to navigate to the Instances page and view the newly created instance.


On the Instances page, you can view the IPv6 address of the ECS instance (ECS\-1).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Some ECS images cannot automatically recognize the IPv6 address. You need to see <a href="https://docs.byteplus.com/en/docs/vpc/Configuring-private-IPv6-addresses-for-ECS-instances">Configuring a private IPv6 address for ECS</a> to confirm if the configuration is needed. If needed, the IPv6 address is effective after configuration.</div>


<span id=".5q2l6aqk5LiJ77ya6YWN572u5a6J5YWo57uE"></span>
### Step 3: Configure security group

If only verifying with the `ping6` command, skip this step.

If requiring access via HTTP or HTTPS from IPv6 terminals on the internet to a service deployed on the ECS, you need to configure a security group for the ECS.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region: **China (Beijing)** .

3. Click the name (ECS\-1) of the target instance to enter the details page.

4. Select the **Security Group** tab, then click **Configure** to the right of the default security group: **Default**.

5. On the Inbound rules tab, click **Add rule** to add the following inbound rules.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Priority |Set the priority of the security group rule. Range: 1\-100. Default: 1, which is the highest priority. |1 |
   |Strategy |Select a strategy for the security group, supporting allow or deny. When priorities are equal, the deny policy takes precedence over the allow policy. |Allow |
   |Protocol type |Select the protocol for the security group. Supports TCP, UDP, and ICMP. |TCP |
   |Port range |Limit the port range based on different protocol types. |80 |
   |Source |Type the IP address or CIDR block allowed to access ECSs within the security group.​​ |::/0 |
   

6. Click **Confirm** to complete the action.


<span id=".5q2l6aqk5Zub77ya5byA6YCaSVB2NuWFrOe9keW4puWuvQ=="></span>
### Step 4: Activate IPv6 Internet bandwidth


1. Log in to the [IPv6 Gateway consol](https://console.byteplus.com/eip/ipv6s)[e](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select your target region.

3. In the IPv6 Gateway instances list, click the name of target instance to enter the details page.

4. On the IPv6 Internet bandwidth tab, click **Enable Internet bandwidth** to the right of target IPv6 address.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Billing method |Currently only supports Pay\-as\-you\-go. |Pay\-as\-you\-go |
   |Metering method |Select the metering method for IPv6 Internet bandwidth. |Pay\-by\-data\-transfer |
   |ISP |Select the ISP for the IPv6 Internet bandwidth. |BGP (multi\-ISP) |
   |Bandwidth cap |Set the maximum bandwidth for IPv6 Internet bandwidth. |1 Mbps |
   |Agreement |Follow the console guidance to review and accept the legal terms. |\- |
   

6. Click **Apply** to complete the action.


<span id=".5q2l6aqk5LqU77ya6aqM6K-B"></span>
### Step 5: Verification

Use `ping6` to verify whether the ECS with IPv6 Internet bandwidth enabled can communicate with the internet.


1. Log in to the ECS instance (ECS\-1).

2. Type `ping6 240c::6666` in the command line. If data is returned, it confirms that ECS\-1 can access internet services via its IPv6 address.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If ping6 fails, see <a href="https://docs.byteplus.com/en/docs/IPv6/FAQs#.5Li65LuA5LmISVB2NueahOS6keacjeWKoeWZqOaXoOazlXBpbmc26YCaSVB2NueahOWFrOe9keWcsOWdgO-8nw==">Why can't IPv6 Elastic Compute Service ping the IPv6 Internet address</a>.   </div>
   

3. Log in to any terminal with IPv6 Internet access and open the terminal's command\-line interface.

4. Type `ping6 <ECS-1's IPv6 address>` in the command line. If data is returned, it confirms that the IPv6 terminal on the internet can properly access ECS\-1 of the VPC.
