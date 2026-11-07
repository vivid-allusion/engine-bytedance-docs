---
title: "Managing service resource"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Managing-service-resources"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Add service resources

<span id="RN1Ytbkb"></span>
## Action notes


* The number of service resources that can be added per Availability Zone for a single endpoint service is 100. If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList) to increase the corresponding quota.

* Currently, CLB, ALB, NLB are supported as service resources for external services.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The ALB, NLB and  service resource support for PrivateLink is in beta stage. For trial requests, contact your account manager.   </div>
   

<span id="pOAgClYr"></span>
## Procedures


1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click the service ID of the target endpoint service, and select the **Service Resource** tab.

4. Click **Add service resources** and check and select the target load balancer instance.

5. Click **Add** to complete the action.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If Access Management (IAM) is enabled on any listener within the Load Balancer instance serving as a service resource, you must add the PrivateLink service's deployment CIDR block <code>100.64.0.0/10</code> and <code>fd00:64::/32</code> to the access control allowlist.</div>


   * <div data-tips="true" data-tips-type="tip">For detailed CLB instance operations, see <a href="https://docs.byteplus.com/en/docs/clb/Managing-access-control-policy-groups#.566h55CGSVDmnaHnm64=">Adding an IP entry to an access control policy group</a>.</div>


   * <div data-tips="true" data-tips-type="tip">For detailed ALB instance operations, see <a href="https://docs.byteplus.com/en/docs/clb/Access-control">Identity and Access Management</a>.</div>


* <div data-tips="true" data-tips-type="tip">After a load balancer instance is added as a service resource to an Endpoint Service, deleting that load balancer instance may cause service access disruptions. If deletion is necessary, it is recommended to first remove the load balancer instance by referring to the procedure for <a href="https://docs.byteplus.com/en/docs/privatelink/Managing-service-resources">removing a service resource</a>.</div>



<span id=".56e76Zmk5pyN5Yqh6LWE5rqQ"></span>
## Remove service resource

<span id="2IevyqQu"></span>
### Action notes


* A service resource that has active endpoint connections cannot be removed. To remove a connection, see [Rejecting an endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection#.5ouS57ud57uI56uv6IqC54K56L-e5o6l).

* Each endpoint service must retain at least one service resource. The last service resource of an endpoint service cannot be removed.

* Removing a service resource will cause the private connection to stop serving the corresponding Availability Zone. Please proceed with caution.


<span id="dtSQZb82"></span>
### Procedures


1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click on the service ID of the target endpoint service, select the **Service Resource** tab, and remove service resources as needed.

   * **Single removal**: Click **Remove** on the right side of the target service resource and confirm the resource information.

   * **Batch move**: Check all service resources to be removed, click **Batch remove**, and confirm the resource information.

4. Click **Remove** to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AttachResourceToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AttachResourceToVpcEndpointService)

* [DescribeVpcEndpointServiceResources](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceResources)

* [DetachResourceFromVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/DetachResourceFromVpcEndpointService)

* [ModifyVpcEndpointZoneConnectionResourceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointZoneConnectionResourceAttributes)


&nbsp;

&nbsp;

&nbsp;
