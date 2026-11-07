---
title: "UpdateTool - Modifies tool description"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UpdateTool_-_Modifies_tool_description"
---

You can call this operation to modify tool description.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|T4jGML">必选</span> `Sample value: UpdateTool`

The action that you want to perform. Value: UpdateTool.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|pTmhlR">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**Description**<span data-label="purple"> string</span>` Optional Sample value: tool01`

Description of the tool. Value: cannot exceed 1000 Unicode characters.



**ApmplusEnable**<span data-label="purple"> boolean</span>` Optional Sample value: true`

Whether to enable TLS. Valid values:


* true: Enabled.

* false: Disabled.



**ToolId ** <span data-label="purple">string </span><span data-api-tag="require|qxc2wA">必选</span> `Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



**Command ** <span data-label="purple">string </span>`optional` `Sample value: ./run.sh`

The command to start the tool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>ToolType</code> is set to Private, you need to configure this parameter. Default value: ./run.sh.</div>




**CpuMilli ** <span data-label="purple">integer </span>`Optional` `Sample value: 2000`

The vCPU specification of the instance. Unit: milli cpu.


* All\-in\-one and Skill: 2000



**Envs.N.Key ** <span data-label="purple">string[] </span><span data-api-tag="require|uDhha7">必选</span> `Sample value: Envs.1.Key=k1`

The key of the tool's environment variable.


* Parameter \- N: Specifies the serial number of the environment variable. Valid value: 1\-30.

* Value: Can only contain letters, numbers, and underscores, and start with an underscore or a letter. The length is 1 to 63 characters.



**Envs.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: Envs.1.Value=v1`

The value of the tool's environment variable.


* Parameter \- N: Specifies the serial number of the environment variable. Valid value: 1\-30.



**EnableSnapshot ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to automatically create a snapshot before the instance expires.


* true: create.

* false: not create.



**ImageUrl ** <span data-label="purple">string </span>`Optional` `Sample value: http://***`

The tool image URL.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>ToolType</code> is set to Private.</div>




**Port ** <span data-label="purple">integer </span>`optional` `Sample value: 8000`

The listening port for the tool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>ToolType</code> is set to Private, you need to configure this parameter. Default value: 8000.</div>




**ModelAgentName ** <span data-label="purple">string </span>`Optional` `Sample value: doubao-seed-1.6`

The access point for the inference model.



**ToolType ** <span data-label="purple">string </span>`Optional` `Sample value: All-in-one`

Tool type. Valid values:


* All\-in\-one: An integrated toolset, i.e., the preset tool AIO Sandbox.

* Skill: Skill tool image, which is the preset tool Skills Sandbox.

* PersonalAssistant: preset tool OpenClaw.

* Private: Custom tool.



**TosMountConfig.Credentials.AccessKeyId ** <span data-label="purple">string </span>`Optional` `Sample value: GY2OGJiOTdl****`

Enter the Access Key ID of the platform.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**MemoryMb ** <span data-label="purple">integer </span>`Optional` `Sample value: 600`

The memory specification of the instance. Unit: MiB. Valid range: 512\-131072.



**TosMountConfig.Credentials.SecretAccessKey ** <span data-label="purple">string </span>`Optional` `Sample value: emRoTnpVNU5HU****`

Enter the Secret Access Key ID of the platform.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.EnableTos ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to enable TOS mounting. After mounting, the data generated in the corresponding directory of the tool instance will be stored in the TOS service. Valid values:


* true: Enabled.

* false: Disabled.



**TosMountConfig.MountPoints.N.BucketName ** <span data-label="purple">string[] </span>`Optional` `Sample value: bucket01`

The TOS bucket name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.MountPoints.N.BucketPath ** <span data-label="purple">string[] </span>`Optional` `Sample value: http://tos-ap-southeast-1.ivolces.com`

The TOS bucket path.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.MountPoints.N.Endpoint ** <span data-label="purple">string[] </span>`Optional` `Sample value: tmp/abc`

The TOS bucket subdirectory.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.MountPoints.N.LocalMountPath ** <span data-label="purple">string[] </span>`Optional` `Sample value: /home/app`

The local directory of the tool instance to be mounted.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




**TosMountConfig.MountPoints.N.ReadOnly ** <span data-label="purple">boolean[] </span>`Optional` `Sample value: false`

The access permission for the local directory of the tool instance to be mounted. Valid values:


* true: Read\-only permission.

* false: Read/write permissions.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Required when <code>TosMountConfig.EnableTos</code> is set to true.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ToolId ** <span data-label="purple">string </span>`Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=UpdateTool&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "ToolId": "t-ye6xzwchkwoaroxxxxxx"
    "Description": "123"
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "UpdateTool",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "ToolId": "t-ye7hr4n01soarome****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format of the specified description is invalid. |
|400 |InvalidKey.Malformed |The specified Key is malformed. |The specified Key is invalid. |
|400 |InvalidModelAgentName.Malformed |The specified ModelAgentName is malformed. |The specified ModelAgentName is invalid. |
|400 |MissingParameter.Key |The required parameter Key is not supplied. |The parameter Key cannot be empty.  |
|400 |MissingParameter.ToolId |The required parameter ToolId is not supplied. |The parameter ToolId cannot be empty. |
|400 |InvalidResourceStatus |The status of the specified resource does not support this request. |The current status of the resource does not support this operation. |
|400 |InvalidParameter.Port |The specified Port is invalid. |The specified Port is invalid. |
|400 |InvalidParameter.ToolType |The specified ToolType is invalid. |The specified ToolType is invalid. |
|400 |MissingParameter.ImageUrl |The required parameter ImageUrl is not supplied. |ImageUrl cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
