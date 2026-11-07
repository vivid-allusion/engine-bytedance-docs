---
title: "DescribeHealthCheckLogTopicAttributes - Querying the health check log topic information"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeHealthCheckLogTopicAttributes"
---

Call the DescribeHealthCheckLogTopicAttributes API to query the CLB instance information associated with the specified log topic.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeHealthCheckLogTopicAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|7iH5ry">必选</span> `Example: DescribeHealthCheckLogTopicAttributes`

Action to execute. Set the value to **DescribeHealthCheckLogTopicAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|OzdSdt">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**LogTopicId ** <span data-label="purple">String </span><span data-api-tag="require|tlCmyg">必选</span> `Example: 74936ae4-bbd6-41de-a0d2-ed156203****`

The ID of the log topic.

You can call the [DescribeTopics](https://docs.byteplus.com/en/docs/tls/api-describetopics) API to query the log topic ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**LoadBalancerIds ** <span data-label="purple">String[] </span>`Example: ["clb-3tihaugk2y3vj0wt****","clb-2fe6fszjgeznk5oxruv0u****"]`

Eligible CLB ID information.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeHealthCheckLogTopicAttributes&Version=2020-04-01&LogTopicId=74936ae4-bbd6-41de-a0d2-ed156203****
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeHealthCheckLogTopicAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "LoadBalancerIds": [
            "clb-3tihaugk2y3vj0wt****",
            "clb-2fe6fszjgeznk5oxruv0u****"
        ],
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidTopic.LoadBalancerMismatch |The specified Topic and LoadBalancer are not matched. |The specified Topic is not associated with CLB. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LogTopicId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as LogTopicId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
