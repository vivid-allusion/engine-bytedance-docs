---
title: "ListSkillsBySkillSpace - Queries version details of a Skill in a specific space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListSkillsBySkillSpace_-_Queries_version_details_of_a_Skill_in_a_specific_space"
---

Query details for existing Skill versions within a Skills space using custom filter criteria.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|6yZCor">必选</span> `Sample value: ListSkillsBySkillSpace`

The action that you want to perform. Value: ListSkillsBySkillSpace.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|6EQyr8">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



**Filter ** <span data-label="purple">object </span>`Optional` `Sample value: --`

The filter conditions for Skill. If you do not specify this parameter, all Skills in the Skills space are queried by default.


**Status ** <span data-label="purple">string[] </span>`Optional` `Sample value: creating`

The version status of the Skill. Value:


* creating: Being created.

* running: Running.

* failed: Unavailable. This indicates a version creation failure.



**Id ** <span data-label="purple">string </span>`Optional` `Sample value: s-yed19lc8ow54****`

The Skill ID.



**Name ** <span data-label="purple">string </span>`Optional` `Sample value: name1`

The Skill name.




**SkillSpaceId ** <span data-label="purple">string </span><span data-api-tag="require|0pNhsU">必选</span> `Sample value: ss-yed0d8u1ogo2****`

The ID of the Skills space.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

The details of Skill added to the Skill space.


**SkillStatus ** <span data-label="purple">string </span>`Sample value: running`

The version status of the Skill.



**SkillSpaceId ** <span data-label="purple">string </span>`Sample value: ss-yed0d8u1ogo2****`

The ID of the Skills space.



**SkillSpaceName ** <span data-label="purple">string </span>`Sample value: space01`

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




**TotalCount ** <span data-label="purple">integer </span>`Sample value: 1`

The total number of Skills that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListSkillsBySkillSpace&Version=2025-10-30 HTTP/1.1
{
  "SkillSpaceId": "ss-yed0d8u1ogo2****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601061821220510072490****",
    "Action": "ListSkillsBySkillSpace",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Items": [
      {
        "SkillStatus": "running",
        "SkillSpaceId": "ss-yed0d8u1ogo2****",
        "SkillSpaceName": "name1",
        "SkillSpaceDescription": "description",
        "SkillSpaceStatus": "creating",
        "SkillId": "s-yed19lc8ow54****",
        "SkillName": "name1",
        "Version": "v1",
        "SkillDescription": "description"
      }
    ],
    "TotalCount": 1
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
