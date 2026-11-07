---
title: "PublishSkillToSkillSpace - Publishes Skill to a Skills space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/PublishSkillToSkillSpace_-_Publishes_Skill_to_a_Skills_space"
---

Publish Skill to a Skills space.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|rkUUjD">必选</span> `Sample value: PublishSkillToSkillSpace`

The action that you want to perform. Value: PublishSkillToSkillSpace.



**Version ** <span data-label="purple">string  </span><span data-api-tag="require|giOYiB">必选</span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**SkillSpaces ** <span data-label="purple">string[] </span><span data-api-tag="require|fispBG">必选</span> `Sample value: ss-yed0d8u1ogo2****`

Skill space ID. Multiple IDs are supported.



**Skills ** <span data-label="purple">object[] </span><span data-api-tag="require|OUZmAS">必选</span> `Sample value: --`

Skill information. Multiple values are supported.


**SkillId ** <span data-label="purple">string </span><span data-api-tag="require|m1AZ8c">必选</span> `Sample value: s-yed19lc8ow54****`

Skill ID.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|vxCOL1">必选</span> `Sample value: v1`

The Skill version number.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=PublishSkillToSkillSpace&Version=2025-10-30 HTTP/1.1
{
  "SkillSpaces": [
    "ss-yed0d8u1ogo2****"
  ],
  "Skills": [
    {
      "SkillId": "s-yed19lc8ow54****",
      "Version": "v1"
    }
  ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260106152534102041225212B7F238",
    "Action": "PublishSkillToSkillSpace",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
