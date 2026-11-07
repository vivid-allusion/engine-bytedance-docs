---
title: "GetSkill - Queries Skill details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetSkill_-_Queries_Skill_details"
---

Query Skill details.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|bvee3V">必选</span> `Sample value: GetSkill`

The action that you want to perform. Value: GetSkill.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ctGKxn">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|DnkmX2">必选</span> `Sample value: s-yed19lc8ow54****`

The ID of Skill.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



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

The Skill description.



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

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetSkill&Version=2025-10-30 HTTP/1.1
{
  "Id": "s-yed19lc8ow54****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601071728112051090890****",
    "Action": "GetSkill",
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


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
