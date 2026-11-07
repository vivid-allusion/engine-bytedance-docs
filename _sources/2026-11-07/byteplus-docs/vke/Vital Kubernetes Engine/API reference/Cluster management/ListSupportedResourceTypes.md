---
title: "ListSupportedResourceTypes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListSupportedResourceTypes"
---

Query the types of resources for related services supported by VKE.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListSupportedResourceTypes&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListSupportedResourceTypes&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListSupportedResourceTypes |The API name. The name of the current API is `ListSupportedResourceTypes`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [SupportedResourceTypesFilter](https://docs.byteplus.com/en/docs/vke/ListSupportedResourceTypes#supportedresourcetypesfilter) |no |\- |The filter condition for the resource type to be queried. |
|PageNumber |Integer |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Integer |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="supportedresourcetypesfilter"></span>
### SupportedResourceTypesFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|ZoneIds |Array of String |no |["zone\-a"] |The list of availability zone IDs.<br><br>For availability zone IDs (ZoneID), see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones#.5Zyw5Z-f5ZKM5Y-v55So5Yy65YiX6KGo).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not specify this parameter, resource information in all availability zones in the specified region is returned.</div><br> |
|ResourceTypes |Array of String |no |["Ecs","Zone"] |The returned resource type. Two resource types are supported.<br><br><br>* **Ecs**: ECS resources<br><br>* **Zone**: Availability zone resources<br><br>   If you do not specify this parameter, the API returns all resource types supported by VKE. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=ListSupportedResourceTypes&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "ZoneIds": ["cn-beijing-a"],
        "ResourceTypes": ["Ecs","Zone"]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [SupportedResourceTypeResponse](https://docs.byteplus.com/en/docs/vke/ListSupportedResourceTypes#supportedresourcetyperesponse) |\- |The list of supported resource types and specifications. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |10 |The number of data entries displayed per page. |
|TotalCount |Integer |11 |The total number of data entries that meet the conditions. |


<span id="supportedresourcetyperesponse"></span>
### SupportedResourceTypeResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|ResourceScope |String |Zone |The scope to which the resource belongs. Valid values:<br><br><br>* **Zone**: Availability zone<br><br>* **Region**: Region |
|ZoneId |String |cn\-bei\*\*\*\*\*\* |The ID of the specific availability zone supported by the resource. |
|ResourceType |String |Ecs |The resource type. Valid values:<br><br><br>* **Ecs**: ECS resources<br><br>* **Zone**: Availability zone resources |
|ResourceSpecifications |Array of String |["ecs.g1ie.large"] |The list of specifications that correspond to resources.<br><br>Currently, only ECS resources are supported. For ECS instance specifications, see the description of the **InstanceTypeId** parameter of the [DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) API. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "2022051********",
        "Action": "ListSupportedResourceTypes",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "TotalCount": 2,
        "PageNumber": 1,
        "PageSize": 10,
        "Items": [
            {
                "ResourceScope": "Zone",
                "ZoneId": "cn-bei******",
                "ResourceType": "Ecs",
                "ResourceSpecifications": [
                    "ecs.c1.large"
                ]
            },
            {
                "ResourceScope": "Region",
                "ZoneId": "",
                "ResourceType": "Zone",
                "ResourceSpecifications": [
                    "cn-beijing-a"
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details.

&nbsp;
