---
title: "DescribeGrantRulesToCen - Viewing the cross-account authorization information of qualified CEN instances"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeGrantRulesToCen"
---

Call the DescribeGrantRulesToCen API to query information about the authorization of network instances from other accounts accepted by the Cloud Enterprise Network (CEN) instance of the current account.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeGrantRulesToCen&groupName=%E8%B7%A8%E8%B4%A6%E5%8F%B7%E6%8E%88%E6%9D%83&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|h6Z0Bw">必选</span> `Example: DescribeGrantRulesToCen`

Action to execute. Set the value to DescribeGrantRulesToCen.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|wxh6Bv">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**InstanceOwnerId ** <span data-label="purple">string </span>`optional` `Example: 210000****`

The ID of the account to which the network instance belongs.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

Page number of the list. Default: 1.



**InstanceRegionId ** <span data-label="purple">string </span>`optional` `Example: cn-beijing`

The region where the network instance resides.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.



**InstanceType ** <span data-label="purple">string </span>`optional` `Example: VPC`

Type of the network instance. Valid values:


* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.



**CenId ** <span data-label="purple">string </span>`optional` `Example: cen-uf6o8d1dj8sjwxi6o****`

The CEN instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CenGrantRules ** <span data-label="purple">object[] </span>`Example: -`

Details of cross\-account authorization.


**CenId ** <span data-label="purple">string </span>`Example: cen-9gsm1q2yh1prpt****`

ID of the authorized CEN instance.



**InstanceId ** <span data-label="purple">string </span>`Example: vpc-3rlkeggyn6tc010e****`

Network instance ID.



**InstanceType ** <span data-label="purple">string </span>`Example: VPC`

The network instance type.


* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.



**InstanceOwnerId ** <span data-label="purple">string </span>`Example: 210000****`

The ID of the account to which the network instance belongs.



**InstanceRegionId ** <span data-label="purple">string </span>`Example: cn-beijing`

The region where the network instance resides.



**CreationTime ** <span data-label="purple">string </span>`Example: 2019-11-15T09:26:36Z`

Network Instance authorization time.




**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

Page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.



**TotalCount ** <span data-label="purple">integer </span>`Example: 1`

Total number of cross\-account authorization information entries for the CEN instance that meet the specified conditions.



&nbsp;



**CenGrantRules ** <span data-label="purple">object[] </span>`Example: -`

Details of cross\-account authorization.


**CenId ** <span data-label="purple">string </span>`Example: cen-9gsm1q2yh1prpt****`

ID of the authorized CEN instance.



**InstanceId ** <span data-label="purple">string </span>`Example: vpc-3rlkeggyn6tc010e****`

Network instance ID.



**InstanceType ** <span data-label="purple">string </span>`Example: VPC`

The network instance type.


* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.



**InstanceOwnerId ** <span data-label="purple">string </span>`Example: 210000****`

The ID of the account to which the network instance belongs.



**InstanceRegionId ** <span data-label="purple">string </span>`Example: cn-beijing`

The region where the network instance resides.



**CreationTime ** <span data-label="purple">string </span>`Example: 2019-11-15T09:26:36Z`

Network Instance authorization time.




**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

Page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.



**TotalCount ** <span data-label="purple">integer </span>`Example: 1`

Total number of cross\-account authorization information entries for the CEN instance that meet the specified conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeGrantRulesToCen&Version=2020-04-01 HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T083722Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "2025081517300225521701707263DB16",
    "Action": "DescribeGrantRulesToCen",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "CenGrantRules": [
      {
        "CenId": "cen-9gsm1q2yh1prpt****",
        "InstanceId": "vpc-3rlkeggyn6tc010e****",
        "InstanceType": "VPC",
        "InstanceOwnerId": "210000****",
        "InstanceRegionId": "cn-beijing",
        "CreationTime": "2019-11-15T09:26:36Z"
      }
    ],
    "PageNumber": 1,
    "PageSize": 20,
    "TotalCount": 1
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
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
