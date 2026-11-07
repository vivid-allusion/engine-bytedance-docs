---
title: "DeleteCustomizedCfg - Deleting a custom configuration"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DeleteCustomizedCfg"
---

Call the DeleteCustomizedCfg API to delete a custom configuration.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* A custom configuration that is associated with a listener must be disassociated before it can be deleted.

* Submit up to 10 API requests per second.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteCustomizedCfg&groupName=%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|KQJ0V3">必选</span> `Example: DeleteCustomizedCfg`

Action to execute. Set the value to DeleteCustomizedCfg.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|B5q706">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CustomizedCfgId ** <span data-label="purple">string </span><span data-api-tag="require|cxVzfK">必选</span> `Example: ccfg-3cj44nv0jhhxc6c6rrtet***`

ID of the custom configuration to be deleted.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteCustomizedCfg&CustomizedCfgId=ccfg-3lk5o0tulupdswet340b****&ProjectName=default&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "1665bc5d-d6fd-451d-b37b-b2e9c5f6****",
        "Action": "DeleteCustomizedCfg",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "1665bc5d-d6fd-451d-b37b-b2e9c5f6****"
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
|400 |InvalidCustomizedCfg.InvalidStatus |The specified CustomizedCfg is not in the correct status for the request. |The specified custom configuration is in a state that cannot respond to the request. |
|400 |OperationFailed.RemoveFromProjectFailed |The request on the specified resource failed due to removing it from the project failed. |The operation request for the resource failed because removing it from the project was unsuccessful. |
|400 |InvalidCustomizedCfgListener.InUse |The specified CustomizedCfg is being used by listeners. |The specified custom configuration is in use by the listener. |
|404 |InvalidCustomizedCfg.NotFound |The specified CustomizedCfg does not exist. |The specified custom configuration does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
