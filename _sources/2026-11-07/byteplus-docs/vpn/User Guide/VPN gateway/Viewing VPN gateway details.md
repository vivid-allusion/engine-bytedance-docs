---
title: "Viewing VPN gateway details"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Viewing-network-interfaces-of-a-VPN-gateway"
---

This topic describes how to view information related to the VPN gateway, such as its security group and network interfaces.

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After a VPN gateway is successfully created, the system automatically creates the following resources:


* A VPN gateway security group named **vpn\-default** is created within the VPC to which the VPN gateway belongs. This security group allows all inbound and outbound traffic for the VPN gateway by default. It does not support modification, deletion, rule configuration, or network interface association/dissociation. Its lifecycle is tied to the VPN gateway instance.

* Two VPN gateway network interfaces prefixed with **vgw\-**  are automatically created within a subnet of the VPN gateway's VPC. VPN gateway network interfaces provide the VPC for the backend VPN servers. They only support modifying the name and description, and do not support deletion, binding, or unbinding. Their lifecycle is also tied to the VPN gateway instance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. In the VPN gateway list, click the target gateway name.

4. View the required information.

   
   <Tabs>
   <Tab zoneid="m41Um3cqQO" title="View VPN gateway security group">
   <TabTitle>View VPN gateway security group</TabTitle>
   
   1. On the **Basic Information** of VPN gateway, click the VPC link.
   
   2. On the **Basic Information** of VPC, click Copy VPC ID.
   
   3. In the left\-side navigation pane, click **Security Group**.
   
   4. On the security group list page, select **VPC ID** in the search box at the top right, and paste the copied VPC ID into the search bar. You can also search using the security group name or security group ID.
   
   5. The page will display all security groups under that VPC. The security group named **vpn\-default** with the **VPN Gateway Service Security Group \- Non\-operable** tag in the Actions column is the VPN gateway security group.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can select <strong>Name</strong> in the search box and enter <strong>vpn\-default</strong> in the search box. This will search for all VPN gateway security groups under the current account with unchanged default names.   </div>
      
   
   
   </Tab>
   <Tab zoneid="m22dzVTtKY" title="View VPN gateway network interface">
   <TabTitle>View VPN gateway network interface</TabTitle>
   
   1. On the **Basic Information** of VPN gateway, click the VPC link.
   
   2. On the **Basic Information** of VPC, click Copy VPC ID.
   
   3. Click **Network Interface** in the left navigation pane.
   
   4. On the network interface list page, select **VPC ID** in the search box at the top right, and paste the copied VPC ID into the search bar. You can also search using the network interface name, network interface ID, subnet ID, or private IP address.
   
   5. The page will display all network interfaces under that VPC. Interfaces whose names start with **vgw\-**  and have the **VPN Gateway Network Interface \- Non\-operable** tag in the Actions column are the VPN gateway network interfaces.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can select <strong>Name</strong> in the search box and enter <strong>vgw\-</strong> in the search bar. This will search for all VPN gateway network interfaces under the current account that have not had their default names changed.   </div>
      
   
   
   </Tab>
   </Tabs>
   


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [DescribeVpnGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayAttributes): View the information of a specified VPN gateway.

* [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways): Query VPN gateways that meet the specified conditions.
