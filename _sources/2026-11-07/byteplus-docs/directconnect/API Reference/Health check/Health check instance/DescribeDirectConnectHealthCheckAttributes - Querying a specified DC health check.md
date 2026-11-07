---
title: "DescribeDirectConnectHealthCheckAttributes - Querying a specified DC health check"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectHealthCheckAttributes"
---

Call the DescribeDirectConnectHealthCheckAttributes API to query the details of a specified health check instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectHealthCheckAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|59AAcA">必选</span>`Example: DescribeDirectConnectHealthCheckAttributes`

The interface name. The current API name is `DescribeDirectConnectHealthCheckAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|QjyOko">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectHealthCheckId ** <span data-label="purple">String </span><span data-api-tag="require|4E006S">必选</span> `Example: dhc-2752hz4tek****`

The ID of the health check instance.

You can call [DescribeDirectConnectHealthChecks](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectHealthChecks) to query the health check instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectHealthCheckId ** <span data-label="purple">String </span>`Example: dhc-2752hz4tek****`

The ID of the health check instance.



**DirectConnectHealthCheckName ** <span data-label="purple">String </span>`Example: dchc-01`

Name of the health check instance.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-01`

The Virtual Private Cloud (VPC) where the health check instance is located.



**SubnetId ** <span data-label="purple">String </span>`Example: subnet-01`

The subnet where the target monitoring source IP is located.



**Description ** <span data-label="purple">String </span>`Example: This is a healthcheck`

The description of the health check instance.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the health check instance.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**DirectConnectHealthCheckProbeIds ** <span data-label="purple">String[] </span>`Example: dhp-2sx****`

List of probes included in the health check instance.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-12-07T15:57:22+08:00`

The time when the health check instance is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-12-07T15:57:22+08:00`

The time when the health check instance is updated.



**AccountId ** <span data-label="purple">String </span>`Example: 20******57`

The ID of the account to which the resource belongs.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeDirectConnectHealthCheckAttributes&Version=2020-04-01&DirectConnectHealthCheckId=dhc-2752hz4tek**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDirectConnectHealthCheckAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "AccountId": "20******57",
        "CreationTime": "2021-12-07T15:57:22+08:00",
        "Description": "This is a healthcheck",
        "DirectConnectHealthCheckId": "dhc-2752hz4tek****",
        "DirectConnectHealthCheckName": "dchc-01",
        "DirectConnectHealthCheckProbeIds": [
            "dhp-2sx****"
        ],
        "Status": "Available",
        "SubnetId": "subnet-01",
        "UpdateTime": "2021-12-07T15:57:22+08:00",
        "VpcId": "vpc-01"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidDirectConnectHealthCheck.NotFound |The specified direct connect health check does not exist. |The specified health check does not exist. |
