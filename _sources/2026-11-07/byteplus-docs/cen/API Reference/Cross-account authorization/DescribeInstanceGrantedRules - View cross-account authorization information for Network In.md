---
title: "DescribeInstanceGrantedRules - View cross-account authorization information for Network Instances meeting specified criteria"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeInstanceGrantedRules"
---

Call the DescribeInstanceGrantedRules API to query information about network instances under your account that have been authorized to other accounts' Cloud Enterprise Network (CEN) instances.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstanceGrantedRules&groupName=%E8%B7%A8%E8%B4%A6%E5%8F%B7%E6%8E%88%E6%9D%83&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|h8f1Ev">必选</span> `Example value: DescribeInstanceGrantedRules`

Action to execute. Set the value to DescribeInstanceGrantedRules.



Version string Example: 2020\-04\-01

The API version. Value: 2020\-04\-01.



**InstanceId ** <span data-label="purple">string </span>`Optional` `Example: vpc-3rlkeggyn6tc010e****`

The network instance ID.



**InstanceRegionId ** <span data-label="purple">string </span>`optional` `example: cn-beijing`

The region where the network instance resides.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.



**InstanceType ** <span data-label="purple">string </span>`optional` `example: VPC`

Type of the network instance. Valid values:


* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CenGrantRules ** <span data-label="purple">object[] </span>`Example: --`

Cross\-account authorization details of the network instance.


**CenOwnerId ** <span data-label="purple">string </span>`Example: 210000****`

ID of the account to which the authorized CEN instance belongs.



**InstanceType ** <span data-label="purple">string </span>`Example: VPC`

The network instance type.


* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.



**InstanceRegionId ** <span data-label="purple">string </span>`Example value: cn-beijing`

The region where the network instance resides.



**CreationTime ** <span data-label="purple">string </span>`Example: 2019-11-15T09:26:36Z`

Network Instance authorization time.



**InstanceId ** <span data-label="purple">string </span>`example: vpc-3rlkeggyn6tc010e****`

The network instance ID.



**CenId ** <span data-label="purple">string </span>`Example: cen-9gsm1q2yh1prpt****`

ID of the authorized CEN instance.




**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.



**TotalCount ** <span data-label="purple">integer </span>`Example: 1`

Total number of cross\-account authorization records for network instances meeting the specified criteria.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeInstanceGrantedRules&Version=2020-04-01 HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T083748Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815173100052235218090CE6F78",
    "Action": "DescribeInstanceGrantedRules",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "CenGrantRules": [
      {
        "CenOwnerId": "210000****",
        "InstanceType": "VPC",
        "InstanceRegionId": "cn-beijing",
        "CreationTime": "2019-11-15T09:26:36Z",
        "InstanceId": "vpc-3rlkeggyn6tc010e****",
        "CenId": "cen-9gsm1q2yh1prpt****"
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

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
