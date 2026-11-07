---
title: "GetSharingSkillVersion - Queries preset Skill version details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetSharingSkillVersion_-_Queries_preset_Skill_version_details"
---

Query preset Skill version details.

<span id="JJ9S4BWY"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://www.volcengine.com/docs/6369/67268).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|3j7RPE">必选</span> `Sample value: GetSharingSkillVersion`

The action that you want to perform. Value: GetSharingSkillVersion.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ESLG36">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string</span><span data-api-tag="require|WAxCbR">必选</span>  `Sample value: s-yed19lc8ow54****`

The ID of Skill.



**SkillVersion ** <span data-label="purple">string </span>`Optional` `Sample value: v1`

The Skill version number. If this parameter is not provided, the latest version number is returned by default.



&nbsp;

<span id="fzgTLUdJ"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://www.volcengine.com/docs/6369/80336).



**Id ** <span data-label="purple">string </span>`Sample value: s-yed19lc8ow54****`

Skill ID.



**Name ** <span data-label="purple">string </span>`Sample value: name1`

The Skill name.



**Status ** <span data-label="purple">string </span>`Sample value: creating`

The version status of the Skill. Value:


* creating: Being created.

* running: Running.

* failed: Unavailable. This indicates a version creation failure.



**Description ** <span data-label="purple">string </span>`Sample value: description1`

The description of the Skill.



**Version ** <span data-label="purple">string </span>`Sample value: v1`

The Skill version number.



**CreateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The creation time of the Skill (Unix timestamp format).



**UpdateTimeStamp ** <span data-label="purple">string </span>`Sample value: 1767528835`

The update time of the Skill (Unix timestamp format).



**SkillMd ** <span data-label="purple">string </span>`Sample value: --`

Details for the markdown file of the Skill.



**TosPath ** <span data-label="purple">string </span>`Sample value: https://agentkit-platform.tos-ap-southeast-1.****.com/uploads/***/***.zip`

The address of the Skill.md ZIP file in TOS.



**BucketName ** <span data-label="purple">string </span>`Sample value: agentkit-platform-534***`

The name of the TOS bucket where the Skill.md ZIP file is stored.



&nbsp;

<span id="TMecoPiL"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetSharingSkillVersion&Version=2025-10-30 HTTP/1.1
{
  "Id": "s-yed19lc8ow54****",
  "SkillVersion": "v1"
}
```


<span id="61AFsXYu"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202601061745471311871****",
    "Action": "GetSharingSkillVersion",
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
    "TosPath": "https://agentkit-platform.tos-ap-southeast-1.****.com/uploads/test/test.zip",
    "BucketName": "agentkit-platform-534***"
  }
}
```


<span id="wGkLRSIB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://www.volcengine.com/docs/86681/1913777).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is invalid. |The request parameter value is invalid. Verify the parameter value and try again. |
|404 |ResourceNotFound |The specified resource cannot be found. |The corresponding resource cannot be found. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |
