---
title: "GetSkillVersion - Queries details of a Skill version"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetSkillVersion_-_Queries_details_of_a_Skill_version"
---

Query details of a Skill version.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|qejvAg">必选</span> `Sample value: GetSkillVersion`

The action that you want to perform. Value: GetSkillVersion.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|dkjujU">必选</span>  `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|PKtyhr">必选</span> `Sample value: s-yed19lc8ow54****`

The Skill ID.



**SkillVersion ** <span data-label="purple">string </span>`Optional` `Sample value: v1`

The Skill version number. If this parameter is not provided, the latest version number is returned by default.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Id ** <span data-label="purple">string </span>`Sample value: s-yed19lc8ow54****`

The Skill ID.



**Name ** <span data-label="purple">string </span>`Sample value: name1`

The Skill name.



**Status ** <span data-label="purple">string </span>`Sample value: creating`

The version status of the Skill. Value:


* creating: Being created.

* running: Running.

* failed: Unavailable. This indicates a version creation failure.



**Description ** <span data-label="purple">string </span>`Sample value: description1`

The Skill description.



**Version ** <span data-label="purple">string </span>`Sample value: v1`

The Skill version number.



**CreateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The Skill creation time (in Unix timestamp format).



**UpdateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The Skill update time (in Unix timestamp format).



**SkillMd ** <span data-label="purple">string </span>`Sample value: \# PDF Processing\n\n## Quick start\n\nExtract text with pdfplumber:\n[code example]\n\n## Advanced features\n\n- \*\*Form filling\*\*: See \[FORMS.md\]\(FORMS.md\) for complete guide\n- \*\*API reference\*\*: See \[REFERENCE.md\]\(REFERENCE.md\) for all methods\n- \*\*Examples**: See \[EXAMPLES.md\]\(EXAMPLES.md\) for common patterns`

Details for the markdown file of the Skill.



**TosPath ** <span data-label="purple">string </span>`Sample value: https://agentkit-platform.tos-cn-beijing.volces.com/uploads/***/***.zip`

The address of the Skill ZIP file in TOS.



**BucketName ** <span data-label="purple">string </span>`Sample value: agentkit-platform-534***`

The name of the TOS bucket (Bucket) where the Skill ZIP file is stored.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetSkillVersion&Version=2025-10-30 HTTP/1.1
{
  "Id": "s-yed19lc8ow54****",
  "SkillVersion": "v1"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601061745471311871****",
    "Action": "GetSkillVersion",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Id": "s-yed19lc8ow54****",
    "Name": "name1",
    "Status": "creating",
    "Description": "description1",
    "Version": "v1",
    "CreateTimeStamp": "1767528835",
    "UpdateTimeStamp": "1767528835",
    "SkillMd": "# PDF Processing\n\n## Quick start\n\nExtract text with pdfplumber:\n[code example]\n\n## Advanced features\n\n- **Form filling**: See [FORMS.md](FORMS.md) for complete guide\n- **API reference**: See [REFERENCE.md](REFERENCE.md) for all methods\n- **Examples**: See [EXAMPLES.md](EXAMPLES.md) for common patterns",
    "TosPath": "https://agentkit-platform.tos-cn-beijing.volces.com/uploads/test/test.zip",
    "BucketName": "agentkit-platform-534***"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
