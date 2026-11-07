---
title: "CreateSilencePolicy"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/CreateSilencePolicy"
---

parametersparametersparametersmetersCreate a suppression policy.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

A root user can have up to 1,000 suppression policies.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=CreateSilencePolicy&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateSilencePolicy&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateSilencePolicy |The name of the API. The API name is `CreateSilencePolicy`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Name |String |Yes |silence\-policy |Suppression policy name.<br><br><br>* It cannot start with a digit or hyphen (`-`).<br><br>* The name must be 1 to 128 characters in length. |
|Description |String |No |this is a silence policy |Description of the suppression policy.<br><br><br>* It cannot start with a digit, hyphen (`-`), or Chinese punctuation mark.<br><br>* It can contain only Chinese characters, letters, digits, underscore (`_`), hyphen (`-`), and Chinese punctuation marks.<br><br>* It must be 0 to 255 characters in length. |
|Namespace |String |Yes |VCM_ECS |The namespace to which the metric specified in this policy belongs. For details, see [Supported cloud services](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics) for the namespace of each cloud product. |
|SilenceType |String |Yes |metric |Suppression policy type. Values:<br><br><br>* **metric**: Alert suppression policy.<br><br>* **event**: Event suppression policy. |
|SilenceConditions |Object of [SilenceConditions](https://docs.byteplus.com/en/docs/39/54548#silenceconditions) |No |\- |Suppression conditions. |
|EffectTime |Object of [EffectTime](https://docs.byteplus.com/en/docs/39/54548#effecttime) |Yes |\- |The period when the suppression policy is active. |


<span id="silenceconditions"></span>
### SilenceConditions


|Parameters |Types |Required |Sample value |Description |
|---|---|---|---|---|
|RuleId |String |No |1894363\*\*\* |Alert policy ID or event rule ID. If `MetaCondition` is not configured, suppression applies to all matching resources. |
|EventType |Array of String |No |["ecs:Disk:DiskError.Redeploy.Executing"] |Event type matched by the suppression policy.<br><br>This setting is valid only when `SilenceType` is `event`. It supports up to 100 items. |
|MetaCondition |Object of [SilenceCondition](https://docs.byteplus.com/en/docs/39/54548#silencecondition) |No |\- |Resource filter for suppression. |


<span id="effecttime"></span>
### EffectTime


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Type |String |Yes |always |Type of the active time of the suppression policy. Values:<br><br><br>* **always**: Permanent suppression.<br><br>* **once**: Absolute time\-based suppression. The policy takes effect once.<br><br>* **daily**: Relative time\-based suppression. The policy takes effect recurrently. |
|Range |Array of [Range](https://docs.byteplus.com/en/docs/39/54548#range) |No |\- |Time range during which the suppression policy is active. This setting is required only when `Type` is `once` or `daily`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can specify up to 3 time ranges.</div><br> |


<span id="silencecondition"></span>
### SilenceCondition


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Metas |Array of [SilenceKVComparator](https://docs.byteplus.com/en/docs/39/54548#silencekvcomparator) |No |\- |Suppression conditions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A maximum of 10 suppression conditions can be configured.</div><br> |
|Condition |String |No |and |Suppression condition logic. Values:<br><br><br>* **and**: All conditions must be met.<br><br>* **or**: Any condition is met. |


<span id="range"></span>
### Range


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|StartDate |String |No |2025\-03\-10 |The date when the suppression policy starts being active.<br><br><br>* If `Type` is `once`, this field is required.<br><br>* If `Type` is `daily`, this field is optional.<br><br>   * If this field is configured, the policy is recurrently active within the specified date range.<br><br>   * If this field is not configured, the policy is recurrently active permanently.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>StartDate</code> and <code>EndDate</code> must be configured together, and <code>StartDate</code> must be earlier than <code>EndDate</code>.</div><br> |
|EndDate |String |No |2025\-03\-11 |The date when the suppression policy stops being active.<br><br><br>* If `Type` is `once`, this field is required.<br><br>* If `Type` is `daily`, this field is optional.<br><br>   * If this field is configured, the policy is recurrently active within the specified date range.<br><br>   * If this field is not configured, the policy is recurrently active permanently.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>StartDate</code> and <code>EndDate</code> must be configured together, and <code>StartDate</code> must be earlier than <code>EndDate</code>.</div><br> |
|StartTime |String |No |08:00 |The time when the suppression policy starts being active.<br><br><br>* If `Type` is `once`, it is an absolute date and time combination, for example, `2006-01-02 15:04`.<br><br>* If `Type` is `daily`, it is a specific time of each day, for example, `08:00`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>StartTime</code> and <code>EndTime</code> must both be configured, and <code>StartTime</code> must be earlier than <code>EndTime</code>.</div><br> |
|EndTime |String |No |16:00 |The time when the suppression policy stops being active.<br><br><br>* If `Type` is `once`, it is an absolute date and time combination, for example, `2006-01-02 18:00`.<br><br>* If `Type` is `daily`, it is a specific time of each day, for example, `16:00`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>StartTime</code> and <code>EndTime</code> must both be configured, and <code>StartTime</code> must be earlier than <code>EndTime</code>.</div><br> |


<span id="silencekvcomparator"></span>
### SilenceKVComparator


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |No |ResourceID |* When configuring an alert suppression policy, you can configure DimensionName. For example, if `Namespace` is `VCM_VKE`, you can enter `Cluster`, `Node`, or another supported value.<br><br>* When configuring an event suppression policy:<br><br>   * You can configure `ResourceID` to implement suppression by resource.<br><br>   * You can specify `data.xxx` to implement suppression based on values in event details. |
|Values |Array of String |No |["i\-ydvsmy\*\*\*"] |Value of the corresponding `key`.<br><br>The maximum number of array elements is 100, and each element can contain up to 128 characters. |
|Comparator |String |No |equal |Comparator for tag matching.<br><br><br>* **contain**: Contains<br><br>* **not_contain**: Does not contain<br><br>* **prefix_match**: Prefix match<br><br>* **suffix_match**: Suffix match<br><br>* **equal**: Equal to<br><br>* **not_equal**: Not equal to |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=CreateSilencePolicy&Version=2018-01-01
Content-Type: application/json
{
    "Name": "silence-policy",
    "Namespace": "VCM_ECS",
    "Description": "this is a silence policy",
    "SilenceType": "event",
    "EffectTime": {
        "Type": "daily",
        "Range": [
            {
                "EndDate": "2025-03-11",
                "EndTime": "16:00",
                "StartDate": "2025-03-10",
                "StartTime": "08:00"
            }
        ]
    },
    "SilenceConditions": {
        "RuleId": "1856943902796222464",
        "EventType": [
            "ecs:Instance:RebootInstance.Executing"
        ],
        "MetaCondition": {
            "Condition": "and",
            "Metas": [
                {
                    "Key": "ResourceID",
                    "Values": [
                        "i-ydvsmy***"
                    ],
                    "Comparator": "equal"
                }
            ]
        }
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |19222306\*\*\* |Suppression policy ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateSilencePolicy",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            "19222306***"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
