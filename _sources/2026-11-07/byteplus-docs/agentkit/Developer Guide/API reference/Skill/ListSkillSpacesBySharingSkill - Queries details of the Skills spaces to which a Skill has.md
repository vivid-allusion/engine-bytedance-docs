---
title: "ListSkillSpacesBySharingSkill - Queries details of the Skills spaces to which a Skill has been added"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListSkillSpacesBySharingSkill_-_Queries_details_of_the_Skills_spaces_to_which_a_Skill_has_been_added"
---

You can use custom filter conditions to query details of Skills spaces to which a preset Skill has been added.

<span id="UJ3ofpfb"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://www.volcengine.com/docs/6369/67268).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|YcilnG">必选</span> `Sample value: ListSkillSpacesBySharingSkill`

The action that you want to perform. Value: ListSkillSpacesBySharingSkill.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|14lEvI">必选</span>  `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**SkillId**<span data-label="purple"> string</span><span data-api-tag="require|vD20R7">必选</span>  `Sample value: s-yed19lc8ow54****`

The Skill ID.



**SkillVersion ** <span data-label="purple">string </span>`Optional` `Sample value: v1`

The Skill version number. If this parameter is not provided, all versions are returned by default.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



**Filter ** <span data-label="purple">object </span>`Optional` `Sample value: --`

The conditions for filtering Skills spaces. If this parameter is not specified, all Skills spaces to which the Skill has been added are queried by default.


**Status ** <span data-label="purple">string[] </span>`Optional` `Sample value: creating`

The status of the Skills space. Value:


* creating: Being created.

* running: Running.



**Id ** <span data-label="purple">string </span>`Optional` `Sample value: ss-yed0d8u1ogo2****`

The ID of the Skills space.



**Name ** <span data-label="purple">string </span>`Optional` `Sample value: space01`

The name of the Skills space.




&nbsp;

<span id="W2MzofNr"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://www.volcengine.com/docs/6369/80336).



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

Details of the Skills space to which the Skill has been added.


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




**TotalCount ** <span data-label="purple">integer </span>`Sample value: 1`

The total number of Skills spaces that meet the conditions.



&nbsp;

<span id="FZrSokhY"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListSkillSpacesBySharingSkill&Version=2025-10-30 HTTP/1.1
{
  "SkillId": "s-yed19lc8ow54****",
  "SkillVersion": "v1",
  "PageNumber": 1,
  "PageSize": 10,
  "Filter": {
    "Status": [
      "creating"
    ],
    "Id": "b9dc3cf6-c29e-48e4-82e1-fa2d4****",
    "Name": name1"
  }
}
```


<span id="wTwoAOMD"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601061848461732461600****",
    "Action": "ListSkillSpacesBySharingSkill",
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


<span id="PVk2H3kd"></span>
## Error codes

To learn more error codes, see [Common error codes](https://www.volcengine.com/docs/86681/1913777).
