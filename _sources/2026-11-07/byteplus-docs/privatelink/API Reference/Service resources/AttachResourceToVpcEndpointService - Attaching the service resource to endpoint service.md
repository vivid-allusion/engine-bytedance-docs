---
title: "AttachResourceToVpcEndpointService - Attaching the service resource to endpoint service"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/AttachResourceToVpcEndpointService"
---

Call the AttachResourceToVpcEndpointService API to associate a service resource with a specified endpoint service. For operational instructions and precautions, see [Managing Service Resources](https://docs.byteplus.com/en/docs/privatelink/Managing-service-resources).

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* A single endpoint service supports adding a default maximum of 100 service resources per Availability Zone.

* A single ALB instance can be added to endpoint services a total of 200 times (this count is calculated per Availability Zone).

   For example, if an ALB instance is located in Availability Zone A, B, and C, and Availability Zone A and B are selected when adding this ALB instance to an endpoint service, then the total remaining number of times this ALB instance can be added to endpoint services is: 200 \- 2 = 198.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The ALB service resource support for PrivateLink is in beta stage. For trial requests, contact your account manager.</div>


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AttachResourceToVpcEndpointService&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|1mBkNj">必选</span> `Example: AttachResourceToVpcEndpointService`

Action to execute. Set the value to **AttachResourceToVpcEndpointService**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|r93m_3">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ServiceId ** <span data-label="purple"> String  </span><span data-api-tag="require|d76YQo">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



**ResourceId ** <span data-label="purple"> String  </span><span data-api-tag="require|n-fWa0">必选</span> `Example: clb-bp1o94dp5i6ea****`

ID of the service resource.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to obtain the CLB instance ID.



**ZoneIds.N ** <span data-label="purple"> String </span>`optional` `Example: cn-guangzhou-a`

Availability Zones in which the Application Load Balancer (ALB) provides services.


* This parameter is required when the service resource type is ALB.

* Parameter \-N: Represents the serial number of the availability zone where the resource provides services. The value ranges from 1 to the maximum number of availability zones supported by the service.

* This parameter does not take effect when the service resource type is CLB or RDS for MySQL.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=AttachResourceToVpcEndpointService&Version=2020-04-01&ServiceId=epsvc-2fe630gurkl37k5gfuy33****&ResourceId=clb-bp1o94dp5i6ea**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "AttachResourceToVpcEndpointService",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Here, XXX represents the name of the missing parameter.</div><br> |
|400 |InvalidEndpointService.InvalidStatus |The specified EndpointService is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |InvalidServiceResource.Malformed |The specified ServiceResource is malformed. |The specified ServiceResource parameter format is invalid. |
|400 |ErrPrivateLinkServiceNotSupportedZone |The privatelink service does not support the zone. |The VPC endpoint service does not support adding service resources from this Availability Zone. |
|400 |ErrInterfaceNotSupportedResourceType |The Interface does not support the resource type. |The endpoint service API does not support this service resource type. |
|400 |InvalidServiceResourceType.Malformed |The specified ServiceResourceType is malformed. |The specified ServiceResourceType parameter format is invalid. |
|400 |InvalidServiceResource.ServiceResourceConflict |The specific resource already attached. |The specified service resource is already attached. |
|400 |QuotaExceed.ServiceResourceEachZone |You've reached the limit on the number of service resources in the zone that you can create. |The quota limit for the number of service resources that can be created in a single Availability Zone has been reached. |
|400 |InvalidServiceResourceStatus.IPVersionMismatch |The specified service resource can not support the EndpointService ipAddressVersion that you want. |The current service resource does not support the specified endpoint service IP address type. |
|400 |InvalidLocation.Intercepted |The specified action has been intercepted by location. |The current account does not have operation permissions in the specified region. Please request to be added to the allowlist. |
|400 |InvalidApplicationLoadBalancer.InvalidZoneInfo |The specified Application LoadBalancer zone attributes is invalid. |The specified Availability Zone information for the ALB is invalid. |
|400 |InvalidZoneforALB.conflict |The application load balancer does not support the zone. |The specified ALB instance does not support this Availability Zone. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
