---
title: "GrantInstanceToCen - Authorizing a specified network instance to a cross-account CEN instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/GrantInstanceToCen"
---

Call the GrantInstanceToCen API to grant a network instance under the current account to a CEN instance under a specified account.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=GrantInstanceToCen&groupName=%E8%B7%A8%E8%B4%A6%E5%8F%B7%E6%8E%88%E6%9D%83&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|QD5z3E">必选</span> `Example: GrantInstanceToCen`

Action to execute. Set the value to GrantInstanceToCen.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|GTsosQ">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CenId ** <span data-label="purple">string </span><span data-api-tag="require|yvGK2J">必选</span> `Example: cen-7qthudw0ll6jmc****`

The ID of the CEN instance of the other account.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the CEN instance ID.



**CenOwnerId ** <span data-label="purple">string </span><span data-api-tag="require|qOWKHI">必选</span> `Example: 210000****`

Peer account.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the account ID.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|e8n5ZW">必选</span> `Example: vpc-uf6o8d1dj8sjwxi6o****`

The ID of the network instance to be granted.


* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the ID of a network instance of the "VPC" type.

* You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to query the ID of a network instance of the "DCGW" type.



**InstanceRegionId ** <span data-label="purple">string </span><span data-api-tag="require|qdxyEn">必选</span> `Example: cn-beijing`

The region where the network instance resides.



**InstanceType ** <span data-label="purple">string </span><span data-api-tag="require|rygssB">必选</span> `Example: VPC`

Type of the network instance. Valid values:


* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=GrantInstanceToCen&Version=2020-04-01&CenId=cen-7qthudw0ll6jmc****&CenOwnerId=210000****&InstanceId=vpc-uf6o8d1dj8sjwxi6o****&InstanceRegionId=cn-beijing&InstanceType=VPC HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T083642Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815172922249182104119D59FBD",
    "Action": "GrantInstanceToCen",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidCenOwnerId.Malformed |The specified CenOwnerId is malformed. |The account ID to which the specified CEN instance belongs is invalid. |
|400 |InvalidCenAttachedInstance.Malformed |The specified instance type is malformed. |The specified network instance type is not supported. |
|400 |InvalidCenAttachedInstance.DcgwInvalidStatus |Specified direct connect gateway has been frozen. |The specified Direct Connect Gateway is frozen. |
|400 |LimitExceeded.GrantVpcToCen |You've reached the limit on the number of CENs that a VPC can grant to. |The maximum number of CEN instances that can be authorized for the specified VPC has been reached. |
|400 |LimitExceeded.GrantDCGWToCen |You've reached the limit on the number of CENs that a DCGW can grant to. |The maximum number of CEN instances that can be authorized for the specified Direct Connect Gateway has been reached. |
|404 |InvalidVpcId.NotFound |The specified VPC ID does not exist in this region. |The specified VPC does not exist in the specified region. |
|404 |InvalidDcgwId.NotFound |The specified DCGW ID does not exist in this region. |The specified DC Gateway does not exist in the specified region. |
|404 |InvalidCenRegion.NotFound |The specified region does not exist. |The specified region does not exist. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified CEN instance does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|409 |InvalidGrantInstance.Conflict |The specified instance has been granted. |The specified network instance has already been granted authorization. |
|409 |InvalidGrantInstanceAccount.Conflict |The specified granted account is equal to the login account, please change the account to grant. |The specified account for authorization is the same as the current account. Change another account to authorize. |
|409 |InvalidGrantInstanceAccountType.Conflict |The specified granted account type and login account type is different. |The specified authorized account type is different from the current account type. Please change the account for authorization. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
