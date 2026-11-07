---
title: "Configuring EIP Direct"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Set-up-EIP-Pass-through-Mode"
---

<span id="TSbqN0ye"></span>
## Scenarios

Elastic IP Address (EIP) Direct applies to scenarios where intranet and internet traffic need to be forwarded separately to the private IP and EIP of the Elastic Compute Service (ECS). In normal mode (NAT mode, Network Address Translation), ECS instances associated with EIPs can access the internet via NAT mode, and internet traffic can be forwarded to the private IP address. After enabling pass\-through mode, you can view both the private IP address and its corresponding EIP in the ECS network interface. Internet traffic can only be forwarded to the EIP, while intranet traffic can only be forwarded to the private IP address. The detailed comparison of the two modes is as follows:


|Comparison |Normal mode |EIP Direct mode |
|---|---|---|
|Whether the EIP is visible on the network interface of the operating system |No |Yes |
|Network interface types supported by EIP association |Primary network interface and secondary network interface<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Associating an ECS automatically associates it with the primary network interface.</div><br> |Primary network interface and secondary network interface<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Associating an ECS automatically associates it with the primary network interface.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The secondary network interface must be associated with the ECS.</div><br> |
|Number of EIPs allowed by the network interface |* Primary network interface: Depends on the number of private IPs supported by the primary network interface.<br><br>* Secondary network interface: Depends on the number of the secondary network interface's private IPs.<br><br>   > The EIP corresponds to the private IP addresses on the secondary network interface. For example, if the secondary network interface has 10 private IP addresses, you can associate up to 10 EIPs with this elastic network interface.   <br>   <br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can check the number of private IPs that a single network interface can bind based on the ECS <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">instance type</a>.</div><br> ||
|Whether the private network feature is available after the EIP associates with the network interface |Yes ||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The EIP Direct feature is in the beta stage. To request a trial, please contact your account manager.</div>


* <div data-tips="true" data-tips-type="tip">Only ECS instance types currently on sale support enabling EIP Direct. For details, see <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications</a>.</div>



<span id=".5byA5ZCv55u06YCa"></span>
## Enable Direct

<span id="GzRfFo6h"></span>
### Instructions


* The direct feature only supports EIPs attached to ECS and a secondary network interface. The secondary network interface must already be attached to ECS. You can follow this procedure to enable Direct for an EIP already attached to a cloud resource, or check "EIP Direct" when [associating a cloud resource with the EIP](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP).

* Restarting the ECS does not invalidate the EIP Direct configuration. When the ECS switches the Virtual Private Cloud (VPC) or the network service restarts, EIP Direct becomes invalid. Please rerun the Direct script.

* Enabling EIP Direct may cause network interruption. Ensure it does not affect your business before proceeding.


<span id="giLDMyKr"></span>
### Procedure


<Tabs>
<Tab zoneid="jCEIkjVxwS" title="Linux OS">
<TabTitle>Linux OS</TabTitle>

After enabling EIP Direct on Linux\-based ECS, the primary and secondary network interfaces associated with the EIP can simultaneously forward both internet and private traffic.

<span id="lTTW3Zq1"></span>
#### Step 1: Enable EIP Direct on the Elastic IP console


