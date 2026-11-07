---
title: "InvokeCommand - Executes commands"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/InvokeCommand_-_Execute_command"
---

Call the InvokeCommand operation to create a task via an existing custom command or an existing public command.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=InvokeCommand&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|U8JcyY">必选</span> `Sample value: InvokeCommand`

The action that you want to perform. Value: InvokeCommand.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|LulBLi">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**Tags.N.Value** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The value of the tag.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).


Naming rules:


* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 0 to 256 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




**Tags.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The key of the tag.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with &.


Naming rules:


* It cannot start with `volc:` or `sys:` in any case form.

* It can contain only language characters, digits, spaces, and English symbols of " _", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: default`

The associated project. Each instance can only belong to one project.



**WindowsPassword** <span data-label="purple">string</span> `Optional` `Sample value: --`

The password of the Windows custom user



**CommandId** <span data-label="purple">string</span> <span data-api-tag="require|0Z3orn">必选</span> `Sample value: cmd-ydckta****`

The command ID. You can call the [DescribeCommands](https://docs.byteplus.com/en/docs/ecs/DescribeCommands_-_Query_the_command_list) operation to query and obtain all available command IDs.



**InvocationName** <span data-label="purple">string</span> <span data-api-tag="require|DICynA">必选</span> `Sample value: updateAgent`

The name of the job.


* Cannot exceed 64 characters.

* Currently, special characters can be used.

* Jobs within the same region can use the same name.



**InvocationDescription** <span data-label="purple">string</span> `Optional` `Sample value: description`

The job description. Default value: empty string. The length cannot exceed 256 characters.



**Timeout** <span data-label="purple">integer</span> `Optional` `Sample value: 60`

The maximum timeout duration for the created command running on the ECS instance. Unit: **seconds**.


* Default value: 60.

* Value range: 30~86400.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A timeout occurs when the created command cannot be executed for some reason. When the command execution times out, the command process is stopped forcibly.</div>




**Frequency** <span data-label="purple">string</span> `Optional` `Sample value: 5m`

The execution frequency. This parameter is required only when `RepeatMode=Rate`. To specify the execution cycle, pass in the Rate expression parameter in the following format:


* <execution interval value\><execution interval unit\>

   * Supported units of the execution interval: minute (m), hour (h), and day (d). This applies to jobs executed at fixed intervals.

   * Value range of time interval: 5–60 minutes, 1–24 hours, 1–7 days. The interval must be longer than the job timeout period.

* The execution interval is based on a fixed frequency and independent of the actual execution duration of the job.

* After a job is created, it is executed once at the time specified for `LaunchTime`. The next execution time is based on the specified interval.



**Parameters** <span data-label="purple">string</span> `Optional` `Sample value: {"username":"root"}`

When the command contains a custom parameter, pass in the key\-value pair of the custom parameter via this parameter.

&nbsp;

For example, if the command content is `echo {{name}}`, use the `Parameter` parameter to pass in the key\-value pair `{"name":"Jack"}`. For the custom parameter, the value of the variable `name` is automatically replaced, generating a new command. The command content actually executed is `echo Jack`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The value range of the custom parameter number: 0 \- 60.</div>


* <div data-tips="true" data-tips-type="tip">The key of a custom parameter cannot be an empty string and can be up to 64 characters in length.</div>


* <div data-tips="true" data-tips-type="tip">The value of a custom parameter can be an empty string.</div>


* <div data-tips="true" data-tips-type="tip">After Base64 encoding, the combined length of the custom parameter(s) and original command content cannot exceed 16KB.</div>


* <div data-tips="true" data-tips-type="tip">The set of custom parameter names configured is required to be a subset of the parameter set defined when the command is created. For the parameter not provided, the default parameter value is used.</div>




**Username** <span data-label="purple">string</span> `Optional` `Sample value: root`

The username for command execution in the ECS instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, the built\-in username in the command is used.</div>




**WorkingDir** <span data-label="purple">string</span> `Optional` `Sample value: /home`

The directory in which the created command runs in the ECS instance. Default value:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For Linux instances, the default path is /home.</div>




**RepeatMode** <span data-label="purple">string</span> `Optional` `Sample value: Rate`

Specifies the mode of command execution. Supported values:


* Once (default): Indicates that the command is executed immediately.

* Rate: Indicates that the command is executed periodically. The execution cycle needs to be specified by passing in the Rate expression via the `Frequency` parameter.

* Fixed: Indicates that the command is executed at the specified time. The execution time needs to be specified via the `LaunchTime` parameter.



**LaunchTime** <span data-label="purple">string</span> `Optional` `Sample value: 2022-11-07T11:49:13Z`

The execution time.


* When `RepeatMode=Rate`, pass in the first execution time of the job in the following format:

   * Time format: RFC3339. For example, 2022\-11\-07T11:49:13Z.

* When `RepeatMode=Fixed`, pass in the time the job begins execution in the following format:

   * Time format: RFC3339. For example, 2022\-11\-07T11:49:13Z.



**RecurrenceEndTime** <span data-label="purple">string</span> `Optional` `Sample value: 2022-11-07T11:49:13Z`

The cycle end time. This parameter is required only for periodic jobs (Rate).

Format: RFC3339.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required only when <code>RepeatMode</code> is <code>Rate</code> (which indicates the job is executed periodically).</div>




**InstanceIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|InKg6m">必选</span> `Sample value: InstanceIds.1=i-ervasv*****&InstanceIds.2=i-uihrdgh*****`

The list of instance IDs. Up to 200 IDs are supported. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation to query and obtain the instance ID.


* Argument \- N: specifies the serial number of the instance.

* Separate multiple instance IDs with `&`.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InvocationId** <span data-label="purple">string</span> `Sample value: ivk-2a745b****`

The ID of the executed task.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=InvokeCommand&Version=2020-04-01&CommandId=cmd-ybtvqki****&Username=root&InvocationName=updateAgent&InstanceIds.1=i-bp185dy2o3o6neg****  HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"2023082415303301022514515207C4****",
        "Action":"InvokeCommand",
        "Version":"2020-04-01",
        "Service":"ecs",
        "Region":"cn-beijing"
    },
    "Result":{
        "InvocationId":"ivk-2a74****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.CommandId |The required parameter CommandId is not supplied. |The command ID cannot be empty. |
|400 |InvalidProjects.ListFailed |Fail to list projects. |Failed to obtain projects. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of Tags that you can create. |The upper limit of tags that you can create is reached. |
|400 |MissingParameter.RecurrenceEndTime |The required RecurrenceEndTime is not supplied. |The cycle end time cannot be empty. |
|400 |MissingParameter.Frequency |The required Frequency is not supplied. |The Rate expression cannot be empty. |
|400 |LimitExceeded.MaximumInstanceIds |The specified InstanceIds exceeds the limit. |The number of instances exceeds the limit. |
|400 |InvalidRecurrenceEndTime.Malformed |The specified RecurrenceEndTime is malformed. |The cycle end time is invalid. |
|400 |LimitExceeded.MaximumInvocations |The running invocations exceed the limit. |The number of jobs in progress exceeds the limit. |
|400 |MissingParameter.InstanceIds |The required parameter InstanceIds is not supplied. |The instance ID cannot be empty. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidFrequency.Malformed |The specified Frequency is malformed. |The Rate expression is invalid. |
|400 |InvalidInvocationName.Malformed |The specified InvocationName is malformed. |The specified job name is invalid. |
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|400 |LimitExceeded.MaximumInvocationName |The specified InvocationName exceeds the limit. |The length of the specified job name exceeds the limit. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |LimitExceeded.MaximumInvocationDescription |The specified InvocationDescription exceeds the limit. |The length of the specified job description exceeds the limit. |
|400 |InvalidRepeatMode.Malformed |The specified RepeatMode is malformed. |The specified mode of command execution is invalid. |
|400 |InvalidParameters.Malformed |The specified Parameters are malformed. |The specified custom parameter is invalid. |
|400 |LimitExceeded.MaximumParameters |The specified Parameters exceeds the limit. |The number of specified custom parameters exceeds the limit. |
|400 |MissingParameter.ParameterName |The required Parameters Name is not supplied. |The parameter name cannot be left empty. |
|400 |LimitExceeded.MaximumParameterName |The specified Parameter Name exceeds the limit. |The length of the specified custom parameter name exceeds the limit. |
|400 |InvalidParameterDefinitionType.Malformed |The specified ParameterDefinition Type is malformed. |The custom parameter type is invalid. |
|400 |InvalidParameterDefinitions.Malformed |The specified ParameterDefinitions is malformed. |The specified parameter definition is invalid. |
|400 |MissingParameter.LaunchTime |The required LaunchTime is not supplied. |The execution time cannot be empty. |
|400 |InvalidLaunchTime.Malformed |The specified LaunchTime is malformed. |The specified execution time is invalid. |
|400 |InvalidCloudAssistantStatus.Malformed |The cloud assistant status of the instance cannot be operated. |The current status of the instance Agent does not support this operation. |
|400 |LimitExceeded.MaximumTimeout |The specified timeout exceeds the limit. |The specified timeout period (seconds) exceeds the limit. |
|400 |InvalidInstanceId.Unregister |The specified instance is unregister. |The specified instance has no Agent registered. |
|404 |MissingParameter.Tags |The required parameter Tags are empty. |The tag parameter cannot be empty. |
|404 |InvalidCommand.NotFound |The specified Command does not exist. |The specified command does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|409 |InvalidInstanceIds.Conflict |The specified InstanceId already exists. |The specified instance ID already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |


&nbsp;
