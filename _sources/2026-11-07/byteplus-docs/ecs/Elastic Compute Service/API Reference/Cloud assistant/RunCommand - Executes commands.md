---
title: "RunCommand - Executes commands"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/RunCommand_-_Execute_command"
---

Call the RunCommand operation to create a task by manually entering a command.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* Unlike the [CreateCommand](https://docs.byteplus.com/en/docs/ecs/CreateCommand-Creating_a_custom_command) and [InvokeCommand](https://docs.byteplus.com/en/docs/ecs/InvokeCommand_-_Execute_command) operations, which can be called to create custom commands and to execute existing commands, respectively, the RunCommand operation supports creating a command and executing it in one call.

* You can configure custom parameters in the command using parameters in the `ParameterDefinitions.N.xxx` structure. The usage rules are as follows:

   * Argument \- N: indicates the serial number of the custom parameter. Valid range: 1\-60.

   * Separate multiple custom parameters with `&`.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=RunCommand&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|CmveeW">必选</span> `Sample value: RunCommand`

The action that you want to perform. Value: RunCommand.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|Y8ngjA">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**WindowsPassword** <span data-label="purple">string</span> `Optional` `Sample value: -`

The password of the Windows custom user



**Type** <span data-label="purple">string</span> <span data-api-tag="require|vzvZbz">必选</span> `Sample value: Shell`

The command type. Value:


* Shell: Indicates creating a Shell script that runs in a Linux instance.

* Python: Indicates creating a Python script.

* Bat: Indicates creating a Bat script.

* PowerShell: Indicates creating a PowerShell script.



**ContentEncoding** <span data-label="purple">string</span> `Optional` `Sample value: Base64`

Specifies whether the returned command content is Base64 encoded. Value:


* Base64 (default): The command content is Base64 encoded.

* PlainText: The command content is not Base64 encoded.



**CommandContent** <span data-label="purple">string</span> <span data-api-tag="require|06NRLD">必选</span> `Sample value: IyEvYm****aW9uIHN1Y2Nlc3MhIg%3D%3D`

The command content.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before coding, make sure that the first line of the script specifies the script interpreter. Rules are as follows:</div>


   * <div data-tips="true" data-tips-type="tip">Shell script: The first line needs to be <code>#!/bin/bash</code>.</div>


   * <div data-tips="true" data-tips-type="tip">Python script: The first line needs to be <code>#!/usr/bin/python</code>.</div>


* <div data-tips="true" data-tips-type="tip">The size of the command content cannot exceed 16 KB.</div>




**WorkingDir** <span data-label="purple">string</span> `Optional` `Sample value: /home`

The directory where the created command runs on the ECS instance. For Linux instances, the default value is `/home`.



**Username** <span data-label="purple">string</span> `Optional` `Sample value: root`

The username for command execution.

&nbsp;

Default value: root.



**Timeout** <span data-label="purple">integer</span> `Optional` `Sample value: 60`

The maximum timeout duration for the created command running on the ECS instance. Unit: **seconds**.


* Value range: 30 ~ 86400.

* Default value: 60.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the command execution times out, the command process is stopped forcibly.</div>




**InvocationName** <span data-label="purple">string</span> <span data-api-tag="require|bH3DXF">必选</span> `Sample value: test`

The name of the job. Naming rules are as follows:


* Cannot exceed 64 characters.

* Can contain Chinese characters, letters, numbers, underscores "_", and hyphens "\-" only, and cannot start with a number or hyphen.

* Jobs within the same region can use the same name.



**InvocationDescription** <span data-label="purple">string</span> `Optional` `Sample value: description`

The command description. Default value: empty string. The length cannot exceed 256 characters.



**InstanceIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|DUsQgm">必选</span> `Sample value: InstanceIds.1=i-ervasv*****&InstanceIds.2=i-uihrdgh*****`

The list of instance IDs. Up to 200 IDs are supported. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation to query and obtain the instance ID.


* Argument \- N: specifies the serial number of the instance.

* Separate multiple instance IDs with `&`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If one of the specified instances does not meet the execution condition (for example, an instance is in a shutdown or other unavailable status), you need to specify all required instances again.</div>




**RepeatMode** <span data-label="purple">string</span> `Optional` `Sample value: Rate`

Specifies the mode of command execution. Value:


* Once (default): Indicates that the job is executed immediately.

* Rate: Indicates the job is executed periodically. You need to specify execution cycle by passing in the Rate expression via the `Frequency` parameter.

* Fixed: The job is executed at the specified time. The execution time needs to be specified via the `LaunchTime` parameter.



**Frequency** <span data-label="purple">string</span> `Optional` `Sample value: 5m`

The execution frequency. This parameter is required only when `RepeatMode=Rate`. To specify the execution cycle, pass in the Rate expression parameter in the following format:


* <execution interval value\><execution interval unit\>

   * Supported units of the execution interval: minute (m), hour (h), and day (d). This applies to jobs with fixed interval execution.

   * Value range of time interval: 5–60 minutes, 1–24 hours, 1–7 days. The interval must be longer than the job timeout period.

* The execution interval is based on a fixed frequency and independent of the actual execution duration of the job.

* After a job is created, it is executed once at the time specified for `LaunchTime`. The next execution time is based on the interval configuration.



**LaunchTime** <span data-label="purple">string</span> `Optional` `Sample value: 2022-11-07T11:49:13Z`

The execution time.


* When `RepeatMode=Rate`, pass in the first execution time of the job in the following format:

   * Time format: RFC3339. For example, 2022\-11\-07T11:49:13Z.

* When `RepeatMode=Fixed`, pass in the time the job begins execution in the following format:

   * Time format: RFC3339. For example, 2022\-11\-07T11:49:13Z.



**RecurrenceEndTime** <span data-label="purple">string</span> `Optional` `Sample value: 2022-11-07T11:49:13Z`

The cycle end time. Format: RFC3339.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required only when <code>RepeatMode</code> is <code>Rate</code> (which indicates the job is executed periodically).</div>




**EnableParameter** <span data-label="purple">boolean</span> `Optional` `Sample value: false`

Indicates whether the created command enables the custom parameter feature. Value:


* false (default): Disables the custom parameter feature.

* true: Enables the custom parameter feature.



**ParameterDefinitions.N.Name** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.Name=dir`

The parameter name, which needs to be defined in the script based on {{Param}}. Naming rules:


* A parameter name cannot exceed 64 bytes in length.

* Follow Shell variable naming conventions: Use lowercase letters, uppercase letters, and underscores. Cannot begin with a digit. No spaces are allowed in the middle, but underscores can be used.



**ParameterDefinitions.N.Type** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.Type=String`

The custom parameter type. Value:


* String: Indicates that the custom parameter is of the `String` (string) type.

* Digit: Indicates that the custom parameter is of the `Digit` (number) type.



**ParameterDefinitions.N.Required** <span data-label="purple">boolean[]</span> `Optional` `Sample value: ParameterDefinitions.1.Required=true`

Indicates whether the custom parameter is required. Value:


* true: Required.

* false: Not required.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the parameter is required, pass the custom parameter value via the <code>Parameters</code> parameter.</div>




**ParameterDefinitions.N.DefaultValue** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.DefaultValue=ecs`

The default value of the custom parameter.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pass in the default value corresponding to the parameter type specified by the <code>Type</code> parameter.</div>




**ParameterDefinitions.N.MinLength** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.MinLength=1`

The minimum length of the custom parameter value (string).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Value range of <code>MinLength</code>: 1~1000.</div>


* <div data-tips="true" data-tips-type="tip">When <code>Type=String</code>, the parameter is required, and when <code>Required</code> is set to <code>true</code>, the default value is <code>1</code>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter value needs to be smaller than the value of <code>MaxLength</code>.</div>




**ParameterDefinitions.N.MaxLength** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.MaxLength=98`

The maximum length of the custom parameter value (string).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Value range of <code>MaxLength</code>: 1~1000.</div>


* <div data-tips="true" data-tips-type="tip">When <code>Type=String</code>, the parameter is required, and when <code>Required</code> is set to <code>true</code>, the default value is <code>1000</code>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter value needs to exceed the value of <code>MinLength</code>.</div>




**ParameterDefinitions.N.MinValue** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.MinValue=1`

The minimum value (number) of the custom parameter.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Value range of <code>MinValue</code>: \-1000000~1000000.</div>


* <div data-tips="true" data-tips-type="tip">When <code>Type=Digit</code>, the parameter is required, and when <code>Required</code> is set to <code>true</code>, the default value is <code>-1000000</code>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter value cannot exceed the value of <code>MaxValue</code>.</div>




**ParameterDefinitions.N.MaxValue** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.MaxValue=100`

The maximum value (number) of the custom parameter.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Value range of <code>MaxValue</code>: \-1000000~1000000.</div>


* <div data-tips="true" data-tips-type="tip">When <code>Type=Digit</code>, the parameter is required, and when <code>Required</code> is set to <code>true</code>, the default value is <code>1000000</code>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter value cannot exceed the value of <code>MinValue</code>.</div>




**ParameterDefinitions.N.DecimalPrecision** <span data-label="purple">string[]</span> `Optional` `Sample value: ParameterDefinitions.1.DecimalPrecision=4`

The number of decimal places allowed for the custom parameter value (number).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Value range of <code>DecimalPrecision</code>: 0~10.</div>


* <div data-tips="true" data-tips-type="tip">When <code>Type=Digit</code>, the parameter is required, and when <code>Required</code> is set to <code>true</code>, the default value is <code>0</code>.</div>




**Parameters** <span data-label="purple">string</span> `Optional` `Sample value: {"username":"root"}`

When the command contains a custom parameter, you need to pass in the key\-value pair of the custom parameter via this parameter. For example, if the command content is `echo {{name}}`, use the `Parameter` parameter to pass in the key\-value pair `{"name":"Jack"}` . For the custom parameter, the value of the variable `name` is automatically replaced, generating a new command. The actual command content executed is `echo Jack`.

&nbsp;

Rules for the custom parameter are as follows:


* The value range of the custom parameter number: 0 \- 60.

* The key of a custom parameter cannot be an empty string and can be up to 64 characters in length.

* The value of a custom parameter can be an empty string.

* After Base64 encoding, the combined length of the custom parameter(s) and original command content cannot exceed 16KB.

* The set of custom parameter names configured is required to be a subset of the parameter set defined when the command is created. For the parameter not provided, the default parameter value is used.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: default`

The associated project. Each instance can only belong to one project.



**Tags.N.Value** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The value of the user tag.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).


