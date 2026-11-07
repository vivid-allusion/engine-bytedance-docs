---
title: "DeletePrivateEgressEndpoint - Deleting a private egress endpoint"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DeletePrivateEgressEndpoint"
---

Call the DeletePrivateEgressEndpoint API to delete a private egress endpoint.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

When DNS resolution is enabled for the private network egress, the endpoint cannot be deleted. Call the [DisablePrivateEgressDns](https://docs.byteplus.com/en/docs/privatelink/DisablePrivateEgressDns) API to disable DNS resolution first, then delete the endpoint.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeletePrivateEgressEndpoint&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|2t9XGm">必选</span> `Example: DeletePrivateEgressEndpoint`

The action to perform. Value: **DeletePrivateEgressEndpoint**.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|5xAzZE">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**PrivateEgressEndpointId ** <span data-label="purple"> String </span><span data-api-tag="require|c7aICZ">必选</span> `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the private egress endpoint.

You can call the [DescribePrivateEgressEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribePrivateEgressEndpoints) API to obtain the endpoint ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**AsyncTaskId ** <span data-label="purple"> String </span>`Example: asynctask-13f0odozfrdvk3n6nu41l****`

The ID of the asynchronous task.



**RequestId ** <span data-label="purple"> String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

The request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET /?Action=DeletePrivateEgressEndpoint&Version=2020-04-01&PrivateEgressEndpointId=ep-273yuq6q7bgn47fap8squ****
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeletePrivateEgressEndpoint",
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
