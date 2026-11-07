---
title: "UpdateSkillSpace - Updates Skills space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UpdateSkillSpace_-_Updates_Skills_space"
---

Update a Skills space.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|E7rDY4">必选</span> `Sample value: UpdateSkillSpace`

The action that you want to perform. Value: UpdateSkillSpace.



**Version**<span data-label="purple"> string </span><span data-api-tag="require|pXqZmK">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|F8jNfY">必选</span> `Sample value: ss-yed0d8u1ogo2****`

The ID of the Skills space.



**Name ** <span data-label="purple">string </span>`Optional` `Sample value: name1`

The name of the Skills space. Value:


* A maximum of 64 characters is allowed.

* Can only contain lowercase letters, numbers, and hyphens.

* Cannot contain XML tags.

* Cannot contain the reserved word "agentkit".



**Description ** <span data-label="purple">string </span>`Optional` `Sample value: description`

The description of the Skills space. Value:


* A maximum of 1,024 characters is allowed.

* Cannot contain XML tags.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=UpdateSkillSpace&Version=2025-10-30 HTTP/1.1
{
  "Id": "ss-yed0d8u1ogo2****",
  "Name": "name1",
  "Description": "description"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2026010617484717606112408****",
    "Action": "UpdateSkillSpace",
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
