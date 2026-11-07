---
title: "RemoveZoneFromVpcEndpoint - Removing an availability zone from endpoint"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/RemoveZoneFromVpcEndpoint"
---

Call the RemoveZoneFromVpcEndpoint API to delete the availability zone for a specified endpoint. For action notes and precautions, see [Modifying an availability zone](https://docs.byteplus.com/en/docs/privatelink/Modifying-Availability-Zones).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RemoveZoneFromVpcEndpoint&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|fUuTPg">必选</span> `Example: RemoveZoneFromVpcEndpoint`

Action to execute. Set the value to **RemoveZoneFromVpcEndpoint**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|HJRcXw">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**EndpointId ** <span data-label="purple"> String </span><span data-api-tag="require|5LmzZ4">必选</span> `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.



**ZoneId ** <span data-label="purple">String</span> <span data-api-tag="require|d6qQms">必选</span>`Example: cn-guangzhou-a`

The ID of the availability zone to which the endpoint network interface belongs. For more information, see [Regions and Availability Zones](https://docs.byteplus.com/en/docs/privatelink/Regions-and-Availability-Zones).



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=RemoveZoneFromVpcEndpoint&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ****&ZoneId=cn-guangzhou-a HTTP/1.1
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
        "Action": "RemoveZoneFromVpcEndpoint",
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
|400 |InvalidEndpoint.InvalidStatus |The specified endpoint is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |InvalidEndpoint.ServiceDeleted |The specified endpoint's service has been deleted for the request. |The specified endpoint's associated endpoint service has been deleted, and the request cannot be processed. |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
|404 |InvalidEndpointZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
