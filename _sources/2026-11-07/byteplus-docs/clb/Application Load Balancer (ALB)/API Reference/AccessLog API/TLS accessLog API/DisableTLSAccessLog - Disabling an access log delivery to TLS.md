---
title: "DisableTLSAccessLog - Disabling an access log delivery to TLS"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DisableTLSAccessLog"
---

Call the DisableTLSAccessLog API to disable TLS access log delivery and unbind the Topic from the ALB.

## Instructions

Submit up to 5 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisableTLSAccessLog&serviceCode=alb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DisableTLSAccessLog`

The interface name. The current API name is `DisableTLSAccessLog`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.

**LoadBalancerId ** String必选 `Example: alb-bp1b6c719dfa08ex****`

ALB instance ID.

## Response parameters

**RequestId ** String`Example: 20210811152539010225146063030****`

Request ID.

## Request examples

```JSON
GET /?Action=DisableTLSAccessLog&Version=2020-04-01&LoadBalancerId=alb-bp1b6c719dfa08ex**** HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202108171522560****524314701095A5A",
        "Action": "DisableTLSAccessLog",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-test"
    },
    "Result": {
        "RequestId": "202108171522560****524314701095A5A"
    }
}
```

## Error codes

If the response body contains an Error field, it indicates the API request failed. This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Error-codes).

|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |OperationDenied.AccountArrears |The request on the specified resource is denied due to the account being in arrears status. |The request to operate on this resource was rejected because the account is in an overdue payment state. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|404 |InvalidTlsAccessLog.NotFound |The specified TlsAccessLog does not exist. Please confirm the TlsAccessLog of LoadBalancer is enabled. |The TlsAccessLog does not exist. Please confirm that the TlsAccessLog delivery feature has been enabled for the ALB instance. |
