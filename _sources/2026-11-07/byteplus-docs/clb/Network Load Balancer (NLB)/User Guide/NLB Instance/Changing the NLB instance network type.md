---
title: "Changing the NLB instance network type"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Changing-Network-Load-Balancer-instance-network-type"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The Network Load Balancer (NLB) supports two network types: Internet and VPC. You can flexibly modify the network type based on your business requirements.

<span id="HCpFHu25"></span>
## Modify IPv4 network type

<span id="JMXVgAin"></span>
### Instructions


* **Convert IPv4 from Internet to VPC:** 

   * If the EIP has already been added to a bandwidth package, the system will automatically remove it.

   * The EIP is automatically detached from the NLB instance.

   * If EIP is applied for when the NLB instance is created, it will be automatically released.

   * The NLB domain name resolution changes from a public IPv4 address to a private IP address.

* **Convert IPv4 from VPC to Internet**:

   * You need to bind an EIP address to the service IP of each Availability Zone of the NLB instance, and the EIP type must be the same across different Availability Zones.

      * If the NLB instance uses standard EIPs in different availability zones, their line type, billing method, security protection type, and public egress must be consistent.

      * If the NLB instance uses Global standard EIPs in different availability zones, their line type, billing method, security protection type, and public egress must be consistent.

   * The NLB domain name resolution for the instance has been updated from a private IPv4 address to EIP.


<span id="lMgl4GtP"></span>
### Procedure


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click Convert on the right side of the target NLB instance.

   * **VPC to Internet**: Click **IPv4 will be converted to internet**. To configure the related parameters, see the table below.

      
      |Parameter |Description |Example |
      |---|---|---|
      |EIP type |Select the EIP type. Standard EIP and Global EIP are supported. [Learn more](https://docs.byteplus.com/en/docs/eip/What-is-EIP?lang=en)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Global EIP is in the invite\-only Beta. For trial requests, please contact your account manager.</div><br> |Standard EIP |
      |Network Border Group |Select the NBG to which the Global EIP belongs. This parameter is required only for Global EIPs.<br><br><br>* A network border group defines the access scope of a Global EIP. Select a border group close to your primary business for lower latency.<br><br>* Cross\-region transmission fees are incurred when a Global EIP and the associated backend resource are not in the same network border group.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">BytePlus presets optional NBGs based on your region and cloud resource deployment. If you need to use other NBGs, please contact your account manager for consultation.</div><br> |cn\-north\-beijing |
      |ISP |Select the ISP of the Global EIP. This parameter is required only for Global EIPs. |China Mobile |
      |Public egress |Select the public egress of the Global EIP. This parameter is required only for Global EIPs.<br><br><br>* The available public egresses are determined by the Network Border Group (NBG) to which the Global EIP belongs.<br><br>* To ensure lower internet access latency, it is recommended to select a public egress that is closer to the internet peer outside the cloud. |Tianjin |
      |Availability zone |Displays the availability zones supported by the NLB instance. |Availability zone A |
      |Subnet |Displays the subnet where the NLB instance is deployed. |subnet01 |
      |IPv4 address |Displays the service IP address of the NLB network interface. |192.168.0.15 |
      |EIP |Provides internet capabilities for the NLB instance.<br><br><br>* **New EIP:**  Create an EIP and bind it to the service IP address of the NLB instance.<br><br>   * **Standard EIP**: Defaults to Pay\-by\-data\-transfer, with BGP (multi\-ISP) as the ISP and a maximum bandwidth of 200 Mbps.<br><br>   * **Global ** **EIP**: Defaults to Pay\-by\-main\-transfer.<br><br>* **Use existing EIP**: The selected EIP must meet the following conditions:<br><br>   * This EIP is not added to Bandwidth Package.<br><br>   * EIP type must be the same across different Availability Zones.<br><br>      * If standard EIPs are used, the line type, billing type, security protection type, and public egress of the EIPs in different Availability Zones of the NLB instance must also be consistent.<br><br>      * If Global EIPs are used, the network boundary group, line type, billing type, and public egress of the EIPs in different Availability Zones of the NLB instance must also be consistent. |Newly purchased EIP |
      

   * **Internet to VPC**: Click **IPv4 will be converted to private network**.

4. Click **Confirmed** to complete the action.


<span id=".5Y-Y5pu0SVB2Nue9kee7nOexu-Weiw=="></span>
## Modify IPv6 network type

<span id="jgqsc6hR"></span>
### Prerequisites

Ensure that the VPC associated with the NLB instance has an IPv6 Gateway. If none exists, see [Creating an IPv6 gateway instance](https://docs.byteplus.com/en/docs/IPv6/Creating_an_IPv6_gateway_instance).

<span id="E9NPxzHi"></span>
### Instructions


* Convert IPv6 from Internet to VPC:

   * The system automatically deletes Internet bandwidth for the NLB instance's IPv6 address.

   * If the IPv6 internet bandwidth of the NLB instance has been added to a bandwidth package, the system will first remove it from the bandwidth package and then automatically delete the IPv6 internet bandwidth.

* Convert IPv6 from VPC to Internet: The system automatically provisions Internet bandwidth for the NLB instance's IPv6 address.


<span id="tfkBVJj2"></span>
### Procedures


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click Convert on the right side of the target NLB instance.

   * Internet to VPC: Click **IPv6 will be converted to private network** and confirm the resource information.

   * VPC to Internet: Click **IPv6 will be converted to internet**, and follow the console instructions to review and confirm the associated agreements.

4. Click **Confirmed** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[ModifyNetworkLoadBalancerNetworkType](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerNetworkType)
