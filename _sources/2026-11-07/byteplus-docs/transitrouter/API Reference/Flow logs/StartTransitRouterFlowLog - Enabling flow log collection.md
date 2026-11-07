---
title: "StartTransitRouterFlowLog - Enabling flow log collection"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/StartTransitRouterFlowLog"
---

Call the StartTransitRouterFlowLog API to enable Transit Router (TR) flow logs.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=StartTransitRouterFlowLog&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|DnSqnY">必选</span> `Example: StartTransitRouterFlowLog`

The interface name. The current API name is `StartTransitRouterFlowLog`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|bdE4m4">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterFlowLogId** <span data-label="purple">String</span> <span data-api-tag="require|Ez9pJp">必选</span> `Example: tr-fl-13jjg43etfv****`

ID of the flow log instance.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=StartTransitRouterFlowLog&Version=2020-04-01&TransitRouterFlowLogId=tr-fl-13jjg43etfv**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T105150Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250731185154228042030227330C6F",
        "Action": "StartTransitRouterFlowLog",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterFlowLog.InvalidStatus |The specified Transit Router flow log is not in the correct status for the request. |The specified flow log cannot respond to this request due to its status. |
|404 |InvalidTransitRouterFlowLog.NotFound |The specified Transit Router Flow log does not exist. |The specified flow log does not exist. |
