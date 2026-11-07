---
title: "ModifyCommand - Modifies custom commands"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyCommand_-_Modify_custom_command"
---

Call the ModifyCommand operation to modify the content of the specified custom command.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* If a command is being executed, the command contents can also be modified. After modification, the command is executed based on the new content.

* You can configure custom parameters in the command using parameters in the `ParameterDefinitions.N.xxx` structure. The usage rules are as follows:

   * Argument \- N: indicates the serial number of the custom parameter. Valid range: 1\-60.

   * Separate multiple custom parameters with `&`.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyCommand&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|InN8yi">必选</span> `Sample value: ModifyCommand`

The action that you want to perform. Value: ModifyCommand.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|5qnasw">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**CommandId** <span data-label="purple">string</span> <span data-api-tag="require|5Q6Bcp">必选</span> `Sample value: cmd-hz0127****`

The custom command ID. You can call the [DescribeCommands](https://docs.byteplus.com/en/docs/ecs/DescribeCommands_-_Query_the_command_list) operation to query and obtain custom command IDs.



**Name** <span data-label="purple">string</span> `Optional` `Sample value: UpdateAgent`

The command name. The default value is empty, which indicates retaining the original name.


* Character length: 1–32.

* Special characters can be used.



**Type** <span data-label="purple">string</span> `Optional` `Sample value: Shell`

The command type. Supported values:


* Shell: Indicates that the script type is Shell.

* Python: Indicates that the script type is Python.

* Bat: Indicates creating a Bat script.

* PowerShell: Indicates creating a PowerShell script.



**Description** <span data-label="purple">string</span> `Optional` `Sample value: This is a description.`

The command description. The default value is empty, which indicates retaining the original description.


* Character length: 0–256.

* Special characters can be used.



**EnableParameter** <span data-label="purple">boolean</span> `Optional` `Sample value: false`

Indicates whether the created command enables the custom parameter feature. Value:


* false: Disables the custom parameter feature.

* true: Enables the custom parameter feature.



**ContentEncoding** <span data-label="purple">string</span> `Optional` `Sample value: Base64`

Specifies whether the command content is Base64 encoded. Value:


* Base64 (default): The command content is Base64 encoded.

* PlainText: The command content is not Base64 encoded.



**ParameterDefinitions.N.Name** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.Name=dir`

The parameter name, which needs to be defined in the script based on `{{Param}}`. Naming rules:


* A parameter name cannot exceed 64 bytes in length.

* Follow Shell variable naming conventions: Use combinations of lowercase letters, uppercase letters, digits, underscores, and hyphens. Cannot begin with a digit. No spaces are allowed in the middle, but underscores can be used.



**ParameterDefinitions.N.Type** <span data-label="purple">string[]</span> `Optional` `Sample value: String`

The parameter type. Value:


* String: Indicates that the custom parameter is of the `String` (string) type.

* Digit: Indicates that the custom parameter is of the `Digit` (number) type.



**ParameterDefinitions.N.Required** <span data-label="purple">boolean[]</span> `Optional` `Sample value: ParameterDefinitions.1.Required=true`

Indicates whether the parameter is required. Value:


* true: Required.

* false: Not required.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the custom parameters are required and the InvokeCommand operation is used to execute commands, custom parameter values must be passed in the <code>Parameters</code> parameter.</div>




**ParameterDefinitions.N.DefaultValue** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.DefaultValue=ecs`

The default value of the custom parameter.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pass in the default value corresponding to the parameter type specified by the <code>Type</code> parameter.</div>




**ParameterDefinitions.N.MinLength** <span data-label="purple">integer[]</span> `Optional` `Sample value: ParameterDefinitions.1.MinLength=1`

The minimum length of the custom parameter value (string).


* Value range of `MinLength`: 1~1000.

* When `Type=String`, the parameter is required, and when `Required` is set to `true`, the default value is `1`.

* The parameter value cannot exceed the value of `MaxLength`.



**ParameterDefinitions.N.MaxLength** <span data-label="purple">integer[]</span> `Optional` `Sample value: ParameterDefinitions.1.MaxLength=98`

The maximum length of the custom parameter value (string).


* Value range of` MaxLength`: 1~1000.

* When `Type=String`, the parameter is required, and when `Required` is set to `true`, the default value is `1000`.

* The parameter value needs to exceed the value of `MinLength`.



**ParameterDefinitions.N.MinValue** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.MinValue=1`

The minimum value (number) of the custom parameter.


* Value range of `MinValue`: \-1000000~1000000.

* When `Type=Digit`, the parameter is required, and when `Required` is set to `true`, the default value is `-1000000`.

* The parameter value cannot exceed the value of `MaxValue`.



**ParameterDefinitions.N.MaxValue** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.MaxValue=100`

The maximum value (number) of the custom parameter.


* Value range of `MaxValue`: \-1000000~1000000.

* When `Type=Digit`, the parameter is required, and when `Required` is set to `true`, the default value is `1000000`.

* The parameter value cannot exceed the value of `MinValue`.



**ParameterDefinitions.N.DecimalPrecision** <span data-label="purple">integer[]</span> `Optional` `Sample value: ParameterDefinitions.1.DecimalPrecision=4`

The number of decimal places allowed for the custom parameter value (number).


* Value range of `DecimalPrecision`: 0~10.

* When `Type=Digit`, the parameter is required, and when `Required` is set to `true`, the default value is `0`.



**CommandContent** <span data-label="purple">string</span> `Optional` `Sample value: IyEvYmluL2Jhc2gKZWNobyAib3BlcmF0aW9uIHN1Y2Nlc3MhIg==`

The content obtained after Base64\-encoding the command content.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Provide the corresponding command content based on the <code>ContentEncoding</code> parameter.</div>


* <div data-tips="true" data-tips-type="tip">Before coding, make sure that the first line of the script specifies the script interpreter. Rules are as follows:</div>


   * <div data-tips="true" data-tips-type="tip">Shell script: The first line needs to be <code>#!/bin/bash</code>.</div>


   * <div data-tips="true" data-tips-type="tip">Python script: The first line needs to be <code>#!/usr/bin/python</code>.</div>


* <div data-tips="true" data-tips-type="tip">The size of the command content cannot exceed 16 KB.</div>


* <div data-tips="true" data-tips-type="tip">When <code>EnableParameter=true</code>, the command content supports custom parameters. Rules are as follows:</div>


   * <div data-tips="true" data-tips-type="tip">Define the custom parameter and enclose it in <code>{{}}</code>.</div>


   * <div data-tips="true" data-tips-type="tip">Spaces and line breaks before and after the parameter name within <code>{{}}</code> are ignored.</div>




**WorkingDir** <span data-label="purple">string</span> `Optional` `Sample value: /home`

The directory in which the created command runs in the ECS instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For Linux instances, the default path is <code>/home</code>.</div>




**Username** <span data-label="purple">string</span> `Optional` `Sample value: root`

The user name when the command is executed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default user of executing a command in a Linux instance is <code>root</code>.</div>




**Timeout** <span data-label="purple">integer</span> `Optional` `Sample value: 60`

The maximum timeout duration for the created command running on the ECS instance. Unit: seconds.


* Value range: 30~86400.

* Default value: 60.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A timeout occurs when the created command cannot be executed for some reason. When the command execution times out, the command process is then stopped forcibly.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CommandId** <span data-label="purple">string</span> `Sample value: cmd-hz0127****`

The custom command ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action= ModifyCommand&Version=2020-04-01&CommandId=cmd-ydckta****&Name=demo&CommandContent=IyEvYmluL2Jhc2gKZWNobyB7e2F9fQ==&WorkingDir=/home&Username=root&Timeout=120
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
        "Action":"ModifyCommand",
        "Version":"2020-04-01",
        "Service":"ecs",
        "Region":"cn-beijing"
    },
    "Result":{
        "CommandId":"cmd-ydckta****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.MaximumName |The specified Name exceeds the limit. |The length of the specified command name exceeds the limit. |
|400 |LimitExceeded.MaximumCommandContent |The specified CommandContent exceeds the limit. |The length of the specified command content exceeds the limit. |
|400 |InvalidBase64Content.Malformed |The specified Base64 Content is malformed. |The specified Base64 content is invalid. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified command type is invalid. |
|400 |MissingParameter.CommandId |The required parameter CommandId is not supplied. |The command ID cannot be empty. |
|400 |LimitExceeded.MaximumTimeout |The specified timeout exceeds the limit. |The specified timeout period (seconds) exceeds the limit. |
|400 |LimitExceeded.MaximumDescription |The specified Description exceeds the limit. |The length of the specified command description exceeds the limit. |
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|400 |InvalidEnableParameter.Malformed |The specified EnableParameter is malformed. |The specified value of EnableParameter is invalid. |
|400 |LimitExceeded.MaximumParameterDefinitions |The specified ParameterDefinitions exceeds the limit. |The number of specified custom parameter definitions exceeds the limit. |
|400 |InvalidParameterDefinitionName.Malformed |The specified ParameterDefinition Name is malformed. The name can contain only lowercase letters (a to z), uppercase letters (A to Z), numbers (0 to 9), and underscores (_). |Invalid custom parameter name format: Allowed characters are lowercase letters, uppercase letters, digits, and underscores. The first character cannot be a digit. |
|400 |MissingParameter.ParameterDefinitionName |The required parameter ParameterDefinitionName is not supplied. |The custom parameter name cannot be empty. |
|400 |LimitExceeded.MaximumParameterDefinitionName |The specified ParameterDefinitionName exceeds the limit. |The length of the specified custom parameter name exceeds the limit. |
|400 |InvalidParameterDefinitionType.Malformed |The specified ParameterDefinition Type is malformed. |The custom parameter type is invalid. |
|400 |InvalidParameterDefinitions.Malformed |The specified ParameterDefinitions is malformed. |The specified parameter definition is invalid. |
|404 |InvalidCommand.NotFound |The specified Command does not exist. |The specified command does not exist. |
|404 |InvalidParameterDefinitions.NotFound |The specified ParameterDefinitions does not exist. |The definition of the specified custom parameter does not exist. |
|409 |InvalidParameterDefinitions.Conflict |The specified ParameterDefinition already exists. |The specified custom parameter already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again. If multiple attempts fail, submit a ticket. |
