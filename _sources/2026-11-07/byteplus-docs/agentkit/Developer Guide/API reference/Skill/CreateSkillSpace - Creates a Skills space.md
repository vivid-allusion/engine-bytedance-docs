---
title: "CreateSkillSpace - Creates a Skills space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/CreateSkillSpace_-_Creates_a_Skills_space"
---

Create a Skills space.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|rUbmRz">必选</span> `Sample value: CreateSkillSpace`

The action that you want to perform. Value: CreateSkillSpace.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|HcHyWM">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Name ** <span data-label="purple">string </span><span data-api-tag="require|QyBBwN">必选</span> `Sample value: name1`

The name of the Skills space. Value:


* A maximum of 64 characters is allowed.

* Can only contain lowercase letters, numbers, and hyphens.

* Cannot contain XML tags.

* Cannot contain the reserved word "agentkit".



**Description ** <span data-label="purple">string </span>`Optional` `Sample value: description`

The description of the Skills space. Value:


* A maximum of 1,024 characters is allowed.

* Cannot contain XML tags.

* If left blank, the parameter defaults to an empty value.



**Skills ** <span data-label="purple">object[] </span>`Optional` `Sample value: --`

The Skill to be added.


**SkillId ** <span data-label="purple">string </span><span data-api-tag="require|ypgocN">必选</span> `Sample value: s-yed19lc8ow54****`

The Skill ID.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ACSGpp">必选</span> `Sample value: v1`

The Skill version number.




**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the project associated with the Skills space.



**Tags ** <span data-label="purple">object[] </span>`Optional` `Sample value: --`

The tags of the Skills space.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|T9ULTj">必选</span> `Sample value: key01`

The tag key.



**Value ** <span data-label="purple">string </span><span data-api-tag="require|beJTMb">必选</span> `Sample value: value01`

The tag value.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Id ** <span data-label="purple">string </span>`Sample value: ss-yed0d8u1ogo2****`

The ID of the Skills space.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tags of the Skills space.


**Key ** <span data-label="purple">string </span>`Sample value: key01`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: value01`

The tag value.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=CreateSkillSpace&Version=2025-10-30 HTTP/1.1
{
  "Name": "name1",
  "Description": "description",
  "Skills": [
    {
      "SkillId": "s-yed19lc8ow54****",
      "Version": "v1"
    }
  ],
  "ProjectName": "default",
  "Tags": [
    {
      "Key": "key01",
      "Value": "value01"
    }
  ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260106154054174065147****",
    "Action": "CreateSkillSpace",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Tags": [
      {
        "Key": "key01",
        "Value": "value01"
      }
    ],
    "Id": "ss-yed0d8u1ogo2****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
