---
title: "Configuring Cloud Service access"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Route-entries-for-access-to-cloud-services-01"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Introduction​

Cloud Service refers to cloud products that provide services using the BytePlus's CIDR blocks `100.64.0.0/10` or `fd00:64::/32`, such as Torch Object Storage (TOS) and CloudFS, among others.

By configuring cloud service access routes, IDC data centers under the cloud can access cloud services.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_300bff0dab782116866b73bafe108c0a.png) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When cross\-VPC Elastic Compute Service (ECS) instances or data center servers are used as backend servers for Classic Load Balancer (CLB), you need to configure return routes using this feature.</div>


<div data-tips="true" data-tips-type="default">The <a href="https://docs.byteplus.com/en/docs/clb/Cross-VPC-server-overview">CLB's cross\-VPC backend feature</a> is in Beta stage. If you need a trial, please contact your account manager.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The address and region information of the target cloud service has been obtained.

* The Direct Connect Gateway associated with the on\-premises IDC has been attached to the Cloud Enterprise Network (CEN) instance. If not loaded, see [Attaching a network instance](https://docs.byteplus.com/en/docs/cen/Network-instances-01).

* A VPC instance within the cloud service region has been attached to the CEN instance. If not loaded, see [Attaching a network instance](https://docs.byteplus.com/en/docs/cen/Network-instances-01).

* To configure access for an IPv6\-type cloud service, ensure that the IPv6 capabilities for VPC, Direct Connect, and CEN have been activated, and that an IPv6 CIDR block has been allocated to the VPC.

* Virtual interfaces of Direct Connect are not configured with local peer IP addresses belonging to `100.64.0.0/10` or `fd00:64::/32` CIDR blocks; otherwise, interoperability between the local data center and the Cloud Service cannot be established.

* The address in use by the local data center does not belong to the `100.64.0.0/10` or `fd00:64::/32` CIDR blocks; otherwise, interoperability between the local data center and the Cloud Service cannot be achieved.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click the target CEN instance name.

4. On the **Cloud Services** tab, click **Configure Cloud Service Access**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Service region |Select the region of the cloud service. |China (Beijing) |
   |The VPC of Cloud as a service belongs |Select the VPC instance loaded to the CEN.<br><br><br>* When configuring access to cloud service, any VPC can be selected.<br><br>* When configuring the back\-to\-source route for the CLB, select the VPC to which the CLB instance belongs. |VPC\-1 |
   |Service address |Enter the IP address or CIDR block of the cloud service, which can be an IPv4 or IPv6 address.<br><br><br>* The IPv4 address must fall within the `100.64.0.0/10` CIDR block. Mask range: 10 \- 32.<br><br>* The IPv6 address must fall within the `fd00:64::/32` CIDR block.<br><br>* The return addresses for different Region CLBs vary. For details, see [Cross-VPC backend server overview](https://docs.byteplus.com/en/docs/clb/Cross-VPC-server-overview). |100.XX.XX.105/32 |
   |Publish scope​​ |Select the service scope for accessing the cloud service.<br><br><br>* **Default publish scope**: By default, routes are published to all Direct Connect Gateways in the same region as the cloud service.<br><br>* **Custom publish scope**:<br><br>   * Advertise to VPC instances or Direct Connect gateways in a different Region from the cloud service as needed.<br><br>   * Optionally publish to VPC instances in the same region as the cloud service, as needed **.** <br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The feature that publishes cloud service routes to VPC instances within the same region is in Beta. If you need to use it, please contact your account manager.   </div><br>    |Default service scope |
   |Posting instances |Select the published target instance.<br><br><br>* When the publishing scope is set to **Default publish scope**, it is fixed as the Region where the cloud service is located.<br><br>* When the publish scope is set to **Custom publish scope**, select the direct connect gateway or virtual private cloud loaded to the Cloud Enterprise Network instance under the target region from the dropdown. |China (Beijing) |
   

6. Click **Configure** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateCenServiceRouteEntry](https://docs.byteplus.com/en/docs/cen/CreateCenServiceRouteEntry)

&nbsp;
