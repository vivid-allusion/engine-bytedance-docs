---
title: "Managing resources in a Bandwidth Package"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Managing_resources_in_a_Bandwidth_Package"
---

This section describes the management actions supported for Elastic IP Address (EIP) and IPv6 Internet bandwidth resources within a Bandwidth Package.


|Cloud resource |[Add to/Remove from Bandwidth Package](https://docs.byteplus.com/en/docs/50/86818#9HNP4wLa) |[Associate/disassociate cloud resources](https://docs.byteplus.com/en/docs/50/86818#A84ss8u8) |Other action paths |
|---|---|---|---|
|Elastic IP Address |Support |Support |* [Elastic IP Address > Associating a cloud resource](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP)<br><br>* [Elastic IP Address > Disassociating a cloud resource](https://docs.byteplus.com/en/docs/eip/Disassociating-Cloud-Resource-from-an-EIP)<br><br>* [Adding to a Bandwidth Package](https://docs.byteplus.com/en/docs/eip/Adding-an-EIP-to-a-Bandwidth-Package)<br><br>* [Removing from a Bandwidth Package](https://docs.byteplus.com/en/docs/eip/Removing-an-EIP-address-from-a-bandwidth-package) |
|IPv6 Internet bandwidth |Support |Not support |* [Add to a Bandwidth Package](https://docs.byteplus.com/en/docs/IPv6/Manage_Shared_Bandwidth_Package#.5Yqg5YWl5YWx5Lqr5bim5a695YyF)<br><br>* [Remove from a Bandwidth Package](https://docs.byteplus.com/en/docs/IPv6/Manage_Shared_Bandwidth_Package#.56e75Ye65YWx5Lqr5bim5a695YyF) |


<span id="9HNP4wLa"></span>
## Add to/Remove from a Bandwidth Package

For conditions that must be met to add an EIP or IPv6 Internet bandwidth to a Bandwidth Package, see [Limits](https://docs.byteplus.com/en/docs/bandwidthpackage/Limits#.5Yqg5YWl5YWx5Lqr5bim5a695YyF6ZmQ5Yi2).

<span id="kO0SUe9g"></span>
### Procedure


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select the region and project of your target Bandwidth Package.

3. In the Bandwidth Package list, click **Manage EIP** to the right of the target Bandwidth Package.

4. Steps to add an EIP or IPv6 Internet bandwidth are as follows:

   
   <Tabs>
   <Tab zoneid="FpRYCZCe" title="Add EIP">
   <TabTitle>Add EIP</TabTitle>
   
   Click **Add EIP** and select **Apply for an EIP and add** or **Select from existing EIPs**.
   
   
   * Apply for an EIP and add: Select the **Number** to apply for, then click **Add** at the bottom right. After successful application, the system automatically adds new EIPs to this Bandwidth Package instance.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The number of EIPs you can apply for is subject to quota limits. For details, see <a href="https://docs.byteplus.com/en/docs/eip/Limits#.6YWN6aKd6ZmQ5Yi2">EIP Quota limits</a>.   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">EIPs applied by the above method belong to the project of the Bandwidth Package instance by default.   </div>
      
   
   * Select from existing EIPs: Check one or more EIP instances and click **Add** at the bottom right.
   
   
   </Tab>
   <Tab zoneid="C8RcSM4d" title="Remove EIP">
   <TabTitle>Remove EIP</TabTitle>
   
   1. Click **Move out** to the right of the target EIP. A dialog box appears to confirm your request.
   
   2. Click **Remove** to complete the action.
   
   
   </Tab>
   <Tab zoneid="BcfgGe18mO" title="Add IPv6 Internet bandwidth">
   <TabTitle>Add IPv6 Internet bandwidth</TabTitle>
   
   1. Click **Add EIP** and select the ** Add IPv6 addresses with enabled internet bandwidth** tab.
   
   2. Select one or more target IPv6 Internet bandwidths as needed.
   
   3. Click **Add** to complete the action.
   
   
   </Tab>
   <Tab zoneid="bb9x2sUvYP" title="Remove IPv6 Internet bandwidth">
   <TabTitle>Remove IPv6 Internet bandwidth</TabTitle>
   
   1. Click **Move out** to the right of the target IPv6 Internet bandwidth. A dialog box appears to confirm your request.
   
   2. Click **Remove** to complete the action.
   
   
   </Tab>
   </Tabs>
   


<span id="VmyBdyau"></span>
### Results


|Action |Results |
|---|---|
|Add to Bandwidth Package |* The EIP or IPv6 Internet bandwidth invalidates its original maximum bandwidth, and shares the bandwidth of the Bandwidth Package.<br><br>* The billing items (bandwidth fee and data transfer fee) for EIP or IPv6 Internet bandwidth become ineffective. Only the IP config fee remains effective. For more billing items, see [Pay-as-you-go for EIP](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go) and [Pay-as-you-go for IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go).<br><br>* In the EIP or IPv6 Internet bandwidth list, you can view the Bandwidth Package to which the resource belongs and the maximum bandwidth of the package. |
|Removed from Bandwidth Package |* The maximum bandwidth of the EIP or IPv6 Internet bandwidth is restored.<br><br>* The billing items (bandwidth fee and data transfer fee) for the EIP or IPv6 Internet bandwidth are restored, and billing starts immediately.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After removal, EIPs applied via the Bandwidth Package console are metered by <a href="https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#.5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5">Pay\-by\-data\-transfer</a>, with the maximum bandwidth of 100 Mbps.   </div><br>    |


<span id="A84ss8u8"></span>
## Associate/disassociate cloud resources

<span id="ju9tjOnK"></span>
### Instructions


* When a Public Classic Load Balancer (CLB) is converted to a Private CLB, the EIP is automatically disassociated.

* To disassociate an EIP that is associated with an Internet NAT gateway, you must access [the Internet NAT Gateway console](https://console.byteplus.com/nat/nats). For details, see [Internet NAT Gateway > Binding or unbinding an EIP](https://docs.byteplus.com/en/docs/natgateway/Associating-or-disassociating-an-EIP#.6Kej57uR5YWs572RSVA=)


<span id="N28ohdyp"></span>
### Procedure


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select the region and project of your target Bandwidth Package.

3. In the Bandwidth Package list, click **Manage EIP** to the right of the target Bandwidth Package.

4. Click **Associate** or **Disassociate** to the right of the target EIP, then select the target cloud resource instance.

5. Click **Associate/Disassociate** to complete the action.


<span id="sdL4ujLP"></span>
## Related documents


* [AddBandwidthPackageIp](https://docs.byteplus.com/en/docs/bandwidthpackage/AddBandwidthPackageIp): Add an EIP or IPv6 Internet bandwidth to a Bandwidth Package.

* [RemoveBandwidthPackageIp](https://docs.byteplus.com/en/docs/bandwidthpackage/RemoveBandwidthPackageIp): Remove the EIP/the IPv6 Internet bandwidth from the Bandwidth Package.

* [AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress): Associate an EIP with a cloud resource.

* [DisassociateEipAddress](https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress): Disassociate the EIP from its attached cloud resource.
