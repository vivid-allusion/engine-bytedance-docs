---
title: "Creating an NLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-an-NLB-instance"
---

<span id="SXUV2PdC"></span>
## Prerequisites


* Ensure you have completed network planning. For details, see [Quick start](https://docs.byteplus.com/en/docs/clb/NLB-Quick-start).

* To ensure the elastic capability of Network Load Balancer (NLB) functions properly, make sure there are at least eight available IP addresses in each selected subnet. 


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click **Create NLB** and configure the related parameters according to the table below.

   
   |Parameter | |Notes |Sample |
   |---|---|---|---|
   |**Basic information** ||||
   |Region ||Select the region where the NLB instance resides. After you select a region, the created NLB instance can only be used by resources in the selected region and cannot be migrated. You must confirm that the region of the instance is the same as that of the backend server instance. |China (Beijing) |
   |Name ||Type the name of the NLB instance. |nlb01 |
   |**Network configuration** ||||
   |Virtual Private Cloud ||Select the VPC to which the NLB instance belongs. You can select all VPCs under the specified region of the current account, excluding shared VPCs. |vpc01 |
   |IP version ||Select the private IP address type of the NLB instance.<br><br><br>* **IPv4**: Only IPv4 is supported.<br><br>* **Dual stack**: Both IPv4 and IPv6 are supported.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">NLB IPv6 feature is currently in invite\-only Beta stage. For trial requests, please contact your account manager.</div><br> |IPv4 |
   |Network type (IPv4) ||Select the network type for the IPv4 address of the NLB instance. The two network types can be interchanged. For detailed information, see [Changing IPv4 network type](https://docs.byteplus.com/en/docs/clb/Changing-Network-Load-Balancer-instance-network-type).<br><br><br>* **Public**: The NLB instance can be accessed by both the IPv4 private network and the IPv4 internet.<br><br>* **Private**: This NLB instance can only be accessed by the IPv4 private network.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The domain name of a public NLB instance resolves to the EIP address of the NLB instance, while the domain name of a VPC NLB instance resolves to the private IP address of the NLB instance.</div><br> |Internet |
   |Network type (IPv6) ||Select the network type for the IPv6 address of the NLB instance.<br><br>Only private network types are supported during instance creation. If you want the NLB instance to be accessible via IPv6 internet, see [Changing IPv6 network type](https://docs.byteplus.com/en/docs/clb/Changing-Network-Load-Balancer-instance-network-type) after the NLB instance is successfully created. |Private |
   |EIP type ||Select the EIP type. Standard EIP and Global EIP are supported. [Learn more](https://docs.byteplus.com/en/docs/eip/What-is-EIP?lang=en)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Global EIP is in the invite\-only Beta. For trial requests, please contact your account manager.</div><br> |Standard EIP |
   |Network Border Group (NBG) ||Select the NBG to which the Global EIP belongs. This parameter is required only for Global EIPs.<br><br><br>* A NBG defines the access scope of a Global EIP. Select a border group close to your primary business for lower latency.<br><br>* Cross\-region transmission fees are incurred when a Global EIP and the associated backend resource are not in the same network border group.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">BytePlus presets optional NBGs based on your region and cloud resource deployment. If you need to use other NBGs, please contact your account manager for consultation.</div><br> |cn\-north\-beijing |
   |ISP ||Select the ISP of the Global EIP. |China Mobile |
   |Public egress ||Select the public egress of the Global EIP. This parameter is required only for Global EIPs.<br><br><br>* The available public egresses are determined by the NBG to which the Global EIP belongs.<br><br>* To ensure lower internet access latency, it is recommended to select a public egress that is closer to the internet peer outside the cloud. |Tianjin |
   |Availability Zone and subnet |AZ |Configure the availability zone and subnet for the NLB. If your services require high reliability, it is recommended to select two or more AZs. |Availability zone A<br><br> |
   ||Subnet |Provides a private deployment environment for the NLB instance. The system automatically creates an ENI within the subnet and attaches it to the NLB.  |subnet01 \| 192.168.3.0/24 |
   ||IPv4 address |Select the allocation method for the NLB instance's IPv4 address. After the instance is created, all assigned IPv4 addresses cannot be modified.<br><br><br>* **Auto assign IP**: The system automatically assigns 3 private IPv4 addresses to the network interfaces associated with the NLB, comprising 1 Service IP and 2 Local IPs.<br><br>* **Manual assign IP**: Please manually input an IPv4 address within the subnet range. The entered IPv4 address serves as the Service IP for the NLB\-associated network interface. The system will additionally automatically assign 2 Local IPs. |Auto\-assign |
   ||IPv6 address |Select the allocation method for the NLB instance's IPv6 address.<br><br><br>* Currently, only automatic assignment is supported. The system automatically assigns 3 private IPv6 addresses to the network interfaces associated with the NLB, comprising 1 Service IP and 2 Local IPs.<br><br>* This parameter needs to be configured only when the IP version is dual\-stack.<br><br>* After the instance is created, all allocated IPv6 addresses cannot be modified. |Auto\-assign |
   ||Elastic IP Address (EIP) |Provides internet capabilities for the NLB instance. Configure this parameter only when the network type (IPv4) is **Public**.<br><br><br>* **Newly purchased EIP**: This EIP is created along with the NLB instance.<br><br>   * **Standard EIP**: Defaults to Pay\-by\-data\-transfer, with BGP (multi\-ISP) as the ISP and a maximum bandwidth of 200 Mbps. <br><br>   * **GlobalEIP**: Defaults to Pay\-by\-main\-transfer.<br><br>* **Use existing EIP**: The selected EIP must meet the following conditions:<br><br>      * This EIP is not added to Bandwidth Package.<br><br>      * EIP type must be the same across different Availability Zones.<br><br>         * If standard EIPs are used, the line type, billing type, security protection type, and public egress of the EIPs in different Availability Zones of the NLB instance must also be consistent.<br><br>         * If Global EIPs are used, the NBG, ISP, billing method, and public egress of the EIPs in different Availability Zones of the NLB instance must also be consistent. |New EIP |
   |Security group ||Select at least one security group for the NLB instance. In addition to the security group you specify, the NLB instance will also automatically attach a managed security group. For a detailed introduction, see [Managed security group](https://docs.byteplus.com/en/docs/clb/NLB-Instance-Overview#.5a6J5YWo57uE).<br><br>The specified security group and the managed security group are jointly used for controlling inbound and outbound traffic of the NLB instance. |Default |
   |Bandwidth Package/Global Bandwidth Package<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Global bandwidth package is a bandwidth package applicable to Global EIPs.</div><br> ||Select whether to add EIP to a Bandwidth Package. After adding, the EIP associated with the NLB instance will share the bandwidth of the specified Bandwidth Package and will no longer be constrained by the bandwidth cap specified for the EIP itself.<br><br>For an EIP bound to an NLB instance to be added to a Bandwidth Package, the following conditions must be met simultaneously:<br><br><br>* **Standard EIP**<br><br>   * The billing method of the EIP is Pay\-as\-you\-go.<br><br>   * Both are in the same region.<br><br>   * Both have the same protection type.<br><br>   * Both have the same ISP.<br><br>   * Both use the same public egress.​<br><br>* **Global EIP**<br><br>   * Both have the same network border group.<br><br>   * Both have the same ISP.<br><br>   * Both use the same public egress.​ |Not selected |
   |**More information** ||||
   |Project ||Select the project to which the NLB instance belongs. After a public NLB instance is added to a project, the EIP created with the instance will also be added to the same project. [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Project-Management) |default |
   |Tag ||A tag consists of a key\-value pair and is used for categorizing and searching resources. [Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Tag-Management)<br><br>Click the add icon, input the tag key and tag value, add tags to the NLB instance.<br><br>The added tags only take effect on the NLB instance, and the EIP associated with the public NLB instance does not inherit the tags. |* Tag key: nlb\-key<br><br>* Tag value: nlb\-test |
   

4. Follow the console guidance to review and confirm the legal terms.

5. Click **Buy now** to complete instance creation.

6. Click **Go to console** to view the newly created instance.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* After the NLB instance is created successfully, you still need to configure the server group and listener for it to function properly. For detailed steps, see [Creating a server group](https://docs.byteplus.com/en/docs/clb/NLB-Creating-a-server-group) and [Adding a listener](https://docs.byteplus.com/en/docs/clb/NLB-Adding-a-listener).

* Allow traffic for communication with NLB in the associated security group or Network ACL. Otherwise, NLB cannot provide services properly. For detailed configuration, see [Configuring the access control](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB).


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateNetworkLoadBalancer](https://docs.byteplus.com/en/docs/clb/CreateNetworkLoadBalancer)
