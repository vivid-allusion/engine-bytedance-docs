---
title: "Modifying the associated security group"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Managing-associated-security-groups"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Action description


* When the connection status of the interface endpoint is **Service deletion**, modifying the attached security group is not supported.

* Each endpoint supports associating with a maximum of five security groups and must be associated with at least one.


<span id=".5paw5aKe5YWz6IGU5a6J5YWo57uE"></span>
## Associate new security group

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">PrivateLink health check requests originate from the private CIDR blocks <code>100.64.0.0/10</code> and <code>fd00:64::/32</code>. Ensure the security groups associated with the endpoint network interface allow traffic from <code>100.64.0.0/10</code> and <code>fd00:64::/32</code>. Otherwise, the endpoint network interface service status may become abnormal.</div>



1. Use the service consumer account to log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints).

2. In the top menu bar, select the target project and region.

3. Click the name of the target endpoint and select the **Security Group** tab.

4. Click **Associate new security group** and select the target security group(s).

5. Click **Add** to complete the action.


<span id=".56e76Zmk5YWz6IGU5a6J5YWo57uE"></span>
## Remove associated security group


1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using the service consumer account.

2. In the top menu bar, select the target project and region.

3. Click the name of the target endpoint and select the **Security Group** tab.

4. Click **Remove** on the right side of the target security group to confirm resource information.

5. Click **Remove** to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AttachSecurityGroupToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AttachSecurityGroupToVpcEndpoint)

* [DescribeVpcEndpointSecurityGroups](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointSecurityGroups)

* [DetachSecurityGroupFromVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/DetachSecurityGroupFromVpcEndpoint)
