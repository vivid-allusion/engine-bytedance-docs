---
title: "RemoveSkillFromSkillSpace - Removes Skill from a Skills space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/RemoveSkillFromSkillSpace_-_Removes_Skill_from_a_Skills_space"
---

Remove Skill from a Skills space.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|M0OIxr">必选</span> `Sample value: RemoveSkillFromSkillSpace`

The action that you want to perform. Value: RemoveSkillFromSkillSpace.



**Version ** <span data-label="purple">string  </span><span data-api-tag="require|lJgTB6">必选</span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**SkillId ** <span data-label="purple">string </span><span data-api-tag="require|pTbOXe">必选</span> `Sample value: s-yed19lc8ow54****`

The Skill ID.



**SkillSpaceId ** <span data-label="purple">string </span><span data-api-tag="require|7wG2cT">必选</span> `Sample value: ss-yed0d8u1ogo2****`

The ID of the Skills space.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=RemoveSkillFromSkillSpace&Version=2025-10-30 HTTP/1.1
{
  "SkillId": "s-yed19lc8ow54****",
  "SkillSpaceId": "ss-yed0d8u1ogo2****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601061535591211850****",
    "Action": "RemoveSkillFromSkillSpace",
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
