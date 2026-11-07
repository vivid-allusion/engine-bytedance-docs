---
title: "DescribeCommands - Queries command lists"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeCommands_-_Query_the_command_list"
---

Call the DescribeCommands operation to query the command list.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCommands&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|nEnQEx">必选</span> `Sample value: DescribeCommands`

The action that you want to perform. Value: DescribeCommands.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|bOPYGB">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**TagFilters.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Key=k1`

The specified tag key when querying resources based on tags.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with ampersands (&).

* Tag keys must be unique.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: default`

The project to which the resource belongs. A resource can only belong to one project.



**Provider** <span data-label="purple">string</span> `Optional` `Sample value: Volcengine`

Used to query all commands of different types. Value:


* Volcengine: Queries all public commands provided by BytePlus.

* By default, when no value is provided, all custom commands manually created by the user are queried.



**CommandId** <span data-label="purple">string</span> `Optional` `Sample value: cmd-hz012yr52****`

The command ID.



**Name** <span data-label="purple">string</span> `Optional` `Sample value: updateAgent`

The command name.



**Type** <span data-label="purple">string</span> `Optional` `Sample value: Shell`

The command type. Value:


* Shell: The command to be queried is of the Shell type.

* Python: The command to be queried is of the Python type.



**Order** <span data-label="purple">string</span> `Optional` `Sample value: created_at`

The sorting method for the returned commands. Value:


* created_at: Sorted by creation time in descending order.

* name: Sorted by command name in alphabetical order.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Public commands: Sorted by <code>name</code> by default.</div>


* <div data-tips="true" data-tips-type="tip">Custom commands: Sorted by <code>created_at</code> by default. You can sort by the name column (in alphabetical order) or the creation time column.</div>




**ContentEncoding** <span data-label="purple">string</span> `Optional` `Sample value: Base64`

Specifies whether the command content is Base64\-encoded. Value:


* PlainText: The command content is not Base64 encoded.

* Base64: The command content is Base64 encoded.



**PageNumber** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**PageSize** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1~100.

* Default value: 10.



**TagFilters.N.Values.N** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The specified tag value when querying resources based on tags.


* The first N: specifies the serial number of the tag key. Value range: 1–10.

* The second N: specifies the serial number of the tag value. Value range: 1–3. You can query up to three tag values of the same tag key.

* Separate multiple key values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in this parameter, all tag values under the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize** <span data-label="purple">integer</span> `Sample value: 1`

The number of commands returned per page.



**PageNumber** <span data-label="purple">integer</span> `Sample value: 10`

The page number of the command list.



**TotalCount** <span data-label="purple">integer</span> `Sample value: 4`

The total number of commands.



**Commands** <span data-label="purple">object[]</span> `Sample value: --`

Information about commands that meet the criteria.


**Name** <span data-label="purple">string</span> `Sample value: Install Cloud Monitor Agent`

The command name.



**CommandId** <span data-label="purple">string</span> `Sample value: cmd-hz012yr52****`

The command ID.



**CreatedAt** <span data-label="purple">string</span> `Sample value: 2023-06-07T06:58:05Z`

Creation time.



**UpdatedAt** <span data-label="purple">string</span> `Sample value: 2023-06-07T06:58:05Z`

Update time.



**Type** <span data-label="purple">string</span> `Sample value: Shell`

The command type.



**Timeout** <span data-label="purple">integer</span> `Sample value: 60`

The timeout period.



**WorkingDir** <span data-label="purple">string</span> `Sample value: /home`

The command execution path.



**Username** <span data-label="purple">string</span> `Sample value: root`

The user executing the command.



**Description** <span data-label="purple">string</span> `Sample value: This is a command description.`

The description of the command.



**Provider** <span data-label="purple">string</span> `Sample value: BytePlus`

The provider of the public command. Value: Volcengine.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Volcengine: The provider is BytePlus.</div>


* <div data-tips="true" data-tips-type="tip">For custom commands, the returned value of the parameter is empty.</div>




**CommandContent** <span data-label="purple">string</span> `Sample value: IyEvYmluL2Jhc2****c3N3b3JkfX0iIHwgY2hwYXNzd2Q=`

The content after Base64 and URL encoding.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The returned command content is encoded in the format specified by the <code>ContentEncoding</code> request parameter.</div>




**EnableParameter** <span data-label="purple">boolean</span> `Sample value: false`

Indicates whether the command enables the custom parameter feature. Value:


* false: Not enabled.

* true: Enabled.



**ParameterDefinitions** <span data-label="purple">object[]</span> `Sample value: --`

The list of the custom parameters with detailed information (JSON format).


**Name** <span data-label="purple">string</span> `Sample value: Param`

The custom parameter name.



**Type** <span data-label="purple">string</span> `Sample value: String`

The custom parameter type. Value:


* String: Indicates that the custom parameter is of the `String` (string) type.

* Digit: Indicates that the custom parameter is of the `Digit` (number) type.



**Required** <span data-label="purple">boolean</span> `Sample value: true`

Indicates whether the parameter is required. Value:


* true: Required.

* false: Not required.



**DefaultValue** <span data-label="purple">string</span> `Sample value: DefaultValue`

The default value of the custom parameter.



**MinLength** <span data-label="purple">integer</span> `Sample value: 1`

The minimum length of the custom parameter value (string).



**MaxLength** <span data-label="purple">integer</span> `Sample value: 50`

The maximum length of the custom parameter value (string).



**MinValue** <span data-label="purple">string</span> `Sample value: 10`

The minimum value (number) of the custom parameter.



**MaxValue** <span data-label="purple">string</span> `Sample value: 100`

The maximum value (number) of the custom parameter.



**DecimalPrecision** <span data-label="purple">integer</span> `Sample value: 2`

The number of decimal places allowed for the custom parameter value (number).


&nbsp;


**Name** <span data-label="purple">string</span> `Sample value: Param`

The custom parameter name.



**Type** <span data-label="purple">string</span> `Sample value: String`

The custom parameter type. Value:


* String: Indicates that the custom parameter is of the `String` (string) type.

* Digit: Indicates that the custom parameter is of the `Digit` (number) type.



**Required** <span data-label="purple">boolean</span> `Sample value: true`

Indicates whether the parameter is required. Value:


* true: Required.

* false: Not required.



**DefaultValue** <span data-label="purple">string</span> `Sample value: DefaultValue`

The default value of the custom parameter.



**MinLength** <span data-label="purple">integer</span> `Sample value: 1`

The minimum length of the custom parameter value (string).



**MaxLength** <span data-label="purple">integer</span> `Sample value: 50`

The maximum length of the custom parameter value (string).



**MinValue** <span data-label="purple">string</span> `Sample value: 10`

The minimum value (number) of the custom parameter.



**MaxValue** <span data-label="purple">string</span> `Sample value: 100`

The maximum value (number) of the custom parameter.



**DecimalPrecision** <span data-label="purple">integer</span> `Sample value: 2`

The number of decimal places allowed for the custom parameter value (number).




**InvocationTimes** <span data-label="purple">integer</span> `Sample value: 10`

The number of times the command is invoked.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The number of times a public command is invoked is not returned.</div>




**ProjectName** <span data-label="purple">string</span> `Sample value: default`

The associated project.



**Tags** <span data-label="purple">object[]</span> `Sample value: --`

The tag.


**Key** <span data-label="purple">string</span> `Sample value: Key1`

The tag name.



**Value** <span data-label="purple">string</span> `Sample value: Value1`

The tag value.



&nbsp;


**Name** <span data-label="purple">string</span> `Sample value: Install Cloud Monitor Agent`

The command name.



**CommandId** <span data-label="purple">string</span> `Sample value: cmd-hz012yr52****`

The command ID.



**CreatedAt** <span data-label="purple">string</span> `Sample value: 2023-06-07T06:58:05Z`

Creation time.



**UpdatedAt** <span data-label="purple">string</span> `Sample value: 2023-06-07T06:58:05Z`

Update time.



**Type** <span data-label="purple">string</span> `Sample value: Shell`

The command type.



**Timeout** <span data-label="purple">integer</span> `Sample value: 60`

The timeout period.



**WorkingDir** <span data-label="purple">string</span> `Sample value: /home`

The command execution path.



**Username** <span data-label="purple">string</span> `Sample value: root`

The user executing the command.



**Description** <span data-label="purple">string</span> `Sample value: This is a command description.`

The description of the command.



**Provider** <span data-label="purple">string</span> `Sample value: BytePlus`

The provider of the public command. Value: Volcengine.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Volcengine: The provider is BytePlus.</div>


* <div data-tips="true" data-tips-type="tip">For custom commands, the returned value of the parameter is empty.</div>




**CommandContent** <span data-label="purple">string</span> `Sample value: IyEvYmluL2Jhc2****c3N3b3JkfX0iIHwgY2hwYXNzd2Q=`

The content after Base64 and URL encoding.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The returned command content is encoded in the format specified by the <code>ContentEncoding</code> request parameter.</div>




**EnableParameter** <span data-label="purple">boolean</span> `Sample value: false`

Indicates whether the command enables the custom parameter feature. Value:


* false: Not enabled.

* true: Enabled.



**ParameterDefinitions** <span data-label="purple">object[]</span> `Sample value: --`

The list of the custom parameters with detailed information (JSON format).


**Name** <span data-label="purple">string</span> `Sample value: Param`

The custom parameter name.



**Type** <span data-label="purple">string</span> `Sample value: String`

The custom parameter type. Value:


* String: Indicates that the custom parameter is of the `String` (string) type.

* Digit: Indicates that the custom parameter is of the `Digit` (number) type.



**Required** <span data-label="purple">boolean</span> `Sample value: true`

Indicates whether the parameter is required. Value:


* true: Required.

* false: Not required.



**DefaultValue** <span data-label="purple">string</span> `Sample value: DefaultValue`

The default value of the custom parameter.



**MinLength** <span data-label="purple">integer</span> `Sample value: 1`

The minimum length of the custom parameter value (string).



**MaxLength** <span data-label="purple">integer</span> `Sample value: 50`

The maximum length of the custom parameter value (string).



**MinValue** <span data-label="purple">string</span> `Sample value: 10`

The minimum value (number) of the custom parameter.



**MaxValue** <span data-label="purple">string</span> `Sample value: 100`

The maximum value (number) of the custom parameter.



**DecimalPrecision** <span data-label="purple">integer</span> `Sample value: 2`

The number of decimal places allowed for the custom parameter value (number).


&nbsp;


**Name** <span data-label="purple">string</span> `Sample value: Param`

The custom parameter name.



**Type** <span data-label="purple">string</span> `Sample value: String`

The custom parameter type. Value:


* String: Indicates that the custom parameter is of the `String` (string) type.

* Digit: Indicates that the custom parameter is of the `Digit` (number) type.



**Required** <span data-label="purple">boolean</span> `Sample value: true`

Indicates whether the parameter is required. Value:


* true: Required.

* false: Not required.



**DefaultValue** <span data-label="purple">string</span> `Sample value: DefaultValue`

The default value of the custom parameter.



**MinLength** <span data-label="purple">integer</span> `Sample value: 1`

The minimum length of the custom parameter value (string).



**MaxLength** <span data-label="purple">integer</span> `Sample value: 50`

The maximum length of the custom parameter value (string).



**MinValue** <span data-label="purple">string</span> `Sample value: 10`

The minimum value (number) of the custom parameter.



**MaxValue** <span data-label="purple">string</span> `Sample value: 100`

The maximum value (number) of the custom parameter.



**DecimalPrecision** <span data-label="purple">integer</span> `Sample value: 2`

The number of decimal places allowed for the custom parameter value (number).




**InvocationTimes** <span data-label="purple">integer</span> `Sample value: 10`

The number of times the command is invoked.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The number of times a public command is invoked is not returned.</div>




**ProjectName** <span data-label="purple">string</span> `Sample value: default`

The associated project.



**Tags** <span data-label="purple">object[]</span> `Sample value: --`

The tag.


**Key** <span data-label="purple">string</span> `Sample value: Key1`

The tag name.



**Value** <span data-label="purple">string</span> `Sample value: Value1`

The tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action= DescribeCommands&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"2023082515303301022514515207C4****",
        "Action":"DescribeCommands",
        "Version":"2020-04-01",
        "Service":"ecs",
        "Region":"cn-beijing"
    },
    "Result":{
         "pageNumber": 1,
        "pageSize": 10,
        "totalCount": 19,
        "commands": [
            {
                "name": "demo",
                "commandId": "cmd-ycms****",
                "createdAt": "2023-08-30T08:42:56Z",
                "updatedAt": "2023-08-30T08:42:56Z",
                "type": "Shell",
                "timeout": 60,
                "workingDir": "/home",
                "username": "root",
                "description": "",
                "provider": "",
                "commandContent": "***",
                "enableParameter": false,
                "parameterDefinitions": [],
                "invocationTimes": 0
            }]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified command type is invalid. |
|400 |InvalidOrder.Malformed |The specified Order is malformed. |The specified sorting method is invalid. |
|400 |LimitExceeded.TagFilterKeys |You've reached the limit on the number of TagFilter Keys that you can set. |The upper limit of the number of tag filter keys is reached. |
|400 |MissingParameter.TagKey |The required parameter TagFiltersKey is not supplied. |The tag filter key is required. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|409 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |The specified tag filter key already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
