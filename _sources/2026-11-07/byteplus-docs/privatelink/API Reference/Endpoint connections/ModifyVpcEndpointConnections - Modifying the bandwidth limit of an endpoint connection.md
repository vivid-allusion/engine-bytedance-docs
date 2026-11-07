---
title: "ModifyVpcEndpointConnections - Modifying the bandwidth limit of an endpoint connection"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointConnections"
---

Call the ModifyVpcEndpointConnections API to modify the bandwidth limit of an endpoint connection

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyVpcEndpointConnections&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: ModifyVpcEndpointConnections`

Action to execute. Set the value to **ModifyVpcEndpointConnections**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**EndpointId ** String必选 `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.

**ServiceId ** String必选 `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.

**Bps ** Integer`optional` `Example: 1000`

The bandwidth cap for endpoint connections ranges from 100 to 20,000 Mbps.

## Response parameters

**RequestId ** String`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

## Request examples

```json
GET /?Action=ModifyVpcEndpointConnections&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ****&ServiceId=epsvc-2fe630gurkl37k5gfuy33****&Bps=1000 HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyVpcEndpointConnections",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br>> **tip**<br><br><br>> Here, XXX represents the name of the missing parameter.<br> |
|400 |InvalidBps.Malformed |The specified Bps is malformed. |The specified Bps parameter format is invalid. |
|400 |InvalidCps.Malformed |The specified Cps is malformed. |The specified Cps parameter format is invalid. |
|400 |InvalidEndpoint.InvalidStatus |The specified endpoint is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |InvalidEndpoint.ServiceMisMatch |The specified endpoint and service don't match. |The specified endpoint and endpoint service do not match. |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
