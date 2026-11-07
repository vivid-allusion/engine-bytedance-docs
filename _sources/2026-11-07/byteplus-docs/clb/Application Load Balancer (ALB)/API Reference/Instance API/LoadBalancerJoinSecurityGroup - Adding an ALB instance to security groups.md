---
title: "LoadBalancerJoinSecurityGroup - Adding an ALB instance to security groups"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/LoadBalancerJoinSecurityGroup"
---

Call the LoadBalancerJoinSecurityGroup API to add the ALB instance to the security group.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|2unClS">必选</span> `Example: LoadBalancerJoinSecurityGroup`

Action to execute. Set the value to LoadBalancerJoinSecurityGroup.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|w0euYk">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**SecurityGroupIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|K0I0bv">必选</span> `Example: sg-xh1jksdn8***`

ID of the security group to be associated.


* Parameter \- N: Represents the serial number of the security group ID.

* The maximum number of custom security groups that can be bound to an instance is 4.



**LoadBalancerId ** <span data-label="purple">string </span><span data-api-tag="require|U1aeey">必选</span> `Example: alb-bp1b6c719dfa08ex****`

ALB instance ID.



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
GET /?Action=LoadBalancerJoinSecurityGroup&Version=2020-04-01&SecurityGroupIds.1=sg-xh1jksdn8***&LoadBalancerId=alb-bp1b6c719dfa08ex**** HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20260312T023301Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260312/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "2026031210330818916118713758FFC8",
    "Action": "LoadBalancerJoinSecurityGroup",
    "Version": "2020-04-01",
    "Service": "alb",
    "Region": "cn-beijing"
  },
  "Result": {
    "RequestId": "20210811152539010225146063030****"
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
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|400 |InvalidSecurityGroup.NotFound |The specified SecurityGroup does not exist. |The specified security group does not exist. |
|400 |OperationDenied.SecurityGroupManagedByService |The request on the specified SecurityGroup is denied due to the SecurityGroup has been managed by service. |Because the security group is managed by a service, operation requests on this security group are rejected. |
|400 |LimitExceed.SecurityGroupId |You've reached the limit on the number of security groups you can associate with the ALB. |The maximum number of security groups that can be bound to a single ALB instance has been reached. |
|400 |InvalidSecurityGroupId.Duplicated |The specified SecurityGroupId is duplicated. |The specified SecurityGroupId is duplicated. |
|400 |InvalidSecurityGroup.InvalidStatus |The specified SecurityGroup is not in the correct status for the request. |The specified security group is in a state that cannot respond to this request. |
|400 |OperationDenied.AclAndSecurityGroupConflict |The request on the specified LoadBalancer is denied due to acls and security groups cannot be used at the same time. |The operation request for this ALB instance is rejected because access control and security groups cannot be used simultaneously. |
|400 |OperationFailed.QueryVpc |The request on the specified resource failed due to the query on VPC failed. |The request to operate on this resource failed because the VPC request failed. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified ALB instance does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
