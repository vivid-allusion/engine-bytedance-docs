---
title: "GetSkillInfo - Queries the version details of a Skill added to a Skills space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetSkillInfo_-_Queries_the_version_details_of_a_Skill_added_to_a_Skills_space"
---

Query the version details of Skill added to a Skills space.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|UUt4Dg">必选</span> `Sample value: GetSkillInfo`

The action that you want to perform. Value: GetSkillInfo.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|qK8Iuo">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**SkillName ** <span data-label="purple">string </span><span data-api-tag="require|WUYIRn">必选</span> `Sample value: name1`

The Skill name.



**SkillSpaceId ** <span data-label="purple">string </span><span data-api-tag="require|mDzq2W">必选</span> `Sample value: ss-yedd6r***`

The ID of the Skills space.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**BucketName ** <span data-label="purple">string </span>`Sample value: agentkit-platform-cn-beijing-2100136406-skill`

The name of the TOS bucket where the Skill.md ZIP file is stored.



**SkillName ** <span data-label="purple">string </span>`Sample value: name1`

The Skill name.



**Description ** <span data-label="purple">string </span>`Sample value: description`

The Skill description.



**SkillMd ** <span data-label="purple">string </span>`Sample value: --`

Details for the markdown file of the Skill.



**TosPath ** <span data-label="purple">string </span>`Sample value: skills/s-yedf09cutcy6pmyadwtc/v1/algorithmic-art.zip`

The address of the Skill.md ZIP file in TOS.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetSkillInfo&Version=2025-10-30 HTTP/1.1
{
  "SkillName": "name1",
  "SkillSpaceId": "ss-yedd6r***"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601061857461902120992****",
    "Action": "GetSkillInfo",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "SkillName": "name1",
    "Description": "description",
    "SkillMd": "# PDF Processing\n\n## Quick start\n\nExtract text with pdfplumber:\n[code example]\n\n## Advanced features\n\n- **Form filling**: See [FORMS.md](FORMS.md) for complete guide\n- **API reference**: See [REFERENCE.md](REFERENCE.md) for all methods\n- **Examples**: See [EXAMPLES.md](EXAMPLES.md) for common patterns",
    "TosPath": "skills/test.zip",
    "BucketName": "agentkit-platform-1234"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
