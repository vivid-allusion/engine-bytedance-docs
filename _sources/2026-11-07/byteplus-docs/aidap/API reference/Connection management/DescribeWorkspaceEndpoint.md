---
title: "DescribeWorkspaceEndpoint"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaceEndpoint"
---

Call the DescribeWorkspaceEndpoint API to query connection endpoint information of a workspace.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|ComputeId |String |No |cp\-brave\-hills\-ad69\*\*\*\* |ID of the compute.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required if the workspace uses the PostgreSQL engine.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is optional if the workspace uses the Supabase engine.</div><br> |
|BranchId |String |No |br\-bloom\-duck\-61c7\*\*\*\* |Branch ID.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the workspace uses the PostgreSQL engine, this parameter is optional.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the workspace uses the Supabase engine, this parameter is required.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchId |String |br\-bloom\-duck\-61c7\*\*\*\* |Branch ID.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter does not return in every request and depends on the engine type used by the workspace.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the workspace uses the PostgreSQL engine, this parameter will not be returned.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the workspace uses Supabase engine, this parameter is returned.</div><br> |
|ComputeId |String |cp\-brave\-hills\-ad69\*\*\*\* |ID of the compute. |
|Endpoints |Array of [Endpoint](https://docs.byteplus.com/en/docs/330/84443#endpoint) |Refer to the sample response. |Connection endpoint information of the workspace. |
|WorkspaceId |String |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |


<span id="endpoint"></span>
### Endpoint


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Addresses |Array of [Address](https://docs.byteplus.com/en/docs/330/84443#address) |Refer to the sample response. |Connection information of the endpoint. |
|EndpointId |String |ep\-15d73b055d662534\*\*\*\* |Connection endpoint ID. |
|EndpointName |String |ep\-15d73b055d662534\*\*\*\* |The name of the connection endpoint. |
|EndpointType |String |Proxy |Endpoint type. Values:<br><br><br>* `Proxy`: shared endpoint.<br><br>* `Dashboard`: exclusive endpoint. |


<span id="address"></span>
### Address


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AddressDomain |String |cp\-fiery\-tide\-1958\*\*\*\*.pg.aidap\-global.cn\-beijing.volces.com |Domain name associated with the endpoint. |
|AddressId |String |addr\-ffac9dc170a3c6fa\*\*\*\* |Address ID. |
|AddressPort |Integer |80 |The IPv4/IPv6 address port associated with the endpoint. |
|AddressType |String |Public |Address type associated with the endpoint. Values:<br><br><br>* `Public`: public network address.<br><br>* `Private`: private network address. |
|IPAddress |String |192.\*\*\*.\*\*\*.4 |Private network IPv4 address associated with the endpoint.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">This field returns empty if the endpoint's associated address type is public network.</div><br> |
|IPv6Address |String |2406:\*\*\*\*:\*\*\*\*:\*\*\*\*:\*\*\*\*:\*\*\*\*:\*\*\*\*:b38c |Private network IPv6 address associated with the endpoint. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeWorkspaceEndpoint&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "alive-palm-e2bb****",
    "ComputeId": "cp-fiery-tide-1958****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025120214090314FE8B90F8A57F780B41-d5d80f",
        "Action": "DescribeWorkspaceEndpoint",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "ComputeId": "cp-brave-rocks-8608****",
        "Endpoints": [
            {
                "Addresses": [
                    {
                        "AddressDomain": ".supabase.aidap.cn-beijing.ivolces.com",
                        "AddressId": "addr-72a12a66ed71ddebb136",
                        "AddressPort": 80,
                        "AddressType": "Private",
                        "IPAddress": "192.***.***.241",
                        "IPv6Address": ""
                    }
                ],
                "EndpointId": "ep-c2bff5cdda9ecb8b****",
                "EndpointName": "ep-c2bff5cdda9ecb8b****",
                "EndpointType": "DashBoard"
            }
        ],
        "WorkspaceId": "alive-palm-e2bb****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