1. Log in to the [Elastic IP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project for your target EIP.

3. In the EIP list, click  **··· \> Enable Direct** on the right side of your target EIP.

4. Click OK to complete the operation.


<span id="RON49w9n"></span>
#### Step 2: Download the EIP Direct script

[Download the EIP Direct script](https://eip.tos-cn-beijing.volces.com/bytedance_eip_direct.sh) and prepare the script file on your ECS using any of the following methods:


* Method 1: Upload the EIP direct script [to the ECS](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

* Method 2: Create a script file on the ECS.

   1. [Log in to the ECS](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   2. Execute the following command to create the bytedance_eip_direct.sh script file.

      `vim /root/bytedance_eip_direct.sh`

   3. Press the `i` key to enter edit mode, then copy and paste the local script file content.

   4. Press `Esc` to exit edit mode, then enter `:wq` and press Enter to save and exit.


<span id="0Tf28jOa"></span>
#### Step 3: Run the EIP script on the ECS


1. [Log in to the ECS](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to add execution permission to the script file.

   `chmod +x bytedance_eip_direct.sh`

3. Execute the following command to query the name of network interface that requires EIP Direct on the ECS.

   `ip addr`

4. Support configuring EIP Direct for multiple network interfaces. For example, to configure the network interface **eth0** with **33.xx.xx.11** as the direct EIP, execute the following command to run the script.

   `./bytedance_eip_direct.sh install eth0 33.xx.xx.11`

5. Execute the following command to check whether the configuration takes effect.

   `ip addr`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_412aeda7ecef33b7599b478300b2338a.png) </span>


If you can see the EIP address (33.xx.xx.11) and port information in the network interface (eth0) echo response, it indicates EIP Direct is successfully configured.


</Tab>
<Tab zoneid="If9qtUjzR1" title="Windows OS">
<TabTitle>Windows OS</TabTitle>

After enabling EIP Direct on a Windows\-based ECS, the primary/secondary network interfaces associated with this EIP can only forward internet traffic. If the ECS needs to access both the internet and intranet, configure the EIP and private IP on different network interfaces. [How to configure a private IP](https://docs.byteplus.com/en/docs/ecs/Configuring-secondary-private-IPv4-addresses-for-ECS-instances)

<span id="GjFOuffs"></span>
#### Step 1: Enable EIP Direct on the EIP console


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, click  **··· \> Enable Direct** on the right of the target EIP.

4. Click OK to complete the operation.


<span id="jSHSKFhU"></span>
#### Step 2: Download the EIP Direct script

Log in to the ECS and [download the EIP Direct script](https://eip.tos-cn-beijing.volces.com/bytedance_eip_direct.bat) in the browser.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">During the direct enabling process, the network may disconnect. It is recommended to <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance">use VNC to log in</a> to the ECS.</div>


<span id="qIuNHgTH"></span>
#### Step 3: Run the direct script on the ECS


1. Run the following command to query the network interface name requiring EIP Direct on the ECS.

   `ipconfig /all`

2. For example, to configure the network interface **Ethernet** with **118.xx.xx.207** as a direct EIP, execute the following command to run the script.

   `C:\\Users\\Administrator\\Desktop\\bytedance_eip_direct.bat Ethernet 118.xx.xxx.207`

3. Execute the following command to check whether the configuration takes effect.

   `ipconfig /all`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_999486161ef5ebb63614b13d0252c24b.png) </span>

   If you can see the EIP (118.xx.xx.207) and port information in the network interface (Ethernet) echo response, it indicates EIP Direct is successfully configured.


</Tab>
</Tabs>


<span id="giLDMyKr"></span>
## Disable EIP Direct

<span id=".5pON5L2c6K-05piO"></span>
### Instructions

You can follow this procedure to disable EIP Direct. Disabling may cause network interruption. Proceed with caution. If the EIP disassociates from the ECS instance's secondary network interface, or that secondary network interface with the direct configuration disassociates from the ECS instance, EIP Direct is automatically disabled.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


<Tabs>
<Tab zoneid="yg3733pqk5" title="Linux OS">
<TabTitle>Linux OS</TabTitle>

<span id="0ojsEB2d"></span>
#### Step 1: Disable Direct on the EIP console


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips). 

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, click  **··· \> Disable Direct** on the right side of the target EIP.

4. Click **Disable Direct** to complete the operation.


<span id="JJr83iNZ"></span>
#### Step 2: Manually disable Direct in the ECS console


1. [Log in to the ECS](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to disable Direct.

   `bash bytedance_eip_direct.sh uninstall eth0 33.xx.xx.11`


</Tab>
<Tab zoneid="RZMtvFo27J" title="Windows OS">
<TabTitle>Windows OS</TabTitle>

<span id="moOmkf9h"></span>
#### Step 1: Disable Direct on the EIP console


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of the target EIP.

3. In the EIP list, click  **··· \> Disable Direct** to the right of the target EIP.

4. Click **Disable Direct** to complete the operation.


<span id="ocMDSeBJ"></span>
#### Step 2: Change the network interface configuration in the ECS

After disabling EIP Direct on the console, manually change the network configuration of the network interface associated with the EIP to DHCP.


1. Log in to the [Elastic Compute Service instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Go to **Settings \> Network and Internet**, then click **Change adapter options**.

3. Right\-click the target network interface and select **Properties**.

4. In the network tab, modify the properties of **Internet Protocol Version 4 (TCP/IPv4)** .

5. On the **General** tab, select **Obtain an IP address automatically** and **Obtain DNS server address automatically**.

6. Click OK to complete the operation.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress): Associate an EIP with a cloud resource.
