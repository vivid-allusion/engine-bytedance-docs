---
title: "Changing the NLB instance availability zone"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Changing-NLB-instances-Availability-Zone"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Network Load Balancer (NLB) instances support multi\-availability zone deployment. After creation, you can add or remove the availability zones as needed.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* NLB instance

* When canceling an enabled availability zone, other network resources associated with the NLB instance may be deleted. Proceed with caution. The specific resource changes are shown in the table below.

   
   |Network resources associated with the instance |EIP instance |Private instance |
   |---|---|---|
   |Network interface (ENI) |The private IPv4 and IPv6 addresses of the NLB instance in the availability zone are deallocated, and the instance's ENI is deleted. ||
   |EIP (including Global EIP and standard EIP)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Global EIP is in the invite\-only Beta. For trial requests, please contact your account manager.</div><br> |* The EIP added to the Bandwidth Package is removed from the Bandwidth Package.<br><br>* New EIP along with the NLB instance was deleted.<br><br>* The EIP associated with the NLB instance is automatically disassociated but will not be deleted. Description of the EIP has been modified to empty, and its name has been changed to the instance ID of the EIP. |\-\- |
   |IPv6 Internet bandwidth |* The IPv6 Internet Bandwidth that was part of the Bandwidth Package is removed from the Bandwidth Package.<br><br>* IPv6 Internet Bandwidth has been deleted. |\-\- |
   

* Changing the Availability Zone of a public NLB instance involves adding, deleting, or modifying **Elastic IP Address** (EIP) and **IPv6 Internet Bandwidth**, which may cause changes in internet fees.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click  **··· \> Modify Availability Zone** next to the target NLB instance, select/deselect availability zones as needed.

   * If an IP address in an existing availability zone of the NLB instance is bound to a standard EIP, configure the parameters for the new availability zone by the table below.

      
      |Parameters |Description |Sample |
      |---|---|---|
      |Availability zone and subnet |Check the availability zones supported by the NLB instance. |Availability Zone A, Availability Zone B |
      |Subnet |When providing a private network deployment environment for the NLB instance in a specified Availability Zone. The system will automatically create an ENI associated with the NLB within the subnet. |subnet01 \| 192.168.3.0/24 |
      |IPv4 address |Select the allocation method for the IPv4 address of the NLB instance in the specified availability zone.<br><br><br>* **Auto assign IP**: The system automatically assigns 3 private IPv4 addresses to the network interfaces associated with the NLB, comprising 1 Service IP and 2 Local IPs.<br><br>* **Manual assign IP**: Manually enter an IPv4 address within the subnet range. The entered IPv4 address serves as the Service IP for the NLB\-associated network interface. The system will additionally automatically assign 2 Local IPs. |Auto assign IP |
      |IPv6 address |Select the allocation method for the NLB instance's IPv6 address. Currently, only automatic assignment is supported. The system automatically assigns 3 private IPv6 addresses to the network interfaces associated with the NLB, comprising 1 Service IP and 2 Local IPs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter needs to be configured only when the NLB instance is of the dual\-stack type.</div><br> |Auto assign IP |
      |EIP |Provides internet capabilities for the NLB instance. This parameter is required only when an IP address in an existing availability zone of the NLB instance is bound to an EIP.<br><br><br>* **New EIP**: This EIP is created along with the NLB instance. Defaults to Pay\-by\-data\-transfer, with BGP (multi\-ISP) as the ISP and a maximum bandwidth of 200 Mbps. <br><br>* **Use existing EIP**: The selected EIP must meet the following conditions:<br><br>   * This EIP is not added to Bandwidth Package.<br><br>   * The ISP, billing methods, security protection type, and public egress of the EIPs in different availability zones of the NLB instance must be consistent. |New EIP |
      

   * If an IP address in an existing availability zone of the NLB instance is bound to an Global EIP, configure the parameters for the new availability zone by the table below.

      
      |Parameter |Description |Sample |
      |---|---|---|
      |Network Border Group |Select the Network Border Group (NBG) to which the Global EIP belongs.<br><br><br>* A NBG defines the access scope of a Global EIP. Select a border group close to your primary business for lower latency.<br><br>* Cross\-region transmission fees are incurred when a Global EIP and the associated backend resource are not in the same NBG.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">BytePlus presets optional NBGs based on your region and cloud resource deployment. If you need to use other NBGs, please contact your account manager for consultation.</div><br> |cn\-north\-beijing |
      |ISP |Select the ISP of the Global EIP. |China Mobile |
      |Public egress |Select the public egress of the Global EIP.<br><br><br>* The available public egresses are determined by the NBG to which the Global EIP belongs.<br><br>* To ensure lower internet access latency, it is recommended to select a public egress that is closer to the internet peer outside the cloud. |Tianjin |
      |Availability zone and subnet |Check the availability zones supported by the NLB instance. |Availability Zone A, Availability Zone B |
      |Subnet |When providing a private network deployment environment for the NLB instance in a specified Availability Zone. The system will automatically create an ENI associated with the NLB within the subnet. |subnet01 \| 192.168.3.0/24 |
      |IPv4 address |Select the allocation method for the IPv4 address of the NLB instance in the specified availability zone.<br><br><br>* **Auto assign IP**: The system automatically assigns 3 private IPv4 addresses to the network interfaces associated with the NLB, comprising 1 Service IP and 2 Local IPs.<br><br>* **Manual assign IP**: Manually enter an IPv4 address within the subnet range. The entered IPv4 address serves as the Service IP for the NLB\-associated network interface. The system will additionally automatically assign 2 Local IPs. |Auto assign IP |
      |IPv6 address |Select the allocation method for the NLB instance's IPv6 address. Currently, only automatic assignment is supported. The system automatically assigns 3 private IPv6 addresses to the network interfaces associated with the NLB, comprising 1 Service IP and 2 Local IPs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter needs to be configured only when the NLB instance is of the dual\-stack type.</div><br> |Auto assign IP |
      |EIP |Provides internet capabilities for the NLB instance. This parameter is required only when an IP address in an existing availability zone of the NLB instance is bound to an EIP.<br><br><br>* **New EIP**: This G lobal EIP is created along with the NLB instance. Defaults to Pay\-by\-main\-transfer.<br><br>* **Use existing EIP**: The selected Global EIP must meet the following conditions:<br><br>   * Not added to a Global Bandwidth Package.<br><br>   * The network border group, ISP, billing method, and public egress of the Global IPs in different availability zones of the NLB instance must be consistent. |New EIP |
      

4. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[ModifyNetworkLoadBalancerZones](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerZones)
