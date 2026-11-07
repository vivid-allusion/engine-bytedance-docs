---
title: "DescribeCenAttachedInstanceAttributes - Querying the details of network instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenAttachedInstanceAttributes"
---

Call DescribeCenAttachedInstanceAttributes API to view the details of the specified network instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCenAttachedInstanceAttributes&groupName=%E7%BD%91%E7%BB%9C%E5%AE%9E%E4%BE%8B&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|SyK6Ae">必选</span> `Example: DescribeCenAttachedInstanceAttributes`

Action to execute. Set the value to DescribeCenAttachedInstanceAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|H2yAdt">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**InstanceType ** <span data-label="purple">string </span><span data-api-tag="require|AqnUdy">必选</span> `Example: VPC`

Type of the network instance. Valid values:


* VPC: Virtual Private Cloud

* DCGW: Direct Connect Gateway



**InstanceRegionId ** <span data-label="purple">string </span><span data-api-tag="require|CYrg27">必选</span> `Example: cn-beijing`

The region where the network instance resides.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|LpOLjG">必选</span> `Example: vpc-2fexiqjlgjif45oxruvso****`

The network instance ID.


* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the ID of a network instance of the "VPC" type.

* You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to query the ID of a network instance of the "DCGW" type.



**CenId ** <span data-label="purple">string </span><span data-api-tag="require|KWfiRg">必选</span> `Example: cen-7qthudw0ll6jmc****`

The CEN instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the CEN instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CenId ** <span data-label="purple">string </span>`Example: cen-7qthudw0ll6jmc****`

The CEN instance ID.



**InstanceId ** <span data-label="purple">string </span>`Example: vpc-2fexiqjlgjif45oxruvso****`

The network instance ID.



**InstanceOwnerId ** <span data-label="purple">string </span>`Example: 210000****`

The ID of the account to which the network instance belongs.



**InstanceType ** <span data-label="purple">string </span>`Example: VPC`

The network instance type.



**InstanceRegionId ** <span data-label="purple">string </span>`Example: cn-beijing`

The region where the network instance resides.



**Status ** <span data-label="purple">string </span>`Example: Available`

Loading status of the network instance.


* Attaching

* Available



**CreationTime ** <span data-label="purple">string </span>`Example: 2021-01-28T14:55:11+08:00`

Loading time of the network instance.



&nbsp;



**CenId ** <span data-label="purple">string </span>`Example: cen-7qthudw0ll6jmc****`

The CEN instance ID.



**InstanceId ** <span data-label="purple">string </span>`Example: vpc-2fexiqjlgjif45oxruvso****`

The network instance ID.



**InstanceOwnerId ** <span data-label="purple">string </span>`Example: 210000****`

The ID of the account to which the network instance belongs.



**InstanceType ** <span data-label="purple">string </span>`Example: VPC`

The network instance type.



**InstanceRegionId ** <span data-label="purple">string </span>`Example: cn-beijing`

The region where the network instance resides.



**Status ** <span data-label="purple">string </span>`Example: Available`

Loading status of the network instance.


* Attaching

* Available



**CreationTime ** <span data-label="purple">string </span>`Example: 2021-01-28T14:55:11+08:00`

Loading time of the network instance.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeCenAttachedInstanceAttributes&Version=2020-04-01&InstanceType=VPC&InstanceRegionId=cn-beijing&InstanceId=vpc-2fexiqjlgjif45oxruvso****&CenId=cen-7qthudw0ll6jmc**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T084227Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202508151654072081611241165231A8",
    "Action": "DescribeCenAttachedInstanceAttributes",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "CenId": "cen-7qthudw0ll6jmc****",
    "InstanceId": "vpc-2fexiqjlgjif45oxruvso****",
    "InstanceOwnerId": "210000****",
    "InstanceType": "VPC",
    "InstanceRegionId": "cn-beijing",
    "Status": "Available",
    "CreationTime": "2021-01-28T14:55:11+08:00"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|404 |InvalidCenAttachedInstance.NotFound |The specified CEN attached instance does not exist. |The specified network instance does not exist. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
