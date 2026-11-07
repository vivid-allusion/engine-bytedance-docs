---
title: "GetTool - Queries tool details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetTool_-_Queries_tool_details"
---

You can call this operation to query tool details.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|wYpln1">必选</span> `Sample value: GetTool`

The action that you want to perform. Value: GetTool.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|eV9j8e">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**ToolId ** <span data-label="purple">string </span><span data-api-tag="require|Z6IV2t">必选</span> `Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CpuMilli ** <span data-label="purple">integer </span>`Sample value: 1000`

Maximum CPU per instance. Unit: milli cpu.



**MemoryMb ** <span data-label="purple">integer </span>`Sample value: 2048`

Maximum memory per instance, in MB.



**ApmplusEnable ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to enable TLS. Valid values:


* true: Enabled.

* false: Disabled.



**AssociatedRuntimes ** <span data-label="purple">object[] </span>`Sample value: --`

Agent runtimes associated with the tool.


**Id ** <span data-label="purple">string </span>`Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



**Name ** <span data-label="purple">string </span>`Sample value: runtime-01`

Runtime name.




**AuthorizerConfiguration ** <span data-label="purple">object </span>`Sample value: --`

The inbound identity authentication information of the tool. Currently, API Key authentication configuration is supported.


**CustomJwtAuthorizer ** <span data-label="purple">object</span>

The information about inbound authentication using the CustomJWTAuthorizer method.


**AllowedClients ** <span data-label="purple">string[]</span>

The list of allowed clients.



**DiscoveryUrl ** <span data-label="purple">string</span>

The authentication service address.




**KeyAuth ** <span data-label="purple">object </span>`Sample value: --`

API Key authentication configuration.


**ApiKey ** <span data-label="purple">string </span>`Sample value: 22243eefff**`

The value of the API Key.



**ApiKeyLocation ** <span data-label="purple">string </span>`Sample value: Header`

The location where the API Key is passed. Currently, only Header is supported.



**ApiKeyName ** <span data-label="purple">string </span>`Sample value: test-key`

API Key name.





**Command ** <span data-label="purple">string </span>`Sample value: ./run.sh`

The command to start the tool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A return value is provided only when the tool is of the custom type.</div>




**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Creation time of the tool.



**Description ** <span data-label="purple">string </span>`Sample value: this is a tool`

Description of the tool.



**EnableSnapshot ** <span data-label="purple">boolean </span>`Sample value: false`

Whether to automatically create a snapshot before the instance expires.


* true: create.

* false: not create.



**Envs ** <span data-label="purple">object[] </span>`Sample value: --`

The environment variable of the tool.


**Key ** <span data-label="purple">string </span>`Sample value: k1`

The key of the environment variable.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The value of the environment variable.




**ImageUrl ** <span data-label="purple">string </span>`Sample value: http://***`

The tool image URL.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A return value is provided only when the tool is of the custom type.</div>




**ModelAgentName ** <span data-label="purple">string </span>`Sample value: doubao-seed-1.6`

The access point for the inference model.



**Name ** <span data-label="purple">string </span>`Sample value: tool-test`

Tool name.



**NetworkConfigurations ** <span data-label="purple">object[] </span>`Sample value: --`

Access information for the tool, including public network and VPC.


**Endpoint ** <span data-label="purple">string </span>`Sample value: https://sd3p0u******.apigateway-ap-southeast-1.volceapi.com`

Domain name of the tool.



**NetworkType ** <span data-label="purple">string </span>`Sample value: public`

Access type. Value:


* public: Access using public network

* private: Access using private network



**VpcConfiguration ** <span data-label="purple">object </span>`Sample value: --`

VPC configuration.


**EnableSharedInternetAccess ** <span data-label="purple">boolean </span>`Sample value: true`

The public network egress configuration. Valid values:


* true: Enabled. This value indicates that the tool uses the public network egress provided by the platform to access the public network.

* false: Not enabled. This value indicates that the tool uses the public network NAT gateway egress configured in the private network to access the public network.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only when network access is set to Private network.</div>




**SecurityGroupIds ** <span data-label="purple">string[] </span>`Sample value: ["sg-w08tvkc3e****"]`

List of security group IDs.



**SubnetIds ** <span data-label="purple">string[] </span>`Sample value: ["subnet-1234567890"]`

