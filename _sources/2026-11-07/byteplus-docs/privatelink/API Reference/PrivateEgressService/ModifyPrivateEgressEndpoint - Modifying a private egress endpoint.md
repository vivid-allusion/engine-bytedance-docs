---
title: "ModifyPrivateEgressEndpoint - Modifying a private egress endpoint"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/ModifyPrivateEgressEndpoint"
---

Call the ModifyPrivateEgressEndpoint API to specify the CIDR blocks for Claw instances to access your enterprise service, and to enable or disable private access for the private egress endpoint.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

After private access is enabled for the private egress endpoint, DNS queries from Claw instances are forwarded to the BytePlus DNS servers (100.96.0.2 and 100.96.0.3). To specify an external DNS server, call the [EnablePrivateEgressDns](https://docs.byteplus.com/en/docs/privatelink/EnablePrivateEgressDns) API.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyPrivateEgressEndpoint&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|UpzStK">必选</span> `Example: ModifyPrivateEgressEndpoint`

The action to perform. Value: **ModifyPrivateEgressEndpoint**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|gAUZnk">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**PrivateEgressEndpointId ** <span data-label="purple">String </span><span data-api-tag="require|xEEwk8">必选</span> `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the private egress endpoint.

You can call the [DescribePrivateEgressEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribePrivateEgressEndpoints) API to obtain the endpoint ID.



**DestinationCidrs ** <span data-label="purple">String </span><span data-api-tag="require|y6QQaA">必选</span> `Example: 10.0.0.0/24`

The CIDR blocks of enterprise services that can be accessed by the Claw instance.


* N represents the sequence number of a CIDR block. Valid values: 1\-50.

* Separate multiple CIDR blocks with ampersands (&).

* The CIDR block must not fall within the following ranges: 100.64.0.0/10, 224.0.0.0/4, 127.0.0.0/8, 0.0.0.0/0, 240.0.0.0/4, 192.18.0.0/15, 33.0.0.0/8, 66.0.0.0/8, 9.0.0.0/8, and 169.254.0.0/16.



**AppPrivateAccessEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Describe whether the private access to apps feature is enabled.


* true

* false



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**AsyncTaskId ** <span data-label="purple">String </span>`Example: asynctask-13f0odozfrdvk3n6nu41l****`

The ID of the asynchronous task.



**RequestId ** <span data-label="purple">String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

The request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=ModifyPrivateEgressEndpoint&Version=2020-04-01&SpaceId=csi-yeihfm47b48gethr****&PrivateEgressEndpointId=ep-273yuq6q7bgn47fap8squ****&DestinationCidrs=10.0.0.0/24
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyPrivateEgressEndpoint",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "AsyncTaskId": "asynctask-13f0odozfrdvk3n6nu41l****",
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no service\-specific error codes. For more details, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).
