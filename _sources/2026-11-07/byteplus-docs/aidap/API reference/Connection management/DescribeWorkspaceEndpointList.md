---
title: "DescribeWorkspaceEndpointList"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaceEndpointList"
---

Call the DescribeWorkspaceEndpointList API to query connection endpoint information of multiple workspaces.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

&nbsp;


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceIds |Array of String |Yes |["noble\-heath\-3a48\*\*\*\*","stoic\-chili\-ab80\*\*\*\*"] |List of workspace IDs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 20 workspace IDs can be input.</div><br> |
|Offset |Integer |No |1 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Limit |Integer |No |20 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

&nbsp;


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Integer |20 |The quantity of results that meet the query conditions. |
|WorkspaceEndpoints |Array of [WorkspaceEndpoint](https://docs.byteplus.com/en/docs/330/106702#workspaceendpoint) |Refer to the Sample response. |Connection endpoint list of the workspace. |


<span id="workspaceendpoint"></span>
### WorkspaceEndpoint


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|WorkspaceId |String |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|WorkspaceName |String |TestWorkspace |Name of the workspace. |
|WorkspaceDetailEndpoint |Array of [WorkspaceDetailEndpoint](https://docs.byteplus.com/en/docs/330/106702#workspacedetailendpoint) |Refer to the Sample response. |Details of the workspace's endpoint. |


<span id="workspacedetailendpoint"></span>
### WorkspaceDetailEndpoint


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchId |String |br\-dear\-tern\-753b\*\*\*\* |Branch ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for workspaces using the Supabase engine.</div><br> |
|ComputeId |String |cp\-cute\-foam\-f92a\*\*\*\* |ID of the compute.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">This field returns only in workspaces using the PostgreSQL engine.</div><br> |
|Endpoints |Array of [Endpoint](https://docs.byteplus.com/en/docs/330/106702#endpoint) |Refer to the sample response. |Endpoint list |
|WorkspaceId |String |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |


<span id="endpoint"></span>
### Endpoint


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Addresses |Array of [Address](https://docs.byteplus.com/en/docs/330/106702#address) |Refer to the sample response. |Connection information of the endpoint. |
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
POST /?Action=DescribeWorkspaceEndpointList&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceIds": ["cosy-holly-4f04314i","zappy-fern-17562659"]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260507192341AA64326D5E83620497BE-01ad47",
        "Action": "DescribeWorkspaceEndpointList",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 2,
        "WorkspaceEndpoints": [
            {
                "WorkspaceDetailEndpoint": [
                    {
                        "ComputeId": "cp-cute-foam-f92a****",
                        "Endpoints": [
                            {
                                "Addresses": [
                                    {
                                        "AddressDomain": "cp-cute-foam-f92a****.pg.aidap-global.cn-beijing.volces.com",
                                        "AddressId": "addr-9b7a940a1698184e****",
                                        "AddressPort": 0,
                                        "AddressType": "Public",
                                        "IPAddress": "33.***.***.222",
                                        "IPv6Address": ""
                                    },
                                    {
                                        "AddressDomain": "cp-cute-foam-f92a****.pg.aidap.cn-beijing.inner.ivolces.com",
                                        "AddressId": "addr-9b7a940a1698184e****",
                                        "AddressPort": 0,
                                        "AddressType": "Inner",
                                        "IPAddress": "33.***.***.204",
                                        "IPv6Address": "fdbd:dc41:fe:****:****:c425:260e:88c0\n"
                                    }
                                ],
                                "EndpointId": "ep-ca9c2238f4261e82****",
                                "EndpointName": "ep-ca9c2238f4261e82****",
                                "EndpointType": "Proxy"
                            }
                        ],
                        "WorkspaceId": "cosy-holly-4f04****"
                    }
                ],
                "WorkspaceId": "cosy-holly-4f04****",
                "WorkspaceName": "测试1"
            },
            {
                "WorkspaceDetailEndpoint": [
                    {
                        "BranchId": "br-dear-tern-753b7e5b",
                        "Endpoints": [
                            {
                                "Addresses": [
                                    {
                                        "AddressDomain": "br-dear-tern-753b7e5b.supabase.aidap-global.cn-beijing.volces.com",
                                        "AddressId": "addr-dbf0a7537845720c****",
                                        "AddressPort": 443,
                                        "AddressType": "Public",
                                        "IPAddress": "10.249.148.21",
                                        "IPv6Address": ""
                                    }
                                ],
                                "EndpointId": "ep-dab4b5dff712c9fe****",
                                "EndpointName": "ep-dab4b5dff712c9fe****",
                                "EndpointType": "Proxy"
                            }
                        ],
                        "WorkspaceId": "zappy-fern-1756****"
                    }
                ],
                "WorkspaceId": "zappy-fern-1756****",
                "WorkspaceName": "测试2"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
