---
title: "VerifyVpcEndpointServicePrivateDNS - Verifying the private DNS for an endpoint service"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/VerifyVpcEndpointServicePrivateDNS"
---

Call the VerifyVpcEndpointServicePrivateDNS API to verify the DNS name of a specified endpoint service. Only public domain names are supported for verification. For operation instructions and precautions, see [Modifying/Verifying a private DNS name](https://docs.byteplus.com/en/docs/privatelink/Modifying-Verifying-private-DNS-names).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=VerifyVpcEndpointServicePrivateDNS&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|lTXBfg">必选</span> `Example: VerifyVpcEndpointServicePrivateDNS`

Action to execute. Set the value to **VerifyVpcEndpointServicePrivateDNS**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|S0QL3h">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ServiceId ** <span data-label="purple"> String </span><span data-api-tag="require|jnjRgg">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=VerifyVpcEndpointServicePrivateDNS&Version=2020-04-01&ServiceId=epsvc-2fe630gurkl37k5gfuy33**** HTTP/1.1
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
        "Action": "VerifyVpcEndpointServicePrivateDNS",
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
|400 |InvalidPrivateDNS.UnsupportedOperation |The request on the specified PrivateDNS is denied due to the PrivateDNS is disabled. |The request was rejected because the Private DNS feature is not enabled. |
|400 |InvalidPrivateDNSName.InvalidStatus |The specified PrivateDNSName is not in the correct status for the request. |The specified Private DNS name is in a state that cannot respond to this request. |
|400 |InvalidPrivateDNSType.UnsupportedOperation |The operation of verifying private dns is not supported by the private type dns. |Private DNS does not support the private DNS verification feature. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|409 |InvalidPrivateDNSName.Conflict |The specified PrivateDNSName already exists. |The specified Private DNS name already exists. |
|409 |InvalidVerifiedPrivateDNSName.Conflict |The specified PrivateDNSName already verified. |The specified private DNS name has been successfully verified. |
|409 |InvalidVerifyingPrivateDNSName.Conflict |The specified PrivateDNSName is verifying. |The specified private DNS name is being verified. |
