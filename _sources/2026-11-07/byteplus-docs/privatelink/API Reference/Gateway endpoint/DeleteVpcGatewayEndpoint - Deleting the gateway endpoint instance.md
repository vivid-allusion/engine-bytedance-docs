---
title: "DeleteVpcGatewayEndpoint - Deleting the gateway endpoint instance"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DeleteVpcGatewayEndpoint"
---

Call the DeleteVpcGatewayEndpoint API to delete the specified gateway endpoint.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteVpcGatewayEndpoint&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|g_NWMv">必选</span> `Example: DeleteVpcGatewayEndpoint`

Action to execute. Set the value to **DeleteVpcGatewayEndpoint**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|tH0DkS">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**EndpointId ** <span data-label="purple"> String  </span><span data-api-tag="require|k_mzbP">必选</span> `Example: gwep-273yuq6q7bgn47fap8squ****`

ID of the gateway endpoint.

You can call the [DescribeVpcGatewayEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpoints) API to get the gateway endpoint ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteVpcGatewayEndpoint&Version=2020-04-01&EndpointId=gwep-273yuq6q7bgn47fap8squ**** HTTP/1.1
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
        "Action": "DeleteVpcGatewayEndpoint",
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
|400 |InvalidGatewayEndpoint.InvalidStatus |The specified GatewayEndpoint is not in the correct status for the request. |The specified gateway endpoint is in a status that cannot respond to this request. |
|404 |InvalidGatewayEp.NotFound |The specified GatewayEndpoint does not exist. |The specified gateway endpoint does not exist. |
