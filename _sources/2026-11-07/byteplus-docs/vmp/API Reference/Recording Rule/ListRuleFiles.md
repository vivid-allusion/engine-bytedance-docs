---
title: "ListRuleFiles"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListRuleFiles"
---

Obtain the list of RecordingRule files.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListRuleFiles&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required or Not |Value example |Descriptions |
|---|---|---|---|---|
|Action |String |Yes |ListRuleFiles |interface name. The API name is `ListRuleFiles`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |Current page number, minimum or default value is 1. |
|PageSize |Long |No |10 |Results per page:<br><br><br>* The value can range from 0 to 100.<br><br>* Default value is 10. |
|Filter |Object of [RuleFileFilter](https://docs.byteplus.com/en/docs/vmp/ListRuleFiles#rulefilefilter) |No |\- |Filter conditions for rule files. |


<span id="RuleFileFilter"></span>
### RuleFileFilter


|Parameters |Type |Required or Not |Sample Values |Descriptions |
|---|---|---|---|---|
|Ids |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Exact query by rule file IDs. |
|Name |String |No |test |Fuzzy query by the name of the rule file. |
|Status |Array of String |No |["Running"] |Exact query by rule statuses. |
|WorkspaceId |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Exact query by workspace IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListRuleFiles&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Ids": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ],
        "Name": "test",
        "Status": [
            "Running"
        ],
        "WorkspaceId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample Values |Descriptions |
|---|---|---|---|
|Total |Long |100 |Total number of rule files. |
|Items |Array of [RuleFile](https://docs.byteplus.com/en/docs/vmp/ListRuleFiles#rulefile) |\- |A list of rule files. |


<span id="RuleFile"></span>
### RuleFile


|Parameters |Type |Sample Values |Descriptions |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Rule file id |
|Name |String |test |Rule file name:\n\- a valid Linux file name with a length less than 255\n\- it needs to be unique in the workspace |
|Status |String |Running |Rule file status:\n\- Creating\n\- Running\n\- Updating\n\- OverdueShutted\n\- Resuming |
|Content |String |{"groups": [{"name": "my_first_recording_rule", "rules": [{"expr": "up", "record": "up"}], "interval": "30s"}]} |Rule file content:\n\- Data in YAML format\n\- Length requirements\n\- A single expr can be up to 16 KB in size\n\- A single record can be up to 2,048 bytes in size\n\- A single labelname can be up to 256 bytes in size\n\- A single labelvalue can be up to 2,048 bytes in size |
|RuleCount |Long |2 |Number of rules in the rule file |
|CreateTime |String |2022\-01\-01T00:00:00Z |Creation date of rule file |
|Description |String |This is a description |Description of the rule file:<br><br><br>* Supports length of 0\-200 characters (one English character, one Chinese character, or one symbol counts as one character).<br><br>* Supports user modifications |
|LastUpdateTime |String |2022\-01\-01T00:00:00Z |The latest date that the rule file was updated. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListRuleFiles",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "Name": "test",
                "Status": "Running",
                "RuleCount": 2,
                "CreateTime": "2022-01-01T00:00:00Z",
                "Description": "This is a description",
                "LastUpdateTime": "2022-01-01T00:00:00Z"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes specific to this API. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|HTTP status codeS |Error code |Error messages |DescriptionS |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing necessary parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP service. |
|404 |NotFound.Workspace |The specified Workspace {{id}} is not found. |The workspace with the ID was not found. |
