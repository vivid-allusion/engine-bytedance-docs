---
title: "ListTools - Batch queries tool details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListTools_-_Batch_queries_tool_details"
---

You can batch query tool details using custom filter conditions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|NkDGFX">必选</span> `Sample value: ListTools`

The action that you want to perform. Value: ListTools.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|b2iKXd">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**CreateTimeAfter ** <span data-label="purple">string </span>`Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter tools created after this time point. (RFC3339 format)



**CreateTimeBefore ** <span data-label="purple">string </span>`Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter tools created before this time point. (RFC3339 format)



**Filters.N.Name ** <span data-label="purple">string[] </span>`Optional Sample value: Name`

Field name used for exact filtering. Value: 


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Valid values:

   * Id: Tool ID.

   * Name: Tool name.

   * Description: Tool description.

   * Status: Tool status.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.NameContains ** <span data-label="purple">string[] </span>`Optional Sample value: Status`

Field name used for fuzzy filtering. Values: 


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Valid values:

   * Id: Tool ID.

   * Name: Tool name.

   * Description: Tool description.

   * Status: Tool status.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.Values.N ** <span data-label="purple">string[]</span>` Optional Sample value: Ready`

Value of the filter field.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&).


When the filter field is Status, the values are:


* Creating: Being created.

* Error: An error occurred.

* Ready: Running.

* Deleting: Being deleted.

* Updating: Being updated.



**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Minimum value: 1.

* Maximum value: 100. 

* Default value: 100.



**NextToken ** <span data-label="purple">string </span>`Optional Sample value: unique-token`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**UpdateTimeAfter ** <span data-label="purple">string </span>`Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter tools updated before this time point. (RFC3339 format)



**UpdateTimeBefore ** <span data-label="purple">string</span>` Optional Sample value: 2006-01-02T15:04:05Z07:00`

Filter tools updated before this time point. (RFC3339 format)



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the associated project.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Key=k1`

Add tag keys to the resource.


* Parameter \- N specifies the serial number of the tag key.

* Valid range: 1–10, with multiple tag keys separated by ampersands (&).

* Duplicates are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">string[]</span>` Optional Sample value: TagFilters.1.Values.1=v1`

Add tag keys to the resource.


* The first N specifies the serial number of the tag key. Value range: 1–10.

* The second N specifies the serial number of the tag value. Value range: 1–3. You can query up to three tag values for the same tag key .

* Separate multiple tag values with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in TagFilters.N.Key first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in this parameter, all tag values under the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken ** <span data-label="purple">string </span>`Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The pagination token returned by this call. If this value is empty, the current page is the last page.



**Tools ** <span data-label="purple">object[] </span>`Sample value: --`

Information of the tools that meet the condition.


**ApmplusEnable ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to enable TLS. Valid values:


* true: Enabled.

* false: Disabled.



**AuthorizerConfiguration ** <span data-label="purple">object </span>`Sample value: --`

The inbound identity authentication information of the tool. Currently, API Key authentication configuration is supported.


**KeyAuth ** <span data-label="purple">object </span>`Sample value: --`

API Key authentication configuration.


**ApiKey ** <span data-label="purple">string </span>`Sample value: 22243eefff**`

The value of the API Key.



**ApiKeyLocation ** <span data-label="purple">string </span>`Sample value: header`

The location where the API Key is passed. Valid values:


* Header: Currently, only Header is supported.



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



**EnableSnapshot ** <span data-label="purple">boolean </span>`Sample value: true`

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

Tool access information.


**Endpoint ** <span data-label="purple">string </span>`Sample value: http://sd3qupshmeps3v7l9****.apigateway-ap-southeast-1.volceapi.com`

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



**RoleName ** <span data-label="purple">string </span>`Sample value: MyTestRole`

The name of the IAM role associated with the tool.



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



**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Update time of the tool.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListTools&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "Filters": [
        {
            "Name": "Name",
            "Values": [
                ""
            ]
        }
    ]
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "ListTools",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Tools": [
      {
        "ToolId": "t-ye9qwatywwb6wrvc****",
        "Name": "test-name",
        "Description": "",
        "Status": "Ready",
        "ToolType": "All-in-one",
        "AuthorizerConfiguration": {
          "KeyAuth": {
            "ApiKey": "",
            "ApiKeyLocation": "header",
            "ApiKeyName": "test-api-key"
          },
        },
        "RoleName": "",
        "CreatedAt": "2025-11-23T16:55:21+08:00",
        "UpdatedAt": "2025-11-23T16:55:29+08:00",
        "Tags": [],
        "ImageUrl": "enterprise-ap-southeast-1.cr.volces.com/vefaas-public/all-in-one-sandbox:1.0.0.126",
        "Command": "/opt/gem/run.sh",
        "Port": 8080,
        "Envs": [],
        "ProjectName": "default",
        "ApmplusEnable": false,
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
    ],
    "NextToken": "dC15ZTdjZ2xlM3VvYzFrZHRvcn****=="
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.MaximumFilters |The number of specified Filters exceeds the maximum limit. |The specified Filters exceeds the upper limit. |
|400 |InvalidTagFilterKey.Malformed |The specified TagFilterKey is malformed. |The specified TagFilterKey is invalid. |
