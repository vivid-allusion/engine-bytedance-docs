---
title: "CreateEndpointPublicAddress"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/CreateEndpointPublicAddress"
---

Call the CreateEndpointPublicAddress API to enable public network access for the specified endpoint of the workspace.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This API can only be used to operate the workspace using the Supabase engine.

* The public network connection of the workspace using the Supabase engine supports shared address and dedicated address. When initiating the request, if valid values are passed for the request parameters EndpointId and EipId, the dedicated public network address is enabled; if no values or invalid values are passed for EndpointId and EipId, the shared public network address is enabled.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-bloom\-duck\-61c7\*\*\*\* |Branch ID. |
|EndpointId |String |No |ep\-15d73b055d662534\*\*\*\* |Connection endpoint ID. |
|EipId |String |No |eip\-3jhjud2zgy1og3pncmeh7\*\*\*\* |ID of the EIP. You can query the basic information of the EIP using the [DescribeEipAddressAttributes](https://docs.byteplus.com/en/docs/eip/DescribeEipAddresses) API. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=CreateEndpointPublicAddress&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-bloom-duck-61c7****",
    "EndpointId": "ep-15d73b055d662534****",
    "EipId": "eip-3jhjud2zgy1og3pncmeh7****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateEndpointPublicAddress",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
