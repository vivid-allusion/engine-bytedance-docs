---
title: "UpdateObjectGroup"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/UpdateObjectGroup"
---

Update an object group.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

An object group can contain up to 100 cloud products, with at most 1,000 resources specified for each cloud product. An object group can contain up to 5,000 cloud product resources.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=UpdateObjectGroup&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateObjectGroup&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateObjectGroup |The name of the API. The API name is `UpdateObjectGroup`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Id |String |No |1764547228734\*\*\*\*\*\* |Object group ID. |
|Name |String |No |object_group_demo |Object group name.<br><br><br>* It can contain only Chinese characters, letters, digits, and underscores (`_`).<br><br>* It must be 1 to 64 characters in length. |
|Objects |Array of [Object](https://docs.byteplus.com/en/docs/39/29852#object) |No |*  |A list of cloud product resources to be grouped. The maximum list length is 100. |


<span id="object"></span>
### Object


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Id |String |No |1764547228934\*\*\*\*\*\* |Object group ID. |
|Namespace |String |No |VCM_ECS |The namespace to which the cloud product belongs in Cloud Monitor. For details, see the **Namespace** field on the [Cloud Monitor metric query](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) page for each cloud product. |
|Dimensions |JSON Map |No |*  |Cloud product resource IDs. |
|Region |String |No |cn\-beijing |Availability zone of the cloud products under the current resource collection.<br><br><br>* If `Type` is `enum`, you can specify only one Region.<br><br>* If `Type` is `dynamic`, you can specify multiple Regions separated by commas (`,`). |
|Type |String |No |enum |Resource collection type. Available types:<br><br><br>* **enum**: Manually select resources. If it is enum, `Dimensions` cannot be empty.<br><br>* **dynamic**: Select resources by resource name, project, and tag. If it is dynamic, `DimensionConditions` cannot be empty. |
|DimensionConditions |Object of [DimensionConditions](https://docs.byteplus.com/en/docs/39/29852#dimensionconditions) |No |*  |Dimension configuration. |


<span id="dimensions"></span>
### Dimensions


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|key |String |Yes |ResourceID |The key of the metric to retrieve. |
|value |Array of String |Yes |i\-ydvpb\*\*\* |The value corresponding to the metric key. |


<span id="dimensionconditions"></span>
### DimensionConditions


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Type |String |No |meta |Dimensions type. Available types:<br><br><br>* **project**: Select alert objects by project.<br><br>* **tag**: Select alert objects by tag.<br><br>* **meta**: Select alert objects by resource name. |
|TagCondition |Object of [TagCondition](https://docs.byteplus.com/en/docs/39/29852#tagcondition) |No |*  |Tag condition for selecting alert objects. This field is required if `Type` is `tag`. |
|MetaCondition |Object of [MetaCondition](https://docs.byteplus.com/en/docs/39/29852#metacondition) |No |*  |Resource name condition for selecting alert objects. This field is required if `Type` is `meta`. |
|ProjectCondition |Object of [ProjectCondition](https://docs.byteplus.com/en/docs/39/29852#projectcondition) |No |*  |Project condition for selecting alert objects. This field is required if `Type` is set to `project`. |


<span id="tagcondition"></span>
### TagCondition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Tags |Array of [KVComparator](https://docs.byteplus.com/en/docs/39/29852#kvcomparator) |No |\- |A list of tags.<br><br><br>* You can specify up to 10 tags.<br><br>* The tag value can be up to 50 characters in length. |
|Condition |String |No |and |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |


<span id="metacondition"></span>
### MetaCondition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Metas |Array of [MetaKVComparator](https://docs.byteplus.com/en/docs/39/29852#metakvcomparator) |No |\- |A list of resources.<br><br><br>* You can configure up to 10 resource names.<br><br>* When `Comparator` is set to `equal` or `not_equal`, no character length limit is applied to the resource name.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, the resource name cannot exceed 100 characters in length. |
|Condition |String |No |or |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |
|AllDimensions |Boolean |No |true |Whether all resources are included.<br><br><br>* **true**: All resources.<br><br>* **false**: Partial resources. |


<span id="projectcondition"></span>
### ProjectCondition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Projects |Array of String |No |["testDefault1", "testDefault2"] |A list of project names. The data type is array. Separate multiple elements with commas (`,`). |


<span id="kvcomparator"></span>
### KVComparator


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |No |testKey |Tag key. |
|Values |Array of String |No |["testValues", "testValues2"] |Tag value.<br><br><br>* When `Comparator` is set to `exist`, all values corresponding to the key are included. You cannot provide a specific value.<br><br>* When `Comparator` is `equal` or `not_equal`, you can enter multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, you can enter only one value. |
|Comparator |String |No |equal |Comparator for tag matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to<br><br>* **exist**: Exists |


<span id="metakvcomparator"></span>
### MetaKVComparator


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |No |ResourceName |The resource name. Only `ResourceName` is supported. |
|Values |Array of String |No |["testResource1", "testResource2"] |Resource values.<br><br><br>* When `Comparator` is set to `equal` or `not_equal`, you can configure multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, only one value can be configured. |
|Comparator |String |No |equal |Comparator for resource matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=UpdateObjectGroup&Version=2018-01-01
Content-Type: application/json
{
    "Name": "object_group_demo",
    "Objects": [
        {
            "Namespace": "VCM_ECS",
            "Dimensions": {
                "ResourceID": [
                    "i-yccipr76y47gra******",
                    "i-ycbibi30pm8rx6******",
                    "i-ycbibi2y5vb5oz******"
                ]
            },
            "Region": "cn-beijing",
            "Type": "enum"
        },
        {
            "Namespace": "VCM_EIP",
            "Dimensions": {
                "ResourceID": [
                    "eip-13fri2dcbxyps3n6nu5******",
                    "eip-mil3eeb3axvk5smt1a******"
                ]
            },
            "Region": "cn-beijing",
            "Type": "enum"
        }
    ],
    "Id": "1764547228734******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |String |1764547228734\*\*\*\*\*\* |Object group ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240304152908454D22F975D29B******",
        "Action": "UpdateObjectGroup",
        "Version": "2018-01-01",
        "Service": "cloudmonitor",
        "Region": "cn-beijing"
    },
    "Result": {
        "Data": "1764547228734******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
