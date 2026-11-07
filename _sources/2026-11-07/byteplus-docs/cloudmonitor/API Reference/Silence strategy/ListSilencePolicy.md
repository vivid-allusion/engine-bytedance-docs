---
title: "ListSilencePolicy"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListSilencePolicy"
---

&nbsp;

Query suppression policies.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListSilencePolicy&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListSilencePolicy&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListSilencePolicy |The name of the API. The API name is `ListSilencePolicy`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Name |String |No |silence\-policy |Filter by suppression policy name using fuzzy match.<br><br><br>* It cannot start with a digit or hyphen (`-`).<br><br>* The name must be 1 to 128 characters in length. |
|Ids |Array of String |No |19222306\*\*\* |Filter by suppression policy ID. |
|Namespaces |Array of String |No |["VCM_ECS","VCM_VKE"] |Filter by cloud product name. You can specify multiple elements separated by commas  (`,`). For example, `["VCM_ECS","VCM_VKE"]`. |
|EnableState |Array of String |No |enable |Filter by suppression policy status. Values:<br><br><br>* **enable**: Enabled<br><br>* **disable**: Disabled |
|SilenceType |Array of String |No |metric |Filter by suppression policy type. Values:<br><br><br>* **metric**: Alert suppression policy.<br><br>* **event**: Event suppression policy. |
|ValidState |String |No |active |Filter by whether the suppression policy is active. Values:<br><br><br>* **active**: Valid<br><br>* **expired**: Expired |
|PageNumber |Integer |No |1 |The page number for a pagination query. Default value: 1.<br><br><br>* Actual start position = (PageNumber\-1) \* PageSize<br><br>* Actual end position = PageNumber \* PageSize |
|PageSize |Integer |No |30 |The number of rows per page for a pagination query. Default value: 30. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListSilencePolicy&Version=2018-01-01
Content-Type: application/json
{
    "Name": "silence-policy",
    "Ids": [
        "19222306***"
    ],
    "Namespaces": [
        "VCM_ECS",
        "VCM_VKE"
    ],
    "EnableState": [
        "enable"
    ],
    "SilenceType": [
        "event"
    ],
    "ValidState": "active",
    "PageNumber": 1,
    "PageSize": 30
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of [SilencePolicy](https://docs.byteplus.com/en/docs/39/54550#silencepolicy) |\- |Suppression policy details. |


<span id="silencepolicy"></span>
### SilencePolicy


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Id |String |19222306\*\*\* |Suppression policy ID. |
|Name |String |silence\-policy |Suppression policy name. |
|Description |String |this is a silence policy |Description of the suppression policy. |
|CreatedAt |String |1659421463 |Time when the suppression policy was created. It is a timestamp. |
|Namespace |String |VCM_ECS |The namespace to which the metric specified in this suppression policy belongs. For details, see the **Namespace** field on the [Cloud Monitor metric query](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) page for each cloud product. |
|UpdatedAt |String |1659529768 |Time when the suppression policy was last updated. It is a timestamp. |
|EffectTime |Object of [EffectTime](https://docs.byteplus.com/en/docs/39/54550#effecttime) |\- |The period when the suppression policy is active. |
|ValidState |String |enable |Whether the suppression policy has expired. If the return value is `expired`, it has expired. |
|EnableState |String |enable |Suppression policy status. Values:<br><br><br>* **enable**: Enabled<br><br>* **disable**: Disabled |
|SilenceType |String |metric |Suppression policy type. Values:<br><br><br>* **metric**: Alert suppression policy.<br><br>* **event**: Event suppression policy. |
|SilenceConditions |Object of [SilenceConditions](https://docs.byteplus.com/en/docs/39/54550#silenceconditions) |\- |Suppression conditions. |


<span id="effecttime"></span>
### EffectTime


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Type |String |always |Type of the active time of the suppression policy. Values:<br><br><br>* **always**: Permanent suppression.<br><br>* **once**: Absolute time\-based suppression.<br><br>* **daily**: Relative time\-based suppression. The policy recurrently takes effect on a daily basis. |
|Range |Array of [Range](https://docs.byteplus.com/en/docs/39/54550#range) |\- |Time range. |


<span id="silenceconditions"></span>
### SilenceConditions


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|RuleId |String |1894363\*\*\* |Alert policy ID or event rule ID. If `MetaCondition` is not configured, suppression applies to all matching resources. |
|EventType |Array of String |["ecs:Disk:DiskError.Redeploy.Executing"] |Event type matched by the suppression policy.<br><br>This setting is valid only when `SilenceType` is `event`. It supports up to 100 items. |
|MetaCondition |Object of [SilenceCondition](https://docs.byteplus.com/en/docs/39/54550#silencecondition) |\- |Resource filter for suppression. |


<span id="range"></span>
### Range


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|StartDate |String |2024\-10\-01 |The date when the suppression policy starts being active.<br><br><br>* If `Type` is `once`, this field is required.<br><br>* If `Type` is `daily`, this field is optional.<br><br>   * If this field is configured, the policy is recurrently active within the specified date range.<br><br>   * If this field is not configured, the policy is recurrently active permanently.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>StartDate</code> and <code>EndDate</code> must be configured together, and <code>StartDate</code> must be earlier than <code>EndDate</code>.</div><br> |
|EndDate |String |2024\-10\-30 |The date when the suppression policy stops being active.<br><br><br>* If `Type` is `once`, this field is required.<br><br>* If `Type` is `daily`, this field is optional.<br><br>   * If this field is configured, the policy is recurrently active within the specified date range.<br><br>   * If this field is not configured, the policy is recurrently active permanently.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>StartDate</code> and <code>EndDate</code> must be configured together, and <code>StartDate</code> must be earlier than <code>EndDate</code>.</div><br> |
|StartTime |String |08:00 |The time when the suppression policy starts being active.<br><br><br>* If `Type` is `once`, it is an absolute date and time combination, for example, `2006-01-02 15:04`.<br><br>* If `Type` is `daily`, it is a specific time of each day, for example, `08:00`. |
|EndTime |String |16:00 |The time when the suppression policy stops being active.<br><br><br>* If `Type` is `once`, it is an absolute date and time combination, for example, `2006-01-02 18:00`.<br><br>* If `Type` is `daily`, it is a specific time of each day, for example, `16:00`. |


<span id="silencecondition"></span>
### SilenceCondition


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Metas |Array of [SilenceKVComparator](https://docs.byteplus.com/en/docs/39/54550#silencekvcomparator) |\- |Suppression conditions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A maximum of 10 suppression conditions can be configured.</div><br> |
|Condition |String |and |Suppression condition logic. Values:<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |


<span id="silencekvcomparator"></span>
### SilenceKVComparator


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Key |String |ResourceID |* When configuring an alert suppression policy, you can configure DimensionName. For example, if `Namespace` is `VCM_VKE`, you can enter `Cluster`, `Node`, or another supported value.<br><br>* When configuring an event suppression policy:<br><br>   * You can configure `ResourceID` to implement suppression by resource.<br><br>   * You can specify `data.xxx` to implement suppression based on values in event details. |
|Values |Array of String |["i\-ydvsmy\*\*\*"] |Value of the corresponding `key`.<br><br>The maximum number of array elements is 100, and each element can contain up to 128 characters. |
|Comparator |String |equal |Comparator for tag matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202503101953411F3BBDBD6E90438E2B95",
        "Action": "ListSilencePolicy",
        "Version": "2018-01-01",
        "Service": "cloudmonitor",
        "Region": "cn-beijing"
    },
    "Result": {
        "Data": [
            {
                "Name": "silence-policy",
                "Id": "1873407632939147264",
                "CreatedAt": "1735490161",
                "UpdatedAt": "1735827170",
                "Description": "",
                "Namespace": "VCM_ECS",
                "EnableState": "disable",
                "ValidState": "active",
                "EffectTime": {
                    "Type": "always"
                },
                "SilenceType": "metric",
                "SilenceConditions": {
                    "MetaCondition": {
                        "Condition": "or",
                        "Metas": [
                            {
                                "Key": "ResourceID",
                                "Values": [
                                    "i-ydlzxal***"
                                ],
                                "Comparator": "equal"
                            },
                            {
                                "Key": "ResourceID",
                                "Values": [
                                    "18265077***"
                                ],
                                "Comparator": "not_contain"
                            }
                        ]
                    }
                }
            }
        ],
        "PageNumber": 2,
        "PageSize": 10,
        "TotalCount": 52
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
