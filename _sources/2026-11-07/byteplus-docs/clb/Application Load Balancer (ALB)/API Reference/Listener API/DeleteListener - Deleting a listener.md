---
title: "DeleteListener - Deleting a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DeleteListener"
---

Call the DeleteListener API to delete the listener.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Submit up to 5 API requests per second.

* Only listeners whose status is Stopped can be deleted.

* Only listeners that have no non\-default forwarding rules can be deleted.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteListener&groupName=%E7%9B%91%E5%90%AC%E5%99%A8&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ylb3kH">必选</span> `Example: DeleteListener`

Action to execute. Set the value to DeleteListener.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ypSnAK">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ListenerId ** <span data-label="purple">string </span><span data-api-tag="require|U3L3wV">必选</span> `Example: lsn-abc******`

ID of the listener to be deleted.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210816110638****2514606306AF947C`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteListener&Version=2020-04-01&ListenerId=lsn-3ciw6t6efwef46c6rrtdhxu36 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "DeleteListener",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161106****22514606306AF947C"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidListener.InvalidStatus |The specified Listener is not in the correct status for the request. |The specified listener is in a state that cannot respond to this request. |
|400 |InvalidListenerCustomRule.InUse |The specified Listener is being used by custom rules. |The specified listener is currently being used by a custom forwarding rule. |
|400 |OperationFailed.RemoveFromProjectFailed |The request on the specified resource failed due to removing it from the project failed. |The operation request for the resource failed because removing it from the project was unsuccessful. |
|400 |InvalidServerGroup.InvalidStatu |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
