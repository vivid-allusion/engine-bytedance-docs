---
title: "ListSkillsBySpaceId - Queries basic information about added skills via Skills space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListSkillsBySpaceId_-_Queries_basic_information_about_added_skills_via_Skills_space"
---

Query basic information about added skills via Skills space.

<span id="h3tLFb5e"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|aWxbmD">必选</span> `Sample value: ListSkillsBySpaceId`

The action that you want to perform. Value: ListSkillsBySpaceId.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|7RR8NY">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**SkillSpaceId ** <span data-label="purple">string </span><span data-api-tag="require|eO3n9D">必选</span> `Sample value: ss-yedd6rcsu8****`

The ID of the Skills space.



&nbsp;

<span id="BcJ36XMc"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

The Skill details.


**Name ** <span data-label="purple">string </span>`Sample value: name1`

The Skill name.



**Description ** <span data-label="purple">string </span>`Sample value: description`

The Skill description.




&nbsp;

<span id="EO32im08"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.volcengineapi.com?Action=ListSkillsBySpaceId&Version=2025-10-30 HTTP/1.1
{
  "SkillSpaceId": "ss-yedd6rcsu8****"
}
```


<span id="JXDLwEGk"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2026010618563002****8",
    "Action": "ListSkillsBySpaceId",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Items": [
      {
        "Name": "name1",
        "Description": "description"
      }
    ]
  }
}
```


<span id="aKZBqMMM"></span>
## Error codes

To learn more about error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