List of subnet IDs.



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-257gqcdfvx6n****`

VPC ID.





**Port ** <span data-label="purple">integer </span>`Sample value: 8000`

The listening port for the tool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A return value is provided only when the tool is of the custom type.</div>




**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Name of the associated project.



**RoleName ** <span data-label="purple">string </span>`Sample value: AgentKit-Runtime-Default-ServiceRole-xbv8s36`

The name of the IAM role associated with the tool.



**SkillSpaceId ** <span data-label="purple">string </span>`Sample value: ss-yedd6rcsu8****`

The ID of the Skills space.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Tool status. Value:


* Creating: Being created.

* Error: An error occurred.

* Ready: Running.

* Deleting: Being deleted.

* Updating: Being updated.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

Tool tags.


**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Type ** <span data-label="purple">string </span>`Sample value: system`

Tag type.


* system: system tag

* custom: user tag



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**ToolId ** <span data-label="purple">string </span>`Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



**ToolType ** <span data-label="purple">string </span>`Sample value: All-in-one`

Tool type. Valid values:


* All\-in\-one: An integrated toolset, i.e., the preset tool AIO Sandbox.

* Skill: Skill tool image, which is the preset tool Skills Sandbox.

* Private: Custom tool.

* CodeEnv: preset tool Code Sandbox.



**TosMountConfig ** <span data-label="purple">object </span>`Sample value: --`

The TOS mounting configuration.


**Credentials ** <span data-label="purple">object </span>`Sample value: --`

The TOS credentials.


**AccessKeyId ** <span data-label="purple">string </span>`Sample value: GY2OGJiOTdl****`

The Access Key ID of the platform.



**SecretAccessKey ** <span data-label="purple">string </span>`Sample value: emRoTnpVNU5HU****`

The Secret Access Key ID of the platform.




**EnableTos ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to enable TOS mounting. After mounting, the data generated in the corresponding directory of the tool instance will be stored in the TOS service. Valid values:


* true: Enabled.

* false: Disabled.



**MountPoints ** <span data-label="purple">object[] </span>`Sample value: --`

The list of TOS mount points.


**BucketName ** <span data-label="purple">string </span>`Sample value: bucket01`

The TOS bucket name.



**BucketPath ** <span data-label="purple">string </span>`Sample value: http://tos-ap-southeast-1.ivolces.com`

The TOS bucket path.



**Endpoint ** <span data-label="purple">string </span>`Sample value: tmp/abc`

The TOS bucket subdirectory.



**LocalMountPath ** <span data-label="purple">string </span>`Sample value: /home/app`

The local directory of the tool instance to be mounted.



**ReadOnly ** <span data-label="purple">boolean </span>`Sample value: false`

Specify the access permission of the Sandbox tool instance to be mounted. Valid values:


* true: Read\-only permission.

* false: Read/write permissions.





**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Update time of the tool.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetTool&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "ToolId": "t-ye6xzwchkwoaroxxxxxx"
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20251027142329504394C726CC0349****",
    "Action": "GetTool",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "ToolId": "t-ye9qwatywwb6wrvc****",
    "Name": "test-name",
    "Description": "",
    "Status": "Ready",
    "ToolType": "All-in-one",
    "AuthorizerConfiguration": {
      "KeyAuth": {
        "ApiKey": "****",
        "ApiKeyLocation": "header",
        "ApiKeyName": "test-api-key"
      }
    },
    "AssociatedRuntimes": [],
    "RoleName": "",
    "CreatedAt": "2025-11-23T16:55:21+08:00",
    "UpdatedAt": "2025-11-23T16:55:29+08:00",
    "Tags": [],
    "ImageUrl": "enterprise-ap-southeast-1.cr.volces.com/vefaas-public/all-in-one-sandbox:1.0.0.126",
    "Command": "/opt/gem/run.sh",
    "Port": 8080,
    "ApmplusEnable": false,
    "Envs": [],
    "ProjectName": "default",
    "NetworkConfigurations": [
      {
        "NetworkType": "public",
        "Endpoint": "https://sd4hcnv3318ffuppa***.apigateway-ap-southeast-1.volceapi.com",
        "VpcConfiguration": {
          "VpcId": "vpc-1unjb731ek1s51j8e75l****",
          "SubnetIds": [
            "subnet-w0eiz5pvhlhc865ykakf****"
          ],
          "SecurityGroupIds": [
            "sg-1c11cukupn1ts5e8j711g****"
          ]
        }
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.ToolId |The required parameter ToolId is not supplied. |The parameter ToolId cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
