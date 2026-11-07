---
title: "Enabling IPv6 for a VPC"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_for_private_networks"
---

This topic describes how to enable IPv6 for a Virtual Private Cloud (VPC) and subnets.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">IPv6 is the beta stage. To request a trial, please contact your account manager.</div>


<span id=".VlBD5byA5ZCvSVB2Ng=="></span>
## Enable IPv6 for a VPC

<span id=".5paw5bu6VlBD5byA5ZCvSVB2Ng=="></span>
### Enable IPv6 when creating a VPC


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select your target region.

3. Click **Create VPC** to enter the Create VPC page.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region where the VPC is deployed. |China (Beijing) |
   |Name |Type in the name for the VPC. |vpc\-01 |
   |**CIDR block** |||
   |IPv4 CIDR |Set the IPv4 CIDR block. |192.168.0.0/16 |
   |IPv6 CIDR |Specify whether to enable the IPv6 CIDR block. After enabling, the following applies:<br><br><br>* ISP: Currently support BytePlus Auto\-assign (i.e., BGP multi\-ISP). If you need another ISP, contact your account manager.<br><br>* IPv6 CIDR: The system automatically allocates the IPv6 CIDR block to the VPC based on the ISP. IPv6 addresses support intranet communication.<br><br><br>The system automatically creates an IPv6 Gateway to enable Internet bandwidth for IPv6 addresses, allowing communication between the VPC's IPv6 addresses and the internet. |Enabled<br><br>BytePlus Auto\-assign<br><br>2408:XXXX:0:a600::/56 |
   |**Subnet** |||
   |Availability zone |Within the same VPC, intranets between availability zones interconnect. |Availability Zone A |
   |Name |Type in the name of the subnet. |subnet\-01 |
   |IPv4 CIDR |Set the IPv4 CIDR block. |192.168.1.0/24 |
   |IPv6 CIDR |Specify whether to enable the IPv6 CIDR block for the subnet. After enabling, you can type a decimal number from 0\-255 to define a `/64` subnet IPv6 CIDR block. |Enabled<br><br>2408:XXXX:0:a60**<ins>1</ins>**::/64 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more parameter details, see <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC">Creating a VPC</a>.   </div>
   

5. Click **Create** to complete the action.


<span id=".5Li65bey5pyJVlBD5byA5ZCvSVB2Ng=="></span>
### Enable IPv6 for an existing VPC


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select the target project and region.

3. Click **Enable IPv6** to the right of your target VPC. A dialog box appears to confirm enabling.

4. Select the ISP from the dropdown menu to automatically assign an IPv6 CIDR block of that type to the VPC, such as 2408:XXXX:0:a600::/56.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Currently, ISP supports BytePlus Auto\-assign (i.e., BGP multi\-ISP). If you need another ISP, please contact your account manager.   </div>
   

6. Click **Enable** to complete the action.


The system automatically creates an IPv6 Gateway associated with the target VPC. This IPv6 Gateway is used to subsequently [enable Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth) for the IPv6 address, enabling Internet connectivity for the VPC's IPv6 address.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After enabling IPv6 for the VPC, you also need to enable IPv6 for your target subnet.</div>


<span id=".5a2Q572R5byA5ZCvSVB2Ng=="></span>
## Enable IPv6 for a subnet

<span id=".5paw5bu65a2Q572R5byA5ZCvSVB2Ng=="></span>
### Enable IPv6 when creating a subnet

The VPC to which the new subnet belongs has enabled IPv6.


1. Log in to the [Subnet console](https://console.byteplus.com/vpc/subnet).

2. In the top menu bar, select the project and region of your target resource.

3. Click **Create Subnet** to enter the Create Subnet page.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |VPC |Select the VPC for the subnet. |vpc\-01 |
   |IPv4 CIDR block |Select the IPv4 CIDR block to which the subnet belongs. |192.168.0.0/16 (primary CIDR block) |
   |IPv6 CIDR block |Specify whether to enable the IPv6 CIDR block for the subnet. After enabling, select the IPv6 CIDR block to which the subnet belongs. |2408:XXXX:0:a600::/56 |
   |Availability zone |Select the subnet's Availability Zone. |Availability zone A |
   |Name |Set the subnet's name. |subnet\-05 |
   |IPv4 CIDR |Set the subnet's CIDR block. |192.168.5.0/24 |
   |IPv6 CIDR |Type a decimal number from 0 to 255 to define a `/64` subnet IPv6 CIDR block. |Enabled<br><br>2408:XXXX:0:a60**<ins>1</ins>**::/64 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more parameter details, see <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet">Create a subnet</a>.   </div>
   

5. Click  **+Add Subnet** and configure subnet information as in the previous steps to create multiple subnets simultaneously.

   > A maximum of 3 subnets can be created at once.   
   

6. Click **Create** to complete the action.


<span id=".5Li65bey5pyJ5a2Q572R5byA5ZCvSVB2Ng=="></span>
### Enable IPv6 for an existing subnet

The VPC to which your target subnet belongs has enabled IPv6.


1. Log in to the [Subnet console](https://console.byteplus.com/vpc/subnet).

2. In the top menu bar, select the target project and region.

3. On the Subnet page, click **Enable IPv6** to the right of the target subnet to pop up the Enable IPv6 window.

4. Choose the target IPv6 CIDR block from the dropdown. Enter the decimal numbers 0 to 255 to define the subnet IPv6 CIDR block with a default mask of `/64`, such as 2408:XXXX:0:a60**<ins>1</ins>**::/64.

5. Click **Enable** to complete the action.
