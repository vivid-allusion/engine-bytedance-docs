---
title: "CreateCommand - Creates custom commands"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CreateCommand-Creating_a_custom_command"
---

Call the CreateCommand operation to create a custom command.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

You can configure the custom parameters in the command via the `ParameterDefinitions.N.xxx` parameters. The usage rules are as follows:


* Argument \- N: indicates the serial number of the custom parameter. Valid range: 1\-60.

* Separate multiple custom parameters with `&`.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateCommand&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|SMWQse">必选</span> `Sample value: CreateCommand`

The action that you want to perform. Value: CreateCommand.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|bHhtGC">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**Tags.N.Value** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The value of the user tag.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple key values with ampersands (&).


Naming rules:


* Only language characters, digits, spaces, and English symbols of " _", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It can be empty. Length limit: 0–256 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: default`

The associated project. Each instance can only belong to one project.



**Tags.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The key of the user tag.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple keys with ampersands (&).


Naming rules:


* It cannot start with `volc:` or `sys:` in any case form.

* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Name** <span data-label="purple">string</span> <span data-api-tag="require|a8BxzQ">必选</span> `Sample value: updateAgent`

The command name. Naming rules are as follows:


* Character length: 1–32.

* Special characters can be used.



**Description** <span data-label="purple">string</span> `Optional` `Sample value: This is a new command.`

The command description. Default value: empty string.


* Character length: 0–256.

* Special characters can be used.



**Type** <span data-label="purple">string</span> <span data-api-tag="require|k2RzLl">必选</span> `Sample value: Shell`

The command type. Value:


* Shell: Indicates creating a Shell script that runs in a Linux instance.

* Python: Indicates creating a Python script.

* Bat: Indicates creating a Bat script.

* PowerShell: Indicates creating a PowerShell script.



**EnableParameter** <span data-label="purple">boolean</span> `Optional` `Sample value: false`

Indicates whether the created command enables the custom parameter feature. Value:


* false (default): Disables the custom parameter feature.

* True: Enables the custom parameter feature.



**ParameterDefinitions.N.Name** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.Name=dir`

The parameter name, which needs to be defined in the script based on {{Param}}. Naming rules:


* A parameter name can not exceed 64 bytes in length.

* Follow Shell variable naming conventions: Use lowercase letters, uppercase letters, digits, underscores, and hyphens. Cannot begin with a digit. No spaces are allowed in the middle. Underscores can be used.



**ParameterDefinitions.N.Type** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.Type=String`

The custom parameter type. Value:


* String: Indicates that the custom parameter is of the `String` (string) type.

* Digit: Indicates that the custom parameter is of the `Digit` (numeric type) type.



**ParameterDefinitions.N.Required** <span data-label="purple">boolean[]</span> `Optional` `Sample value: ParameterDefinitions.1.Required=true`

Indicates whether the parameter is required. Value:


* true: Required.

* false: Not required.



**ParameterDefinitions.N.DefaultValue** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.DefaultValue=ecs`

The default value of the custom parameter.



**ParameterDefinitions.N.MinLength** <span data-label="purple">integer[]</span> `Optional` `Sample value: ParameterDefinitions.1.MinLength=1`

The minimum length of the custom parameter value (string).


* Value range of `MinLength`: 1~1000.

* When `Type=String`, the parameter is required, and when `Required` is set to `true`, the default value is `1`.

* The parameter value needs to be smaller than the value of `MaxLength`.



**ParameterDefinitions.N.MaxLength** <span data-label="purple">integer[]</span> `Optional` `Sample value: ParameterDefinitions.1.MaxLength=98`

The maximum length of the custom parameter value (string).


* Value range of `MaxLength`: 1~1000.

* When `Type=String`, the parameter is required, and when `Required` is set to `true`, the default value is `1000`.

* The parameter value needs to exceed the value of `MinLength`.



**ParameterDefinitions.N.MinValue** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.MinValue=1`

The minimum value (number) of the custom parameter.


* Value range of `MinValue`: \-1000000~1000000.

* When `Type=Digit`, the parameter is required, and when `Required` is set to `true`, the default value is `-1000000`.

* The parameter value cannot exceed the value of `MaxValue`



**ParameterDefinitions.N.MaxValue** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.MaxValue=100`

The maximum value (number) of the custom parameter.


* Value range of `MaxValue`: \-1000000~1000000.

* When `Type=Digit`, the parameter is required, and when `Required` is set to `true`, the default value is `1000000`.

* The parameter value cannot exceed the value of `MinValue`.



**ParameterDefinitions.N.DecimalPrecision** <span data-label="purple">integer[]</span> `Optional` `Sample value: ParameterDefinitions.1.DecimalPrecision=4`

The number of decimal places allowed for the custom parameter value (number).


* Value range of `DecimalPrecision`: 0~10.

* When `Type=Digit`, the parameter is required, and when `Required` is set to `true`, the default value is `0`.



**CommandContent** <span data-label="purple">string</span> <span data-api-tag="require|ZhPD8D">必选</span> `Sample value: IyEvYmluL2Jhc2gKZWNobyAib3BlcmF0aW9uIHN1Y2Nlc3MhIg==`

The command content.


* Provide the corresponding command content based on the `ContentEncoding` parameter.

