---
title: "DeleteScalingPolicy - Deletes a scaling rule"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DeleteScalingPolicy"
---

Delete a scaling rule. This operation is irreversible. If you want to use a scaling rule later, we recommend that you [disable the scaling rule](https://docs.byteplus.com/en/docs/as/Disabling-a-scaling-policy) instead of deleting it.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteScalingPolicy&groupName=%E4%BC%B8%E7%BC%A9%E8%A7%84%E5%88%99&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|YHyWhk">必选</span> `Sample value: DeleteScalingPolicy`

The operation that you want to perform. Value: DeleteScalingPolicy.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|OW5Za1">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingPolicyId ** <span data-label="purple">string </span><span data-api-tag="require|qdVXqF">必选</span> `Sample value: sp-ybmvamf8uql8j1fl****`

The ID of the scaling rule. You can call [DescribeScalingPolicies](https://docs.byteplus.com/en/docs/as/DescribeScalingPolicies) to query the scaling rule ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScalingPolicyId ** <span data-label="purple">string </span>`Sample value: sp-ybmvamf8uql8j1fl****`

The ID of the scaling rule.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteScalingPolicy&ScalingPolicyId=sp-ybmvamf8uql8j1fl****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T111320Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507191331071208101031D6149C",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScalingPolicyId": "sp-ybmvamf8uql8j1fl****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.ScalingPolicyId |The required parameter ScalingPolicyId is not supplied. |The scaling rule ID cannot be empty. |
|404 |InvalidScalingPolicyId.NotFound |The specified ScalingPolicyId does not exist. |The specified scaling rule ID does not exist. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