Naming rules:


* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 0 to 256 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> parameter first.</div>




**Tags.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the user tag.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple keys with ampersands (&).


Naming rules:


* It cannot start with `volc:` or `sys:` in any case form.

* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InvocationId** <span data-label="purple">string</span> `Sample value: ivk-2a74****`

The ID of the executed task.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=RunCommand&Version=2020-04-01&Type=Shell&InvocationName=test&InstanceIds.1=i-ydgglud*****&CommandContent=ls&ContentEncoding=PlainText HTTP/1.1
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
        "Action":"RunCommand",
        "Version":"2020-04-01",
        "Service":"ecs",
        "Region":"cn-beijing"
    },
    "Result":{
        "InvocationId":"iv-fdkzoqkdl*****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameterDefinitionName.Malformed |The specified ParameterDefinition Name is malformed. The name can contain only lowercase letters (a to z), uppercase letters (A to Z), numbers (0 to 9), and underscores (_). |Invalid custom parameter name format: Allowed characters are lowercase letters, uppercase letters, and underscores. The first character can not be a digit. |
|400 |InvalidParameterDefinitionType.Malformed |The specified ParameterDefinition Type is malformed. |The custom parameter type is invalid. |
|400 |MissingParameter.ParameterDefinitionName |The required parameter ParameterDefinitionName is not supplied. |The custom parameter name cannot be empty. |
|400 |LimitExceeded.MaximumParameterDefinitionName |The specified ParameterDefinitionName exceeds the limit. |The length of the specified custom parameter name exceeds the limit. |
|400 |MissingParameter.ParameterDefinitions |The required parameter ParameterDefinitions is not supplied. |The parameter definition cannot be left empty. |
|400 |LimitExceeded.MaximumInstanceIds |The specified InstanceIds exceeds the limit. |The number of instances exceeds the limit. |
|400 |MissingParameter.InstanceIds |The required parameter InstanceIds is not supplied. |The instance ID cannot be empty. |
|400 |LimitExceeded.MaximumInvocationDescription |The specified InvocationDescription exceeds the limit. |The length of the specified job description exceeds the limit. |
|400 |InvalidInvocationName.Malformed |The specified InvocationName is malformed. |The specified job name is invalid. |
|400 |MissingParameter.CommandContent |The required parameter CommandContent is not supplied. |The command content cannot be empty. |
|400 |LimitExceeded.MaximumInvocations |The running invocations exceed the limit. |The number of jobs in progress exceeds the limit. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of Tags that you can create. |The upper limit of tags that you can create is reached. |
|400 |InvalidProjects.ListFailed |Fail to list projects. |Failed to fetch the specified project. |
|400 |InvalidBase64Content.Malformed |The specified Base64 Content is malformed. |The specified Base64 content is invalid. |
|400 |LimitExceeded.MaximumParameterDefinitions |The specified ParameterDefinitions exceeds the limit. |The number of specified custom parameter definitions exceeds the limit. |
|400 |InvalidFrequency.Malformed |The specified Frequency is malformed. |The Rate expression is invalid. |
|400 |MissingParameter.Frequency |The required Frequency is not supplied. |The Rate expression cannot be empty. |
|400 |InvalidRecurrenceEndTime.Malformed |The specified RecurrenceEndTime is malformed. |The cycle end time is invalid. |
|400 |MissingParameter.RecurrenceEndTime |The required RecurrenceEndTime is not supplied. |The cycle end time cannot be empty. |
|400 |InvalidLaunchTime.Malformed |The specified LaunchTime is malformed. |The specified execution time is invalid. |
|400 |MissingParameter.LaunchTime |The required LaunchTime is not supplied. |The execution time cannot be empty. |
|400 |InvalidInstanceId.Unregister |The specified instance is unregister. |The specified instance has no Agent registered. |
|400 |InvalidCloudAssistantStatus.Malformed |The cloud assistant status of the instance cannot be operated. |The current status of the instance Agent does not support this operation. |
|400 |InvalidRepeatMode.Malformed |The specified RepeatMode is malformed. |The specified mode of command execution is invalid. |
|400 |InvalidParameters.Malformed |The specified Parameters are malformed. |The specified custom parameter is invalid. |
|400 |InvalidParameterDefinitions.Malformed |The specified ParameterDefinitions is malformed. |The specified parameter definition is invalid. |
|400 |LimitExceeded.MaximumCommandContent |The specified CommandContent exceeds the limit. |The length of the specified command content exceeds the limit. |
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidEnableParameter.Malformed |The specified EnableParameter is malformed. |The specified value of EnableParameter is invalid. |
|400 |MissingParameter.Type |The required parameter Type is not supplied. |The command type cannot be empty. |
|400 |LimitExceeded.MaximumParameters |The specified Parameters exceeds the limit. |The number of specified custom parameters exceeds the limit. |
|400 |MissingParameter.ParameterName |The required Parameters Name is not supplied. |The parameter name cannot be left empty. |
|400 |LimitExceeded.MaximumParameterName |The specified Parameter Name exceeds the limit. |The length of the specified custom parameter name exceeds the limit. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified command type is invalid. |
|400 |LimitExceeded.MaximumTimeout |The specified timeout exceeds the limit. |The specified timeout period (s) exceeds the limit. |
|400 |LimitExceeded.MaximumInvocationName |The specified InvocationName exceeds the limit. |The length of the specified job name exceeds the limit. |
|404 |InvalidParameterDefinitions.NotFound |The specified ParameterDefinitions does not exist. |The definition of the specified custom parameter does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |MissingParameter.Tags |The required parameter Tags are empty. |The tag parameter cannot be empty. |
|409 |InvalidParameterDefinitions.Conflict |The specified ParameterDefinition already exists. |The specified custom parameter already exists. |
|409 |InvalidInstanceIds.Conflict |The specified InstanceId already exists. |The specified instance ID already exists. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
