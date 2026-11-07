---
title: "DeleteSkill - Deletes a Skill"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/DeleteSkill_-_Deletes_a_Skill"
---

Delete a Skill.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|fFMsAd">必选</span> `Sample value: DeleteSkill`

The action that you want to perform. Value: DeleteSkill.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|vNAOtm">必选</span>  `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|1yFOC8">必选</span> `Sample value: s-yed19lc8ow54****`

The Skill ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=DeleteSkill&Version=2025-10-30 HTTP/1.1
{
  "Id": "s-yed19lc8ow54****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601061507550680150322****",
    "Action": "DeleteSkill",
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
