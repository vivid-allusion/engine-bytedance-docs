---
title: "EnableVpcEndpointConnection - Accepting an endpoint connection"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection"
---

Call the EnableVpcEndpointConnection API to accept the specified endpoint connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=EnableVpcEndpointConnection&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|aN5fRb">必选</span> `Example: EnableVpcEndpointConnection`

Action to execute. Set the value to **EnableVpcEndpointConnection**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|FhDDxp">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**EndpointId ** <span data-label="purple">String </span><span data-api-tag="require|whp7RQ">必选</span> `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.



**ServiceId ** <span data-label="purple">String </span><span data-api-tag="require|RmfcVu">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



**ResourcesAllocate.N.ZoneId ** <span data-label="purple">String </span>`optional` `Example: cn-guangzhou-a`

Specify the availability zone of the endpoint.



**ResourcesAllocate.N.ResourceId ** <span data-label="purple">String </span>`optional` `Example: clb-bp1o94dp5i6ea***`

Specify the service resource for the endpoint connection.


* Parameter \-N: Indicates the serial number of the service resource. The valid range is 1 to 20. Separate multiple service resources with ampersands (&).

* If this parameter is not specified, a service resource is randomly assigned to the endpoint connection by default.



**ResourcesAllocate.N.CrossRegionResourceZoneIds.N ** <span data-label="purple">String </span>`optional` `Example: cn-guangzhou-b`

Specify the availability zone of the cross\-region service resource.


* The first N: Endpoint availability zone.

* The second N: The availability zone serial number of the cross\-region service resource.


One endpoint availability zone can correspond to multiple service resource availability zones, and multiple endpoint availability zones can also share a single service resource availability zone.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=EnableVpcEndpointConnection&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ****&ServiceId=epsvc-2fe630gurkl37k5gfuy33**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "Action": "EnableVpcEndpointConnection",
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


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request is missing a required parameter. Ensure that your request includes all required parameters, such as XXX.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Here, XXX represents the name of the missing parameter.</div><br> |
|400 |UnsupportedOperation.ConnectionStatus |The connection status does not support operation. |The current connection state does not support this operation. |
|400 |InvalidEndpoint.ServiceMisMatch |The specified endpoint and service don't match. |The specified endpoint and endpoint service do not match. |
|400 |InvalidEndpoint.InvalidStatus |The specified endpoint is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |ErrEndpointServiceNotSupportedZone |The specified endpoint service does not support the zone. |The specified endpoint service does not support the current Availability Zone. |
|400 |InvalidResource.Disorder |The specified resource index orders are malformed. |The serial number of the specified resource entry is invalid. |
|400 |InvalidResource.ZoneMisMatch |The specified resource and available zone don't match. |The specified Availability Zone and resource do not match. |
|400 |InvalidZone.Conflict |The specified zone is duplicated. |Duplicate Availability Zones specified. |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |InvalidEndpointIpAddressVersions.EndpointServiceMisMatch |The IpAddressVersions of associated EndpointService and Endpoint mismatch. |The IP address type of the endpoint does not match the associated endpoint service. |
|400 |InvalidPrivateDNS.UnsupportedOperation |The request on the specified PrivateDNS is denied due to the PrivateDNS is disabled. |The request was rejected because the Private DNS feature is not enabled. |
|400 |InvalidPrivateDNSName.Conflict |The PrivateDNSName of associated EndpointService and Endpoint mismatch. |The DNS name of the endpoint does not match the associated endpoint service. |
|400 |UnsupportedOperation.ReplaceResourceConflict |The specified endpoint connection has not completed the service resource replacement. Please disconnect the service resource first. |The specified endpoint connection has not yet completed the service resource replacement. Please disconnect the service resource first. |
|400 |InvalidEndpointZone.InvalidStatus |The specified EndpointZone is not in the correct status for the request. |The specified endpoint availability zone is in a status that cannot respond to this request. |
|404 |InvalidEndpointZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
