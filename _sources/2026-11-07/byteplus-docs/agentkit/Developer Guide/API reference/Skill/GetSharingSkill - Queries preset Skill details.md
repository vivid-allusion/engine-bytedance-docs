---
title: "GetSharingSkill - Queries preset Skill details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetSharingSkill_-_Queries_preset_Skill_details"
---

Query preset Skill details.

<span id="Il2U5Z9H"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://www.volcengine.com/docs/6369/67268).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|PFDjwK">必选</span> `Sample value: GetSharingSkill`

The action that you want to perform. Value: GetSharingSkill.



**Version ** <span data-label="purple">string  </span><span data-api-tag="require|l4ydah">必选</span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string</span><span data-api-tag="require|kwsW1t">必选</span>  `Sample value: s-yed19lc8ow54****`

The ID of Skill.



&nbsp;

<span id="5z3I2DO4"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://www.volcengine.com/docs/6369/80336).



**Id ** <span data-label="purple">string </span>`Sample value: s-yed19lc8ow54****`

Skill ID.



**Name ** <span data-label="purple">string </span>`Sample value: name1`

The Skill name.



**Status ** <span data-label="purple">string </span>`Sample value: creating`

The Skill status. The status of Skill is determined by the status of its versions. Valid values:


* creating: Creating. This indicates that the Skill has only one version, and that version is being created.

* failed: Unavailable. This indicates that all versions of the Skill are unavailable.

* updating: Updating. This indicates that the Skill has more than one version, and at least one version is being created.

* running: Running. This indicates that the versions of the Skill are in a state other than those described above.



**Description ** <span data-label="purple">string </span>`Sample value: description1`

The description of the Skill.



**Versions ** <span data-label="purple">string[] </span>`Sample value: v1`

The Skill version number.



**CreateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The creation time of the Skill (Unix timestamp format).



**UpdateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The update time of the Skill (Unix timestamp format).



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The name of the project associated with the Skill.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tags associated with the Skill.


**Key ** <span data-label="purple">string </span>`Sample value: key01`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: value01`

The tag value.




&nbsp;

<span id="63NXUTpq"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetSharingSkill&Version=2025-10-30 HTTP/1.1
{
  "Id": "s-yed19lc8ow54****"
}
```


<span id="RkyjcKvU"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601071728112051090890****",
    "Action": "GetSharingSkill",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Id": "s-yed19lc8ow54****",
    "Name": "name1",
    "Status": "creating",
    "Description": "description1",
    "Versions": [
      "v1"
    ],
    "CreateTimeStamp": "1767528835",
    "UpdateTimeStamp": "1767528835"
    "ProjectName": "default",
    "Tags": [
      {
        "Key": "key01",
        "Value": "value01"
      }
    ]
  }
}
```


<span id="e5sWrT9V"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://www.volcengine.com/docs/86681/1913777).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|404 |ResourceNotFound |The specified resource cannot be found. |The corresponding resource cannot be found. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |
