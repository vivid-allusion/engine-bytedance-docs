---
title: "Accessing the Internet via Internet NAT Gateway from an on-premises data center"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Configuring-servers-in-a-data-center-to-communicate-with-the-internet-using-an-Internet-NAT-Gateway"
---

If servers in your on\-premises data center need to communicate with the internet, you can share a cloud\-based Internet NAT Gateway to centrally manage their internet ingress/egress.This topic describes how to enable servers in an on\-premises data center to use this shared gateway.

<span id=".6IOM5pmv5LuL57uN"></span>
## Background

A company uses a shared cloud\-based Internet NAT Gateway for internet communication for servers in its on\-premises data center.


* On\-premises data center: CIDR block: 172.16.1.0/24; Server A IP address: 172.16.1.11.

* Cloud VPC Information: VPC Name: VPC\-A; VPC CIDR Block: 192.168.0.0/16; Subnet 1 Name: Subnet\-A; Subnet 1 CIDR Block: 192.168.1.0/24; ECS IP Address: 192.168.1.22.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f48a2ac08a32f16568d21c0d0e99b17.png) </span>


The diagram above illustrates a single SNAT rule (all\-pass mode). In practice, you can create multiple SNAT and DNAT rules as needed.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Complete the following steps based on the background information before proceeding:


1. Create a VPC with parameters consistent with the Background description. For specific actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

2. Create an ECS\-A (192.168.1.22) without an EIP in Subnet\-A of VPC\-A. For detailed steps, see [Purchasing an Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

3. Create a CEN and add VPC\-A. For specific actions, see [Creating a CEN instance](https://docs.byteplus.com/en/docs/cen/CEN-instances-01).

4. Configure a Direct Connect to enable communication between the on\-premises data center and the VPC. For detailed steps, see [Connecting on-premises data center to VPC](https://docs.byteplus.com/en/docs/directconnect/Quick-start).

5. Apply for 1 EIP not bound to any cloud resources. This topic uses EIP\-1 (180.XX.XX.44). For procedure, see [Applying for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6aqM6K-B5pys5ZywSURD5LiO5LqR5LiKVlBD5LqS6YCa"></span>
### Step 1: Verify connectivity between on\-premises data center and VPCs


1. Log in to local Server A (172.16.1.11).

2. Execute the `ping 192.168.1.22` command in the command line.

3. A successful `ping` response confirms connectivity between your on\-premises data center and VPCs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If <code>ping</code> fails, see <a href="https://docs.byteplus.com/en/docs/directconnect/Direct-Connect-gateway#.5bey5a6M5oiQ5LqR5LiK5LqR5LiL6YWN572u77yM5L2G572R57uc5LuN54S25LiN6YCa77yM5aaC5L2V5o6S5p-l77yf">Troubleshooting network connectivity issues after cloud\-to\-on\-premises configuration</a>.</div>


<span id=".5q2l6aqk5LqM77ya6YWN572u5YWs572RTkFU572R5YWz"></span>
### Step 2: Configure Internet NAT gateway

Through the following steps, you can create an Internet NAT Gateway in all\-pass mode within the VPC.


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select the target region and project. In this example, they are **China (Beijing)**  and **default**.

3. Click **Create NAT Gateway**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Billing method |Supports pay\-as\-you\-go and subscription. |Pay\-as\-you\-go |
   |Regions |Select the region where the internet NAT gateway is located. |China (Beijing) |
   |Name |Set a name for the Internet NAT gateway. |NAT\-X |
   |Metering method |When the billing method is **Pay\-as\-you\-go**, select a metering method for the Internet NAT gateway. Supports [Pay-by-specification](https://docs.byteplus.com/en/docs/natgateway/Pay-as-you-go) and [Pay-by-CU](https://docs.byteplus.com/en/docs/natgateway/Pay-by-CU).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The metering method defaults to Pay\-by\-specification.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">With Pay\-by\-CU, you don't need to specify a specification. Performance scales dynamically based on demand, making it ideal for scenarios with significant traffic fluctuations.</div><br> |Pay\-by\-specification |
   |Specification |Select the specification of the Internet NAT gateway. |Small |
   |VPC |Select a VPC. |VPC\-A\|192.168.0.0/16 |
   |Subnet |Select a subnet from the dropdown list. |Subnet\-A \| 192.168.1.0/24 |
   |Project |Select the project to which the internet NAT gateway belongs as needed. |default |
   |Configuration mode |When the billing method is **Pay\-as\-you\-go**, select the configuration method for the Internet NAT Gateway.<br><br><br>* Manual configuration: After creation, you must manually associate an EIP and configure SNAT or DNAT entries.<br><br>* Auto\-configure (all\-pass mode): Automatically creates a 0.0.0.0/0 SNAT rule. |Automatic configuration (all\-pass mode) |
   |Gateway mode |Select the mode of the Internet NAT Gateway\-According to your networking scenario. The mode of an Internet NAT Gateway cannot be changed after creation. Proceed with caution.<br><br><br>* Internet egress is an IPv4 Gateway: Please select **Non\-passthrough mode.** <br><br>* Internet egress is an EIP: Please select **Pass\-through mode.**  |Pass\-through mode |
   |EIP |When the configuration method is set to **Automatic configuration**, select an EIP from the drop\-down list |EIP\-1 |
   |Tags |Add one or more user tags to the Internet NAT gateway as needed. |No tags added |
   

5. Click **Buy now**.

6. Follow the console guidance to review and accept Legal, and click **Buy now** to complete the operation.


<span id=".5q2l6aqk5LiJ77ya5omL5Yqo5Y-R5biD6Lev55Sx"></span>
### Step 3: Manually publish the route

You can follow the steps below to publish the route of the above Internet NAT gateway to the Cloud Enterprise Network (CEN).


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

3. In the top menu bar, select the region and project.

4. In the route table list, click the target system route table name.

5. Select the **Route entry \> Custom route** tab, and click **Publish** on the right side of the route entry where the next hop points to the Internet NAT gateway.

6. Click **Publish** to complete the propagation.

7. Verify whether the route was successfully published.

   1. Log in to the Cloud Enterprise Network console.

   2. Click the target CEN name to navigate to its details page.

   3. On the **Route Table** tab, view whether there is a route entry with the Destination CIDR Block of 0.0.0.0/0.


<span id=".5q2l6aqk5Zub77ya6aqM6K-B"></span>
### Step 4: Verification


1. Log in to local Server A (172.16.1.11) and execute `ping 8.8.8.8` in the command line.

2. If the `ping` is successful, it indicates that after local Server A is included in the SNAT rule, it can access the internet through the Internet NAT Gateway and EIP\-1.
