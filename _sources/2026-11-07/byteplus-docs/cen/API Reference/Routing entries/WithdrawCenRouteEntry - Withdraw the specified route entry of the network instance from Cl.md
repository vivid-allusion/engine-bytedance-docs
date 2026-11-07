---
title: "WithdrawCenRouteEntry - Withdraw the specified route entry of the network instance from Cloud Enterprise Network (CEN)"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/WithdrawCenRouteEntry"
---

Call the WithdrawCenRouteEntry API to withdraw the specified route entry of the network instance from Cloud Enterprise Network (CEN).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=WithdrawCenRouteEntry&groupName=%E8%B7%AF%E7%94%B1%E4%BF%A1%E6%81%AF&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|p1weBt">必选</span> `Example: WithdrawCenRouteEntry`

The operation to perform, value: WithdrawCenRouteEntry.



Version string Example: 2020\-04\-01

The API version. Value: 2020\-04\-01.



**InstanceType ** <span data-label="purple">string </span><span data-api-tag="require|p3jtYE">必选</span> `Example value: VPC`

Network instance type.


* VPC: Virtual Private Cloud.



**InstanceRegionId ** <span data-label="purple">string </span><span data-api-tag="require|wbA1w6">必选</span> `Example: cn-beijing`

Region.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|1GOb6D">必选</span> `Example: vpc-vtbnbb04qw3k2hgi12cv****`

Network instance ID.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) interface to query the ID of the “VPC” type network instance.



**DestinationCidrBlock ** <span data-label="purple">string </span><span data-api-tag="require|y7yqD9">必选</span> `Example value: 10.XX.XX.0/24`

Destination CIDR block.



**CenId ** <span data-label="purple">string </span><span data-api-tag="require|HFBQsF">必选</span> `Example value: cen-2nim00ybaylts7trquyzt****`

The CEN instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) interface to query the CEN instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=WithdrawCenRouteEntry&Version=2020-04-01&InstanceType=VPC&InstanceRegionId=cn-beijing&InstanceId=vpc-vtbnbb04qw3k2hgi12cv****&DestinationCidrBlock=10.XX.XX.0%2F24&CenId=cen-2nim00ybaylts7trquyzt**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T084525Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815170029107085114148F8E4D8",
    "Action": "WithdrawCenRouteEntry",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidCenAttachedInstance.Malformed |The specified instance type is malformed. |The specified network instance type is not supported. |
|400 |UnsupportedOperation |The specified CEN route entry does not support being withdrawn. |The specified route entry does not support withdrawal from the Cloud Enterprise Network (CEN). |
|400 |InvalidInstance.Isolated |The specified instance is abnormal and has been isolated. |The specified resource is isolated due to an exception. Retry later. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified Cloud Enterprise Network (CEN) instance does not exist. |
|404 |InvalidCenAttachedInstance.NotFound |The specified CEN attached instance does not exist. |The specified network instance does not exist. |
|404 |InvalidCenRouteEntry.NotFound |The specified CEN route entry does not exist. |The specified route does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified Cloud Enterprise Network (CEN) instance is in a state that cannot respond to this request. Try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
