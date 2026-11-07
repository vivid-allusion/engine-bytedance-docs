---
title: "ModifyTransitRouterFlowLogAttributes - Updating attributes of a specified flow log"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterFlowLogAttributes"
---

Call the ModifyTransitRouterFlowLogAttributes API to modify the name, description, or collection period of TR flow log.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterFlowLogAttributes&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Gp65i6">必选</span> `Example: ModifyTransitRouterFlowLogAttributes`

The interface name. The current API name is `ModifyTransitRouterFlowLogAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|XY9XUR">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterFlowLogId ** <span data-label="purple">String </span><span data-api-tag="require|DXZDB9">必选</span> `Example: tr-fl-12sedwag489a****`

ID of the flow log instance.



**TransitRouterFlowLogName ** <span data-label="purple">String </span><span data-api-tag="require|q6e2q1">必选</span> `Example: tr-fl-test`

Name of the flow log.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not provide this parameter or leave it unset, the original name is retained.



**Description ** <span data-label="purple">String </span><span data-api-tag="require|G9mby9">必选</span> `Example: tr-desc`

Description of the flow log.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, the original description is retained.



**AggregationInterval ** <span data-label="purple">Integer </span><span data-api-tag="require|o3fOaz">必选</span> `Example: 1`

The collection period of flow logs. It is also the cycle at which TR aggregates log data and reports data to TLS. Allows 1 and 10, measured in minutes.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyTransitRouterFlowLogAttributes&Version=2020-04-01&TransitRouterFlowLogId=tr-fl-12sedwag489a**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T104914Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250731184918068070002255926271",
        "Action": "ModifyTransitRouterFlowLogAttributes",
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
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.TooLong |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.TooLong |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterFlowLog.AggregationIntervalMalformed |The specified aggregation interval is malformed. |The specified flow log collection period is invalid. |
|400 |InvalidTransitRouterFlowLog.InvalidStatus |The specified Transit Router flow log is not in the correct status for the request. |The specified flow log cannot respond to this request due to its status. |
|404 |InvalidTransitRouterFlowLog.NotFound |The specified Transit Router Flow log does not exist. |The specified flow log does not exist. |
