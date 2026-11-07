---
title: "ListObjectGroups"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListObjectGroups"
---

Query the list of object groups.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListObjectGroups&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListObjectGroups&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListObjectGroups |The name of the API. The API name is `ListObjectGroups`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|PageSize |Integer |No |20 |Number of rows per page for a pagination query. The default value is 10. |
|PageNumber |Integer |No |1 |Page number of the list. The value must be greater than 0. The default value is 1. The list range to be queried is:<br><br><br>* Actual start position = (PageNumber\-1) \* PageSize<br><br>* Actual end position = PageNumber \* PageSize |
|Ids |Array of String |No |["1744977683943\*\*\*\*\*\*"] |A list of object group IDs. |
|Name |String |No |object_group |The keyword in object group names. Fuzzy search is supported. |
|AlertTemplateIds |Array of String |No |['1963447872315\*\*\*'] |Alert template ID. You can perform the query with alert template IDs as a filter. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListObjectGroups&Version=2018-01-01
Content-Type: application/json
{
    "Ids": [
        "1744977683943******"
    ],
    "Name": "object_group",
    "AlertTemplateIds": [
        "1963447872315***"
    ],
    "PageNumber": 1,
    "PageSize": 20
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Array of [ObjectGroupVO](https://docs.byteplus.com/en/docs/39/29853#objectgroupvo) |\- |Details about object groups that meet the criteria. |


<span id="objectgroupvo"></span>
### ObjectGroupVO


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |1744977683943\*\*\*\*\*\* |Object group ID. |
|Name |String |object_group_demo |Name of the object group. |
|Objects |Array of [Object](https://docs.byteplus.com/en/docs/39/29853#object) |\- |A list of cloud product resources under the object group. |
|CreatedAt |String |2021\-10\-25T18:27:24+08:00 |Creation time of the object group. |
|UpdatedAt |String |2021\-10\-25T18:49:43+08:00 |Update time of the object group. |
|AlertTemplateId |String |1744971093943\*\*\*\*\*\* |ID of the alert template associated with the object group.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This field will soon be deprecated. We recommend using the <code>TemplateDetails</code> field.</div><br> |
|AlertTemplateName |String |Alerting template |Name of the alert template associated with the object group.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This field will soon be deprecated. We recommend using the <code>TemplateDetails</code> field.</div><br> |
|TemplateDetails |Array of [TemplateDetail](https://docs.byteplus.com/en/docs/39/29853#templatedetail) |\- |All alert templates managed by the object group. |


<span id="object"></span>
### Object


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |1763465351913\*\*\*\*\*\* |Object group ID. |
|Namespace |String |VCM_ECS |The namespace to which the cloud product belongs in Cloud Monitor. For details, see the **Namespace** field on the [Cloud Monitor metric query](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) page for each cloud product. |
|Dimensions |JSON Map |\- |Cloud product resource IDs. |
|Region |String |cn\-beijing |Availability zone of the cloud products under the current resource collection.<br><br><br>* If `Type` is `enum`, you can specify only one Region.<br><br>* If `Type` is `dynamic`, you can specify multiple Regions separated by commas (`,`). |
|Type |String |enum |Resource collection type.<br><br><br>* **enum**: Manually select resources. If it is enum, `Dimensions` cannot be empty.<br><br>* **dynamic**: Select resources by resource name, project, and tag. If it is dynamic, `DimensionConditions` cannot be empty. |
|Rules |Array of [BindRules](https://docs.byteplus.com/en/docs/39/29853#bindrules) |\- |Associated alert policies. |
|DimensionConditions |Object of [DimensionConditions](https://docs.byteplus.com/en/docs/39/29853#dimensionconditions) |\- |Dimension configuration. |


<span id="templatedetail"></span>
### TemplateDetail


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AlertTemplateId |String |1963498169788\*\*\* |Alert template ID. |
|AlertTemplateName |String |alert\-template\-demo |Alert template name. |


<span id="dimensions"></span>
### Dimensions


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |ResourceID |The key of the metric to retrieve. |
|value |Array of String |i\-es\*\*\* |The value corresponding to the key of the metric to retrieve. |


<span id="bindrules"></span>
### BindRules


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |1354766247190\*\*\*\*\*\* |ID of the associated alert policy. |
|Name |String |rule1 |Name of the associated alert policy. |
|TemplateRuleId |String |1963498169788\*\*\* |ID of the associated alert policy template. |
|AlertTemplateId |String |1963498169788\*\*\* |ID of the associated alert template. |


<span id="dimensionconditions"></span>
### DimensionConditions


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |meta |Dimensions type. Available types:<br><br><br>* **project**: Select alert objects by project.<br><br>* **tag**: Select alert objects by tag.<br><br>* **meta**: Select alert objects by resource name. |
|TagCondition |Object of [TagCondition](https://docs.byteplus.com/en/docs/39/29853#tagcondition) |\- |Tag condition for selecting alert objects. This field is required if `Type` is `tag`. |
|MetaCondition |Object of [MetaCondition](https://docs.byteplus.com/en/docs/39/29853#metacondition) |\- |Resource name condition for selecting alert objects. This field is required if `Type` is `meta`. |
|ProjectCondition |Object of [ProjectCondition](https://docs.byteplus.com/en/docs/39/29853#projectcondition) |\- |Project condition for selecting alert objects. This field is required if `Type` is set to `project`. |


<span id="tagcondition"></span>
### TagCondition


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Tags |Array of [KVComparator](https://docs.byteplus.com/en/docs/39/29853#kvcomparator) |\- |A list of tags.<br><br><br>* You can specify up to 10 tags.<br><br>* The tag value can be up to 50 characters in length. |
|Condition |String |and |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition can be met. |


<span id="metacondition"></span>
### MetaCondition


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Metas |Array of [MetaKVComparator](https://docs.byteplus.com/en/docs/39/29853#metakvcomparator) |\- |A list of resources.<br><br><br>* You can configure up to 10 resource names.<br><br>* When `Comparator` is set to `equal` or `not_equal`, no character length limit is applied to the resource name.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, the resource name cannot exceed 100 characters in length. |
|Condition |String |or |Condition for evaluation.<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |
|AllDimensions |Boolean |true |Whether all resources are included.<br><br><br>* **true**: All resources.<br><br>* **false**: Partial resources. |


<span id="projectcondition"></span>
### ProjectCondition


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Projects |Array of String |["testDefault1", "testDefault2"] |A list of project names. The data type is array. Separate multiple elements with comma (`,`). |


<span id="kvcomparator"></span>
### KVComparator


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |testKey |Tag key. |
|Values |Array of String |["testValues", "testValues2"] |Tag value.<br><br><br>* When `Comparator` is set to `exist`, all values corresponding to the key are included. You cannot provide a specific value.<br><br>* When `Comparator` is set to `equal` or `not_equal`, you can enter multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, you can enter only one value. |
|Comparator |String |equal |Comparator for tag matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to<br><br>* **exist**: Exists |


<span id="metakvcomparator"></span>
### MetaKVComparator


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |ResourceName |The resource name. Only `ResourceName` is supported. |
|Values |Array of String |["testResource1", "testResource2"] |Resource values.<br><br><br>* When `Comparator` is set to `equal` or `not_equal`, you can configure multiple values.<br><br>* When `Comparator` is set to `contain`, `not_contain`, `prefix_match`, or `suffix_match`, only one value can be configured. |
|Comparator |String |equal |Comparator for resource matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListObjectGroups",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Id": "1744977683943******",
                "Name": "object_group_demo",
                "Objects": [
                    {
                        "Id": "1763465351913******",
                        "Type": "enum",
                        "Rules": [
                            {
                                "Id": "1354766247190******",
                                "Name": "rule1",
                                "TemplateRuleId": "1963498169788***",
                                "AlertTemplateId": "1963498169788***"
                            }
                        ],
                        "Region": "cn-beijing",
                        "Namespace": "VCM_ECS",
                        "DimensionConditions": {
                            "Type": "meta",
                            "TagCondition": {
                                "Tags": [
                                    {
                                        "Key": "testKey",
                                        "Values": [
                                            "testValues",
                                            "testValues2"
                                        ],
                                        "Comparator": "equal"
                                    }
                                ],
                                "Condition": "and"
                            },
                            "MetaCondition": {
                                "Metas": [
                                    {
                                        "Key": "ResourceName",
                                        "Values": [
                                            "testResource1",
                                            "testResource2"
                                        ],
                                        "Comparator": "equal"
                                    }
                                ],
                                "Condition": "or",
                                "AllDimensions": true
                            },
                            "ProjectCondition": {
                                "Projects": [
                                    "testDefault1",
                                    "testDefault2"
                                ]
                            }
                        }
                    }
                ],
                "CreatedAt": "2021-10-25T18:27:24+08:00",
                "UpdatedAt": "2021-10-25T18:49:43+08:00",
                "AlertTemplateId": "1744971093943******",
                "AlertTemplateName": "Alarm template",
                "TemplateDetails": [
                    {
                        "AlertTemplateId": "1963498169788***",
                        "AlertTemplateName": "alert-template-demo"
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
