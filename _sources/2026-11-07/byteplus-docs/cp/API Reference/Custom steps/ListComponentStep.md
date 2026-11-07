---
title: "ListComponentStep"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ListComponentStep"
---

Query custom steps for the current account

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the Region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=ListComponentStep&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListComponentStep |The API name. The name of the current API is `ListComponentStep`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|Filter |Object of [ComponentStepFilter](https://docs.byteplus.com/en/docs/292/73432#componentstepfilter) |no |\- |Custom steps filter condition |
|PageNumber |Long |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Long |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="componentstepfilter"></span>
### ComponentStepFilter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|IsBuiltin |Boolean |no |false |Indicates whether this is a predefined step. In this scenario, the value is false. |
|Name |String |no |demo |Filter by custom step name using fuzzy matching. |
|Category |String |no |Test |Filter custom steps by category:<br><br><br>* Other: others.<br><br>* Build<br><br>* Test: Test<br><br>* Deployment<br><br>* Registry: Image registry<br><br>* Command: command execution |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=ListComponentStep&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "IsBuiltin": false
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TotalCount |Long |10 |Total number of custom steps. |
|Items |Array of [ComponentStep](https://docs.byteplus.com/en/docs/292/73432#componentstep) |\- |Custom steps list. |
|PageSize |Long |10 |Page size. |
|PageNumber |Long |1 |The current page number. |


<span id="componentstep"></span>
### ComponentStep


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Identifier |String |custom@1.0.0/v2customstep |Custom step unique identifier. |
|Name |String |v2customstep |Custom step name. |
|DisplayName |String |Custom steps V2 |The custom step display name. |
|Image |String |busybox:latest |Custom step execution image |
|Inputs |Array of [ComponentInput](https://docs.byteplus.com/en/docs/292/73432#componentinput) |\- |Custom steps input |
|Outputs |Array of [ComponentOutput](https://docs.byteplus.com/en/docs/292/73432#componentoutput) |\- |Custom Step output. |
|WorkingDirectory |String | |Working directory. |
|Script |String | |Script for executing custom steps. |
|Description |String |This is a description. |Custom steps description. |
|Category |String |Command |Custom step categories<br><br><br>* Other<br><br>* Build<br><br>* Test<br><br>* Deploy: Deployment<br><br>* Registry: image registry<br><br>* Command: Command execution |
|Yaml |String | |YAML description for custom steps. |
|Creator |Object of [IAMUser](https://docs.byteplus.com/en/docs/292/73432#iamuser) |\- |The custom steps creator. |
|CreateTime |String |2023\-05\-10T21:33:20Z |Custom step creation time. |
|UpdateTime |String |2023\-05\-10T21:33:20Z |Update time for custom steps. |


<span id="componentinput"></span>
### ComponentInput


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Name |String |version |Input a name. |
|DisplayName |String |version |Enter a display name. |
|Type |String |string |Input type:<br><br><br>* string (default value): "string"<br><br>* array |
|DefaultValue |String |v1 |Default value. |
|Required |Boolean |true |Input required:<br><br><br>* true: Yes<br><br>* false: No |
|Description |String |A description |Enter a description. |
|UiConfig |Object of [UiField](https://docs.byteplus.com/en/docs/292/73432#uifield) |\- |Input UI configuration. |


<span id="uifield"></span>
### UiField


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |Input |UI component types mapped to frontend UI components.<br><br><br>* Input (default value): input field<br><br>* Select: Dropdown list<br><br>* CheckBoxGroup: checkbox<br><br>* CodeEditor: Command line, supports Bash commands by default<br><br>* Password: Input box where entered characters are displayed as asterisks<br><br>* Text: Fixed text that displays a section of read\-only text. |
|DataSource |Object of [DataSource](https://docs.byteplus.com/en/docs/292/73432#datasource) |\- |UI component data sources. |
|ValidateRule |Array of String | |The validation rule name will be mapped to some preset validation rules on the frontend. |


<span id="datasource"></span>
### DataSource


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |value |Data source type. The default value is value, and currently only value is supported. |
|Value |Array of String |["v1"] |Data values that match the corresponding component. |


<span id="componentoutput"></span>
### ComponentOutput


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Name |String |count |Output name. |
|DisplayName |String |count |The output display name. |
|Type |String |string |Output type:<br><br><br>* string (default value): string<br><br>* array: a data structure used to store a collection of elements |
|DefaultValue |String |1 |Default value. |
|Description |String |Maximum Number of Instances |Description. |


<span id="iamuser"></span>
### IAMUser


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AccountId |Long |210048\*\*\*\* |account (main account) ID. |
|UserId |Long |28\*\*\*\* |Sub\-user (IAM user) ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071831008065A83CB2C0585****",
        "Action": "ListComponentStep",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Items": [
            {
                "Identifier": "custom@1.0.0/autotest-****",
                "Name": "autotest-VXd4O9",
                "DisplayName": "customstep—0330030017",
                "Image": "cp-enterprise-ap-southeast-1.cr.volces.com/cp-auto-test/****",
                "Inputs": [
                    {
                        "Name": "cmd",
                        "DisplayName": "Custom Step Command Execution",
                        "Type": "string",
                        "DefaultValue": "\"echo 'hello world'\"",
                        "Required": true,
                        "Description": "command",
                        "UiConfig": {
                            "Type": "Input",
                            "DataSource": null,
                            "ValidateRule": null
                        }
                    }
                ],
                "WorkingDirectory": "",
                "Script": "$(inputs.cmd)",
                "Description": null,
                "Category": "Command",
                "Status": "Enabled",
                "Yaml": "step: autotest-VXd4O9\ndisplayName: customstep—0330030017\nimage: cp-enterprise-ap-southeast-1.cr.volces.com/cp-auto-test/****\ninputs:\n    - name: cmd\n      displayName: Custom Step Command Execution\n      type: string\n      defaultValue: echo 'hello world'\n      required: true\n      description: Please enter commands\n      uiConfig:\n        type: Input\nscript: $(inputs.cmd)\ncategory: Command\n",
                "Creator": {
                    "AccountId": 210048****,
                    "UserId": 539****
                },
                "CreateTime": "2024-03-30T03:00:17+08:00",
                "UpdateTime": "2024-03-30T03:00:17+08:00"
            }
        ],
        "PageSize": 1,
        "PageNumber": 1,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not have dedicated error codes. If the API call returns an exception, refer to the [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
