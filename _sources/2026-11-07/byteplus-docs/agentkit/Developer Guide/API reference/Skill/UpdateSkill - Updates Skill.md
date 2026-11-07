---
title: "UpdateSkill - Updates Skill"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UpdateSkill_-_Updates_Skill"
---

Update a Skill.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

Ensure the Skill.md ZIP file meets the following requirements. Otherwise, the creation may fail:


* After decompression, there must be exactly one folder, and its name must be consistent with the Skill name.

* In the {skill_name} folder, SKILL.md is located in the root directory.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|BhNra8">必选</span> `Sample value: UpdateSkill`

The action that you want to perform. Value: UpdateSkill.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|1SxTFz">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|4uqqW7">必选</span> `Sampe value: s-yed19lc8ow54****`

Skill ID.



**Name ** <span data-label="purple">string </span>`Optional` `Sample value: name1`

Enter the Skill name in the Skill.md ZIP file in TOS. Valid values:


* A maximum of 64 characters is allowed.

* Only lowercase letters, numbers, and hyphens (\-) are allowed.

* It cannot contain XML tags.

* Cannot contain the reserved word "agentkit".


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you do not specify this parameter, the system automatically parses the SKILL.md file to obtain the name. If you specify this parameter, the system performs a consistency check against the SKILL.md file.</div>




**Description ** <span data-label="purple">string </span>`Optional` `Sample value: description1`

Enter the Skill name in the Skill.md ZIP file in TOS. Valid values:


* A maximum of 1,024 characters is allowed.

* It cannot contain XML tags.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you do not specify this parameter, the system automatically parses the SKILL.md file to obtain the name. If you specify this parameter, the system performs a consistency check against the SKILL.md file.</div>




**TosUrl ** <span data-label="purple">string </span><span data-api-tag="require|7apHuf">必选</span> `Sample value: https://agentkit-platform.tos-ap-southeast-1.volces.com/uploads//.zip`

The address of the Skill.md ZIP file in TOS. Format: `https://${bucket name}.${TOS domain name}/${object complete path}`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The allowed public network address or private network address of TOS, that is, <code>https://agentkit-platform.tos-ap-southeast-1.volces.com/****</code> or <code>https://agentkit-platform.tos-ap-southeast-1.ivolces.com/****</code>.</div>




**SkillSpaces ** <span data-label="purple">string[] </span>`Optional` `Sample value: ss-yed0d8u1ogo2****`

The Skills space to which the Skill is added.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=UpdateSkill&Version=2025-10-30 HTTP/1.1
{
  "Id": "s-yed19lc8ow54****",
  "Name": "name1",
  "Description": "description1",
  "TosUrl": "https://agentkit-platform.tos-ap-southeast-1.volces.com/uploads/****/****.zip",
  "SkillSpaces": [
    "ss-yed0d8u1ogo2****"
  ],
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2026010618380711206000****",
    "Action": "UpdateSkill",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more about error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).
