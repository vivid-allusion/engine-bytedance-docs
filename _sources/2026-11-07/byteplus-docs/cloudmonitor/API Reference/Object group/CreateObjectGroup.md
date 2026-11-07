---
title: "CreateObjectGroup"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/CreateObjectGroup"
---

Create an object group.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Each BytePlus root user can have up to 100 object groups at the same time.

* An object group can contain up to 100 cloud products, with at most 1,000 resources specified for each cloud product. An object group can contain up to 5,000 cloud product resources.

* An object group can be associated only with one alert template.


<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=CreateObjectGroup&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateObjectGroup&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateObjectGroup |The name of the API. The API name is `CreateObjectGroup`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Name |String |No |object_group_demo |Object group name.<br><br><br>* It can contain only Chinese characters, letters, digits, and underscores (`_`).<br><br>* It must be 1 to 64 characters in length. |
|Objects |Array of [Object](https://docs.byteplus.com/en/docs/39/29851#object) |No |\- |A list of cloud product resources to be grouped. The maximum list length is 100. |


<span id="object"></span>
### Object


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Namespace |String |No |VCM_ECS |The namespace of the cloud service in Cloud Monitor. For details, see **Namespaces** in [Cloud product monitor metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics). |
|Dimensions |JSON Map |No |\- |Cloud product resource IDs. |
|Region |String |No |cn\-beijing |Availability zone of the cloud products under the current resource collection.<br><br><br>* If `Type` is `enum`, you can specify only one Region.<br><br>* If `Type` is `dynamic`, you can specify multiple Regions separated by commas (`,`). |
|Type |String |No |enum |Resource collection type. Available types:<br><br><br>* **enum**: Manually select resources. If it is enum, `Dimensions` cannot be empty.<br><br>* **dynamic**: Select resources by resource name, project, and tag. If it is dynamic, `DimensionConditions` cannot be empty. |
|DimensionConditions |Object of [DimensionConditions](https://docs.byteplus.com/en/docs/39/29851#dimensionconditions) |No |\- |Dimension configuration. |


<span id="dimensions"></span>
### Dimensions


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|key |String |Yes |ResourceID |Metric key. |
|value |Array of String |Yes |i\-ydvpb\*\*\* |The value corresponding to the metric key. |


<span id="dimensionconditions"></span>
### DimensionConditions


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Type |String |No |meta |Dimensions type. Available types:<br><br><br>* **project**: Select alert objects by project.<br><br>* **tag**: Select alert objects by tag.<br><br>* **meta**: Select alert objects by resource name. |
|TagCondition |Object of [TagCondition](https://docs.byteplus.com/en/docs/39/29851#tagcondition) |No |\- |Tag condition for selecting alert objects. This field is required if `Type` is `tag`. |
|MetaCondition |Object of [MetaCondition](https://docs.byteplus.com/en/docs/39/29851#metacondition) |No |\- |Resource name condition for selecting alert objects. This field is required if `Type` is `meta`. |
|ProjectCondition |Object of [ProjectCondition](https://docs.byteplus.com/en/docs/39/29851#projectcondition) |No |\- |Project condition for selecting alert objects. This field is required if `Type` is set to `project`. |


<span id="tagcondition"></span>
### TagCondition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Tags |Array of [KVComparator](https://docs.byteplus.com/en/docs/39/29851#kvcomparator) |No |\- |A list of tags.<br><br><br>* You can specify up to 10 tags.<br><br>* The tag value can be up to 50 characters in length. |
|Condition |String |No |and |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |


<span id="metacondition"></span>
### MetaCondition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Metas |Array of [MetaKVComparator](https://docs.byteplus.com/en/docs/39/29851#metakvcomparator) |No |\- |A list of resources.<br><br><br>* You can configure up to 10 resource names.<br><br>* When `Comparator` is set to `equal` or `not_equal`, the character length is unlimited.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, the resource name cannot exceed 100 characters in length. |
|Condition |String |No |or |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |
|AllDimensions |Boolean |No |true |Whether to include all resources.<br><br><br>* **true**: All resources.<br><br>* **false**: Partial resources. |


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
|Values |Array of String |No |["testValues", "testValues2"] |Tag value.<br><br><br>* When `Comparator` is set to `exist`, all values corresponding to the key are included. You cannot provide a specific value.<br><br>* When `Comparator` is set to `equal` or `not_equal`, you can enter multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, you can enter only one value. |
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
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=CreateObjectGroup&Version=2018-01-01
Content-Type: application/json
{
    "Name": "object_group_demo",
    "Objects": [
        {
            "Namespace": "VCM_ECS",
            "Dimensions": {
                "ResourceID": [
                    "i-ycsa9lvgu8cva4******",
                    "i-ycr7e0gmwwcva4******"
                ]
            },
            "Region": "cn-beijing",
            "Type": "enum"
        }
    ]
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
        "RequestId": "20240304150337F609773DD7E2C2******",
        "Action": "CreateObjectGroup",
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

This API has no error codes unique to itself. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
