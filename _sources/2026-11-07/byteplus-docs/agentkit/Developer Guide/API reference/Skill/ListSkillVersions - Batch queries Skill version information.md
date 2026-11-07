---
title: "ListSkillVersions - Batch queries Skill version information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListSkillVersions_-_Batch_queries_Skill_version_information"
---

Batch query Skill version information.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|mnzdAS">必选</span> `Sample value: ListSkillVersions`

The action that you want to perform. Value: ListSkillVersions.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|Mz0S4M">必选</span>  `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|JHS0HN">必选</span> `Sample value: s-yed19lc8ow54****`

The Skill ID.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



**PageSize ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 1`

Total number of versions that meet the condition.



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

Version details.


**Id ** <span data-label="purple">string </span>`Sample value: s-yed19lc8ow54****`

The Skill ID.



**Name ** <span data-label="purple">string </span>`Sample value: test`

The Skill name.



**Status ** <span data-label="purple">string </span>`Sample value: running`

The version status of the Skill. Value:


* creating: Being created.

* running: Running.

* failed: Unavailable. This indicates a version creation failure.



**Description ** <span data-label="purple">string </span>`Sample value: description`

The Skill description.



**Version ** <span data-label="purple">string </span>`Sample value: v1`

The Skill version number.



**CreateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767595285`

The Skill creation time (in Unix timestamp format).



**UpdateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767595285`

The Skill update time (in Unix timestamp format).



**Relations ** <span data-label="purple">object[] </span>`Sample value: --`

Details of Skill and Skills space associated with the Skill version.


**SkillStatus ** <span data-label="purple">string </span>`Sample value: running`

The Skill status. The status of Skill is determined by the status of its versions. Valid values:


* creating: Creating. This indicates that the Skill has only one version, and that version is being created.

* failed: Unavailable. This indicates that all versions of the Skill are unavailable.

* updating: Updating. This indicates that the Skill has more than one version, and at least one version is being created.

* running: Running. This indicates that the versions of the Skill are in a state other than those described above.



**SkillSpaceId ** <span data-label="purple">string </span>`Sample value: ss-yed0d8u1ogo2****`

The ID of the Skills space.



**SkillSpaceName ** <span data-label="purple">string </span>`Sample value: name1`

The name of the Skills space.



**SkillSpaceDescription ** <span data-label="purple">string </span>`Sample value: description`

The description of the Skills space.



**SkillSpaceStatus ** <span data-label="purple">string </span>`Sample value: creating`

The status of the Skills space. Value:


* creating: Being created.

* running: Running.



**SkillId ** <span data-label="purple">string </span>`Sample value: s-yed19lc8ow54****`

The Skill ID.



**SkillName ** <span data-label="purple">string </span>`Sample value: name1`

The Skill name.



**Version ** <span data-label="purple">string </span>`Sample value: v1`

The Skill version number.



**SkillDescription ** <span data-label="purple">string </span>`Sample value: description`

The Skill description.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListSkillVersions&Version=2025-10-30 HTTP/1.1
{
  "Id": "s-yed19lc8ow54****",
  "PageNumber": 1,
  "PageSize": 10,
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20260107164731FCD65E6EC9B****",
        "Action": "ListSkillVersions",
        "Version": "2025-10-30",
        "Service": "agentkit"
    },
    "Result": {
        "Items": [
            {
                "Id": "s-yed19lc8ow54****",
                "Name": "algorithmic-art-4",
                "Status": "running",
                "Description": "description",
                "Version": "v1"
                "CreateTimeStamp": "1767595284",
                "UpdateTimeStamp": "1767595285",
                "Relations": [],
            }
        ],
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
