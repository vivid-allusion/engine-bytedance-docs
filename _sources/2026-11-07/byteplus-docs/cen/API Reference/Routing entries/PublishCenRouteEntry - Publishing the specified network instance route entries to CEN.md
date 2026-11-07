---
title: "PublishCenRouteEntry - Publishing the specified network instance route entries to CEN"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/PublishCenRouteEntry"
---

Call the PublishCenRouteEntry API to publish specified network instance route entries to Cloud Enterprise Network (CEN).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=PublishCenRouteEntry&groupName=%E8%B7%AF%E7%94%B1%E4%BF%A1%E6%81%AF&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|uDFDUs">必选</span> `Example: PublishCenRouteEntry`

Action to execute. Set the value to PublishCenRouteEntry.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|8gzg63">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**InstanceType ** <span data-label="purple">string </span><span data-api-tag="require|T13gLP">必选</span> `Example: VPC`

Network instance type.


* VPC: Virtual Private Cloud.



**InstanceRegionId ** <span data-label="purple">string </span><span data-api-tag="require|6Rt9mP">必选</span> `Example: cn-beijing`

Region.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|LBaYde">必选</span> `Example: vpc-vtbnbb04qw3k2hgi12cv****`

Network instance ID.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the ID of a network instance of the "VPC" type.



**DestinationCidrBlock ** <span data-label="purple">string </span><span data-api-tag="require|AQTwbX">必选</span> `Example: 10.XX.XX.0/24`

Destination CIDR.



**CenId ** <span data-label="purple">string </span><span data-api-tag="require|cRyk9p">必选</span> `Example: cen-2nim00ybaylts7trquyzt****`

The CEN instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the CEN instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=PublishCenRouteEntry&Version=2020-04-01&InstanceType=VPC&InstanceRegionId=cn-beijing&InstanceId=vpc-vtbnbb04qw3k2hgi12cv****&DestinationCidrBlock=10.XX.XX.0%2F24&CenId=cen-2nim00ybaylts7trquyzt**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T084440Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815165909228191084084579C78",
    "Action": "PublishCenRouteEntry",
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
|400 |InvalidCenAttachedInstance.Malformed |The specified instance type is malformed. |The specified network instance type is not supported. |
|400 |InvalidCenRouteEntry.Existed |The specified route entry has been published to CEN. |The specified route has already been published to the CEN route table and cannot be published repeatedly. |
|400 |UnsupportedOperation |The specified route entry does not support being published. |The specified route does not support being published to the CEN route table. |
|400 |QuotaExceeded.CenRouteEntry |You've reached the number of route entries can be published to CEN. |The quota limit for the number of CEN route entries has been reached. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidInstance.Isolated |The specified instance is abnormal and has been isolated. |The specified resource has been isolated due to an exception. Please try again later. |
|400 |InvalidInstanceRoutes.Rejected |The cen has reject routes from instance. |CEN has rejected receiving routes from this instance, please try again later. |
|400 |InvalidServiceRoute.Malformed |The specified destination cidr block is malformed. |The destination CIDR block of the specified cloud service route entry is not within 100.64.0.0/10 or fd00:64::/32. |
|403 |Forbidden.PublishIPv6CenRouteEntry |You are not authorized to publish IPv6 route entry to CEN. |No permission to publish the specified IPv6 route. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified CEN instance does not exist. |
|404 |InvalidCenAttachedInstance.NotFound |The specified CEN attached instance does not exist. |The specified network instance does not exist. |
|404 |InvaildRouteEntry.NotFound |The specified route entry does not exist in the instance. |The specified route cannot be found in the network instance. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
