---
title: "AttachServerGroups - Associates Load Balancer backend server groups"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/AttachServerGroups"
---

Associate one or multiple Load Balancer backend server groups with a scaling group. Refer to [Configuring load balancer associated with scaling group](https://docs.byteplus.com/en/docs/as/Configuring-the-load-balancer-associated-with-a-scaling-group) for instructions and precautions.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=AttachServerGroups&groupName=%E4%BC%B8%E7%BC%A9%E7%BB%84&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|OjY3lf">必选</span> `Sample value: AttachServerGroups`

The action that you want to perform. Value: AttachServerGroups.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ihVPaj">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|HqKVTj">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**ServerGroupAttributes.N.ServerGroupId ** <span data-label="purple">string[] </span><span data-api-tag="require|3wwiQr">必选</span> `Sample value: rsp-12b2z5fnxvhts17q7y2fj****`

The ID of the Load Balancer backend server group. You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) operation to query the backend server group ID.


* Parameter \- N: Indicates the serial number of the server group. Value range: 1 ~ 5.

* Parameter \- ServerGroupId: The server group ID.

* Separate multiple server group IDs with ampersands (&).



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

ClientToken is used to ensure the idempotency of the request. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs. Values:


* Not more than 64 ASCII characters.



**ServerGroupAttributes.N.Type ** <span data-label="purple">string[] </span>`Optional` `Sample value: CLB`

The type of Load Balancer server groups:


* Parameter \- N: Indicates the serial number of the Load Balancer server group. Value range: 1 ~ 40. Up to 20 server groups of the same type can be selected.

* Parameter \- Type: Indicates the type of the Load Balancer server group.

   * ALB: Application Load Balancer.

   * CLB: Classic Load Balancer.

* Separate multiple server group IDs with ampersands (&).

* If this parameter is passed in but no value is specified, CLB is selected by default.



**ServerGroupAttributes.N.Port ** <span data-label="purple">integer[] </span><span data-api-tag="require|L9rJFR">必选</span> `Sample value: 80`

The port number of servers in the Load Balancer backend server group.


* Parameter \- N: Indicates the serial number of the server group. Value range: 1 ~ 5.

* Parameter \- Port: Indicates the port number. Value range: 1 to 65535.

* Separate port numbers of multiple server groups with ampersands (&).



**ServerGroupAttributes.N.Weight ** <span data-label="purple">integer[] </span><span data-api-tag="require|j1AIWr">必选</span> `Sample value: 20`

The weight of the server in the Load Balancer backend server group.


* Parameter \- N: Indicates the serial number of the server group. Value range: 1 ~ 5.

* Parameter \- Weight: Indicates the weight. Value range: 0 ~ 100.

* Separate multiple server group weights with &.

* If this parameter is not passed in, this indicates not associating with Load Balancer now.



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
GET /?Action=AttachServerGroups&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T094337Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202405071743461880532151539D7BBA",
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
|400 |LimitExceeded.ServerGroups |You've reached the limit on the number of ServerGroups that you can attach. |The maximum number of backend server groups that can be associated is reached. |
|400 |LimitExceeded.LoadBalancers |You've reached the limit on the number of LoadBalancer, max [%d]. |The maximum number of Load Balancer instances is reached. |
|400 |MissingParameter.ServerGroupId |The required parameter ServerGroupId is not supplied. |The backend server group ID cannot be empty. |
|400 |InvalidServerGroupPort.Malformed |The specified ServerGroup Port is malformed. |The specified backend server group port is invalid. |
|400 |InvalidServerGroupWeight.Malformed |The specified ServerGroup Weight is malformed. |The specified backend server weight is invalid. |
|400 |LimitExceeded.LoadBalancerServerGroups |You've reached the limit on the number of [%s] LoadBalancer ServerGroups, max [%d]. |The maximum number of Load Balancer backend server groups is reached. |
|400 |InvalidResources.VPCMismatch |The specified ServerGroups And Subnets are in different VPC. |The specified backend server group and scaling group subnet are not in the same VPC. |
|400 |MissingParameter.ServerGroupAttributes |The specified ServerGroupAttributes is not supplied. |The backend server group attribute cannot be empty. |
|400 |InvalidServerGroupAttributeType |The required parameter ServerGroupAttributeType is invalid. |The specified server group type is invalid. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup [%s] does not exist. |The specified backend server group does not exist. |
|404 |InvalidServerGroupId.NotFound |The specified ServerGroupId [%s] does not exist in LoadBalancer. |The specified server group ID does not exist. |
|409 |InvalidServerGroupId.Conflict |The specified ServerGroupId [%s] Port [%d] already existed. |The specified backend server group port already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
