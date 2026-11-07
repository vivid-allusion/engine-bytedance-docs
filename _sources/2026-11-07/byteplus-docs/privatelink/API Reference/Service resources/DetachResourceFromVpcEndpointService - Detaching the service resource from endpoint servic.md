---
title: "DetachResourceFromVpcEndpointService - Detaching the service resource from endpoint service"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DetachResourceFromVpcEndpointService"
---

Call the DetachResourceFromVpcEndpointService API to unbind a service resource from the specified VPC endpoint service. For more information and considerations, see [Managing service resources](https://docs.byteplus.com/en/docs/privatelink/Managing-service-resources).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DetachResourceFromVpcEndpointService&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|aRRE8H">必选</span> `Example: DetachResourceFromVpcEndpointService`

Action to execute. Set the value to **DetachResourceFromVpcEndpointService**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|w7x3GB">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ServiceId ** <span data-label="purple">String </span><span data-api-tag="require|EH9_hk">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



**ResourceId ** <span data-label="purple"> String  </span><span data-api-tag="require|AX0Mmh">必选</span> `Example: clb-bp1o94dp5i6ea****`

ID of the service resource.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to obtain the CLB instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/ALB-DescribeLoadBalancers) API to get the ALB instance ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DetachResourceFromVpcEndpointService&Version=2020-04-01&ServiceId=epsvc-2fe630gurkl37k5gfuy33****&ResourceId=clb-bp1o94dp5i6ea**** HTTP/1.1
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
        "Action": "DetachResourceFromVpcEndpointService",
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


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Here, XXX represents the name of the missing parameter.</div><br> |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |UnsupportedOperation.LastResource |The last service resource cannot be deleted. |The last resource cannot be deleted. |
|400 |InvalidServiceResource.InUse |The specified ServiceResource is in use. |Service resource is in use. |
|400 |InvalidEndpointService.InvalidStatus |The specified EndpointService is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |ErrInterfaceNotSupportedResourceType |The Interface does not support the resource type. |The endpoint service API does not support this service resource type. |
|400 |UnsupportedOperation.LastAutoAllocatedResource |The specified Endpoint Service must have at least one automatically allocated resource in one zone. |For the specified VPC endpoint service, there must be at least one auto\-assigned resource in each of its Availability Zones. |
|404 |InvalidServiceResource.NotFound |The specified ServiceResource does not exist. |The specified service resource does not exist. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