* Before coding, make sure that the first line of the script specifies the script interpreter. The rules are as follows:

   * Shell script: The first line needs to be `#!/bin/bash`.

   * Python script: The first line needs to be `#!/usr/bin/python`.

* The size of the command content must not exceed 16 KB.

* When `EnableParameter=true`, the command content supports custom parameters. Rules are as follows:

   * Define the custom parameter and enclose it in `{{}}`.

   * Spaces and line breaks before and after the parameter name within `{{}}` are ignored.



**WorkingDir** <span data-label="purple">string</span> `Optional` `Sample value: /home`

The directory where the created command runs on the ECS instance. For Linux instances, the default value is `/home`.



**Username** <span data-label="purple">string</span> `Optional` `Sample value: root`

The user name when the command is executed.



**Timeout** <span data-label="purple">integer</span> `Optional` `Sample value: 60`

The maximum timeout duration for the created command running on the ECS instance. Unit: **seconds**.


* Value range: 30~86400.

* Default value: 60.



**ContentEncoding** <span data-label="purple">string</span> `Optional` `Sample value: Base64`

Specifies whether the command content is Base64 encoded. Value:


* Base64 (default): The command content is Base64 encoded.

* PlainText: The command content is not Base64 encoded.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CommandId** <span data-label="purple">string</span> `Sample value: cmd-ycgpkuavyrm0tq****`

The custom command ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CreateCommand&Version=2020-04-01&Name=demo&Description=123&Type=Shell&EnableParameter=true&ParameterDefinitions.1.Name=a&ParameterDefinitions.1.Description=desc&ParameterDefinitions.1.Required=true&ParameterDefinitions.1.Required=true&ParameterDefinitions.1.DefaultValue=123&ParameterDefinitions.1.Type=String&ParameterDefinitions.1.MaxLength=1000&ParameterDefinitions.1.MinLength=1&CommandContent=IyEvYmluL2Jhc2gKZWNobyB7e2F9fQ==&WorkingDir=/home&Username=root&Timeout=60
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
        "Action":"CreateCommand",
        "Version":"2020-04-01",
        "Service":"ecs",
        "Region":"cn-beijing"
    },
    "Result":{
        "CommandId":"cmd-shhrh****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.CommandContent |The required parameter CommandContent is not supplied. |The command content cannot be empty. |
|400 |MissingParameter.Type |The required parameter Type is not supplied. |The command type cannot be empty. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of Tags that you can create. |The upper limit of tags that you can create is reached. |
|400 |InvalidProjects.ListFailed |Fail to list projects. |Failed to fetch the specified project. |
|400 |InvalidParameterDefinitions.Malformed |The specified ParameterDefinitions is malformed. |The specified parameter definition is invalid. |
|400 |InvalidEnableParameter.Malformed |The specified EnableParameter is malformed. |The specified value of EnableParameter is invalid. |
|400 |QuotaExceeded.MaximumCommands |You've reached the limit on the number of Commands that you can create, please submit ticket to request an increase in quota. |The custom command quota is insufficient. Please submit a ticket to request a quota increase. |
|400 |InvalidParameterDefinitionType.Malformed |The specified ParameterDefinition Type is malformed. |The custom parameter type is invalid. |
|400 |LimitExceeded.MaximumParameterDefinitionName |The specified ParameterDefinitionName exceeds the limit. |The length of the specified custom parameter name exceeds the limit. |
|400 |MissingParameter.ParameterDefinitionName |The required parameter ParameterDefinitionName is not supplied. |The custom parameter name cannot be empty. |
|400 |InvalidParameterDefinitionName.Malformed |The specified ParameterDefinition Name is malformed. The name can contain only lowercase letters (a to z), uppercase letters (A to Z), numbers (0 to 9), and underscores (_). |Invalid custom parameter name format: Allowed characters are lowercase letters, uppercase letters, and underscores. The first character cannot be a digit. |
|400 |LimitExceeded.MaximumParameterDefinitions |The specified ParameterDefinitions exceeds the limit. |The number of specified custom parameter definitions exceeds the limit. |
|400 |MissingParameter.ParameterDefinitions |The required parameter ParameterDefinitions is not supplied. |The parameter definition cannot be left empty. |
|400 |LimitExceeded.MaximumCommandContent |The specified CommandContent exceeds the limit. |The length of the specified command content exceeds the limit. |
|400 |InvalidBase64Content.Malformed |The specified Base64 Content is malformed. |The specified Base64 content is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |LimitExceeded.MaximumTimeout |The specified timeout exceeds the limit. |The specified timeout period (s) exceeds the limit. |
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified command type is invalid. |
|400 |MissingParameter.Name |The required parameter Name is not supplied. |The command name cannot be empty. |
|400 |LimitExceeded.MaximumName |The specified Name exceeds the limit. |The length of the specified command name exceeds the limit. |
|400 |LimitExceeded.MaximumDescription |The specified Description exceeds the limit. |The length of the specified command description exceeds the limit. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidParameterDefinitions.NotFound |The specified ParameterDefinitions does not exist. |The definition of the specified custom parameter does not exist. |
|404 |MissingParameter.Tags |The required parameter Tags are empty. |The tag parameter cannot be empty. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|409 |InvalidParameterDefinitions.Conflict |The specified ParameterDefinition already exists. |The specified custom parameter already exists. |
