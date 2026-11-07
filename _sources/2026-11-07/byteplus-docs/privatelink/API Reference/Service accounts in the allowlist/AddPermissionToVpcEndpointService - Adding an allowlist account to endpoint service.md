---
title: "AddPermissionToVpcEndpointService - Adding an allowlist account to endpoint service"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/AddPermissionToVpcEndpointService"
---

Call the AddPermissionToVpcEndpointService API to add a allowlist account to the specified endpoint service.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AddPermissionToVpcEndpointService&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|Mas3W7">必选</span> `Example: AddPermissionToVpcEndpointService`

Action to execute. Set the value to **AddPermissionToVpcEndpointService**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|Wl0R-C">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ServiceId ** <span data-label="purple"> String </span><span data-api-tag="require|QkyX07">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



**PermitAccountId ** <span data-label="purple"> String </span><span data-api-tag="require|Y3ftGa">必选</span> `Example: 2100000000`

The ID of the account to be added to the allowlist.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to query the account ID of the endpoint owner.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=AddPermissionToVpcEndpointService&Version=2020-04-01&ServiceId=epsvc-2fe630gurkl37k5gfuy33****&PermitAccountId=2100000000 HTTP/1.1
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
        "Action": "AddPermissionToVpcEndpointService",
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
|400 |InvalidPermitAccountId.Malformed |The specified PermitAccountId is malformed. |The specified PermitAccountId parameter format is invalid. |
|400 |InvalidEndpointService.InvalidStatus |The specified EndpointService is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |InvalidPermissionAccount.Conflict |The specified permission account already exists. |The specified allowlist account already exists. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
