---
title: "DetachServerGroups - Removes Load Balancer backend server groups"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DetachServerGroups"
---

Disassociate one or multiple Load Balancer backend server groups from a scaling group. Refer to [Configuring load balancer associated with scaling group](https://docs.byteplus.com/en/docs/as/Configuring-the-load-balancer-associated-with-a-scaling-group) for instructions and precautions.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DetachServerGroups&groupName=%E4%BC%B8%E7%BC%A9%E7%BB%84&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|GFTY1W">必选</span> `Sample value: DetachServerGroups`

The action that you want to perform. Value: DetachServerGroups.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|5InPrZ">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|KN7naL">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

ClientToken is used to ensure the idempotency of the request. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs. Values:

Not more than 64 ASCII characters.



**ServerGroupAttributes.N.Port ** <span data-label="purple">integer[] </span><span data-api-tag="require|xtozrx">必选</span> `Sample value: 80`

The port number of servers in the Load Balancer backend server group.


* Parameter \- N: Indicates the serial number of the server group. Value range: 1 ~ 20.

* Value \- Port: Indicates the port number. Value range: 1 to 65535.

* Separate port numbers of multiple server groups with ampersands (&).



**ServerGroupAttributes.N.Type ** <span data-label="purple">string[] </span>`Optional` `Sample value: CLB`

The type of Load Balancer server groups:


* Parameter \- N: Indicates the serial number of the Load Balancer server group. Value range: 1 ~ 40. Up to 20 server groups of the same type can be selected.

* Parameter \- Type: Indicates the type of the Load Balancer server group.

   * ALB: Application Load Balancer.

   * CLB: Classic Load Balancer.

* Separate multiple server group IDs with ampersands (&).



**ServerGroupAttributes.N.ServerGroupId ** <span data-label="purple">string[] </span><span data-api-tag="require|fsK6nt">必选</span> `Sample value: rsp-12b2z5fnxvhts17q7y2fj****`

The ID of the Load Balancer backend server group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the ID of the backend server group associated with the specified scaling group.


* Parameter \- N: Indicates the serial number of the server group. Value range: 1 ~ 5.

* Parameter \- ServerGroupId: The server group ID.

* Separate multiple server group IDs with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScalingGroupId ** <span data-label="purple">string </span>`String example: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DetachServerGroups&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T094136Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507174143116112230197538F9E",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScalingGroupId": "scg-ybmssdnnhn5pkgyd****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidScalingGroup.InvalidStatus |The specified ScalingGroup is not in the correct status. |The current status of the specified scaling group does not support this operation. |
|400 |MissingParameter.ScalingGroupId |The required parameter ScalingGroupId is not supplied. |The scaling group ID cannot be empty. |
|400 |MissingParameter.ServerGroupAttributes |The specified ServerGroupAttributes is not supplied. |The backend server group attribute cannot be empty. |
|400 |InvalidServerGroupAttributeType |The required parameter ServerGroupAttributeType is invalid. |The specified server group type is invalid. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup [%s] does not exist. |The specified backend server group does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
