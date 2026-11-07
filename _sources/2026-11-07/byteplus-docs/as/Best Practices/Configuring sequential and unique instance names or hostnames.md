---
title: "Configuring sequential and unique instance names or hostnames"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances"
---

When you use Auto Scaling to automatically scale out instances, you can specify sequential and unique instance names or hostnames for each instance. This enables quick identification of instances corresponding to different services and improving the manageability of instances. This topic describes the rules and methods for configuring sequential names.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Auto Scaling supports two [scaling configuration sources](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources): launch template and scaling configuration. The methods for configuring sequential names differ between the two sources:


|Scaling configuration source |Instance name/hostname configuration rules |Configuration method for instance name or hostname |Related documents |
|---|---|---|---|
|Instance launch template |When a scaling group is associated with the same launch template, the instance names are sequential and unique only for a single scaling\-out activity. However, instance names may repeat across different scaling\-out activities. |You can configure sequential instance names or hostnames for ECS instances only in the [instance launch template console](https://console.byteplus.com/ecs/template). The configuration method is the same as that for purchasing ECS instances. For more information, see [Batch configuring sequential instance names or hostnames](https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames). |* [Creating instance launch templates](https://docs.byteplus.com/en/docs/ecs/Creating-launch-templates)<br><br>* [Creating versions of instance launch templates](https://docs.byteplus.com/en/docs/ecs/Creating-launch-template-versions) |
|Scaling configurations |When a scaling group is associated with the same scaling configuration, the starting number of instance names for different scaling\-out activities will increment based on the maximum sequential number among existing names. All instance names within the scaling group are sequential and unique. |You can configure sequential instance names or hostnames for ECS instances in the console or by using OpenAPI. For more information, see [Configuration rules](https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances#.6YWN572u6KeE5YiZ). |* [Create a scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration)<br><br>* [CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration) |


<span id=".6YWN572u6KeE5YiZ"></span>
## Configuration rules

<span id=".5ZG95ZCN6KeE5YiZ"></span>
### Naming rules

The naming rules for instance names and hostnames are listed below:


|Type |Naming rules |
|---|---|
|Instance name |* Start with a letter or Chinese.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* It must be 1 to 128 characters in length.<br><br>* Special characters are currently not supported. |
|Host name |* Linux instances:<br><br>   * Letters, numbers, periods ".", and hyphens "\-" are allowed.<br><br>   * Can not start or end with a hyphen or period. Hyphens and periods can not be used consecutively.<br><br>   * The length limit is 2 to 63 characters.<br><br>* Windows instances:<br><br>   * Letters, numbers, or hyphens "\-" are allowed. But the name can not be comprised of numbers only.<br><br>   * Can not start or end with a hyphen. Hyphens can not be used consecutively.<br><br>   * The length limit is 2 to 15 characters. |


<span id=".5ZG95ZCN5qC85byP"></span>
### Naming format

Auto Scaling provides the following two naming formats:


* Dynamic extension sequencing (recommended): In addition to the 4\-digit base, 3 extended digits are added to the sequential numeric value of a name, greatly expanding the value range.

* Fixed incremental sequencing: The sequential numeric value of a name supports up to 4 digits, with the upper limit of 9999.


<span id="y0thkbfF"></span>
## Format 1 (recommended): Dynamic extension sequencing

<span id=".5qC85byP"></span>
#### Format

The parameter format is `name_prefix(as_extend_begin,as_extend_bits)[begin_number,bits]name_suffix`.


|**Field name** |**Required** |**Configuration instructions** |**Example** |
|---|---|---|---|
|name_prefix |Yes |The prefix of the instance name or hostname. The prefix is required and must comply with the [naming rules](https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances#.5ZG95ZCN6KeE5YiZ). |name |
|(as_extend_begin,as_extend_bits) |Yes |The extended sequential value of the instance name or hostname. When the base sequential numeric value in existing names of the scaling group reaches the upper limit, this parameter automatically increments by one digit. The base sequential value then restarts incrementing from 0, cycling until the new upper limit is reached.<br><br><br>* as_extend_begin: The start value of the extended sequential value.<br><br>   * Valid range: [0,ZZZ]. Each digit can be 0–9, a–z, or A–Z. For example, 9 increments to a, and z increments to A.<br><br>   * Default value: 0.<br><br>* as_extend_bits: The number of digits occupied by the extended sequential value.<br><br>   * Valid range: [1,3].<br><br>   * The default value is 3.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The separator in (as_extend_begin, as_extend_bits) only supports an English comma (,) and must not include spaces.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you specify [] or [,], as_extend_begin starts from 0, and bits defaults to 3.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the digit count of the value specified for as_extend_begin exceeds the value of as_extend_bits, bits defaults to 3.</div><br> |(0,3) |
|[begin_number,bits] |Yes |The base sequential value of the instance name or hostname. When this parameter increments to its maximum value, subsequent scale\-out operations will automatically increase the extended sequential numeric value by one digit. The parameter then restarts incrementing from 0, cycling until the new upper limit is reached.<br><br><br>* begin_number: The start value of the base sequential value.<br><br>   * Valid range: [0,9999].<br><br>   * Default value: 0.<br><br>* bits: The number of digits occupied by the base sequential value.<br><br>   * Valid range: [2,4].<br><br>   * Default value: 4.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only English commas (,) are supported to separate values of "begin_number" and "bits", and no spaces are allowed between.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If [begin_number,bits] is specified as [] or [,], the value of "begin_number" starts from 0, and "bits" takes the default value 4.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the digit count of the value specified for begin_number exceeds the value of bits, bits defaults to 4.</div><br> | |
|name_suffix |No |Indicates the suffix of instance names or hostnames. |\-ecshost |


<span id=".6K-05piO"></span>
#### Description


* By default, the numeric value of a name increases sequentially. If a scaled\-out instance fails to start, it is removed from the scaling group and a new instance is scaled out. As a result, instance names within the scaling group may not be consecutive.

* When the extended sequential numeric value and base sequential numeric value of instance names reach their upper limits, further scale\-out requests will trigger an error and stop scaling activities. You must reconfigure the name format.

* Calculate the sum of the base sequential numeric value of the maximum sequential value among existing instance names in the scaling group and the number of instances to be scaled out. If this sum is greater than or equal to the maximum value of the base sequential numeric value, instance names may not increase consecutively (that is, discontinuously).


<span id=".56S65L6L"></span>
#### Example

The following table describes the naming parameter examples and final naming results.


|Description |Input parameter |Instance names (3 instances) |
|---|---|---|
|Standard format |name(0,3)[1,3]ecs |name000001ecs, name000002ecs, name000003ecs |
|Value not specified |name()[]ecs or name(,)[,]ecs |name0000000ecs, name0000001ecs, name0000002ecs |
|Standard format. The instance with the maximum numeric value in the current scaling group is nameZ99ecs. |name(0,1)[0,2]ecs |Further scale\-out requests will trigger an error and halt scaling activities. |
|Standard format. The digit count of the value specified for begin_number exceeds the value of bits. |name(0,1)[999,2]ecs |name00999ecs, name01000ecs, name01001ecs |
|Standard format. The instance with the maximum numeric value in the current scaling group is name0009ecs and there are instances that failed to scale out. |name(0,2)[0,2]ecs |name0010ecs, name0011ecs, name0013ecs |
|Standard format. The instance with the maximum numeric value in the current scaling group is name0098ecs. The sum of the base sequential numeric value (from the maximum sequential value of existing instances) and the number of instances to be scaled out exceeds the maximum value of the base sequential numeric value. |name(0,2)[0,2]ecs |name0100ecs, name0101ecs, name0102ecs |


<span id="O1StFcfk"></span>
### Format 2: Fixed incremental sequencing

<span id="kPmUsLe8"></span>
#### Format

The parameter format is name_prefix(AUTO_INCREMENT)[begin_number,bits]name_suffix.


|**Field name** |**Required** |**Configuration instructions** |**Example** |
|---|---|---|---|
|name_prefix |Yes |Indicates the prefix of instance names or hostnames. You are required to specify this field based on the [naming rules](https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances#.5ZG95ZCN6KeE5YiZ). |name |
|(AUTO_INCREMENT) |Yes |Fixed value, used to identify this sequencing method. |(AUTO_INCREMENT) |
|[begin_number,bits] |Yes |The sequential value of the instance name or hostname. The sequential value of the instance names or hostnames will increase based on this rule.<br><br><br>* begin_number: The start value of the sequential value.<br><br>   * Valid range: [0,9999].<br><br>   * Default value: 0.<br><br>* bits: The number of digits occupied by the sequential value.<br><br>   * Valid range: [2,4].<br><br>   * Default value: 4.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only English commas (,) are supported to separate values of "begin_number" and "bits", and no spaces are allowed between.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If [begin_number,bits] is specified as [] or [,], the value of "begin_number" starts from 0, and "bits" takes the default value 4.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the digit count of the value specified for begin_number exceeds the value of bits, bits defaults to 4.</div><br> |[0,4] |
|name_suffix |No |Indicates the suffix of instance names or hostnames. |ecs |


<span id="t5SzHFy5"></span>
#### Description


* By default, the numeric value of a name increases sequentially. If a scaled\-out instance fails to start, it is removed from the scaling group and a new instance is scaled out. As a result, instance names within the scaling group may not be consecutive.

* When the numeric value of an instance name reaches the upper limit, further scale\-out requests will trigger an error and halt scaling activities. You must reconfigure the name creation format.


<span id="s6KvMdy1"></span>
#### Example

The following table describes the naming parameter examples and final naming results.


|Description |Input parameter |Instance names (3 instances) |
|---|---|---|
|Standard format |name(AUTO_INCREMENT)[1,3]ecs |name001ecs, name002ecs, name003ecs |
|Value not specified |name(AUTO_INCREMENT)[]ecs or name(AUTO_INCREMENT)[,]ecs |name0000ecs, name0001ecs, name0002ecs |
|Standard format. The digit count of the value specified for begin_number exceeds the value of bits. |name(AUTO_INCREMENT)[999,2]ecs |name1000ecs, name1001ecs, name1002ecs |
|Standard format. The instance with the maximum numeric value in the current scaling group is name99ecs. |name(AUTO_INCREMENT)[99,2]ecs |Further scale\-out requests will trigger an error and halt scaling activities. |
|Standard format. The instance with the maximum numeric value in the current scaling group is name99ecs and there are instances that failed to scale out. |name(AUTO_INCREMENT)[99,3]ecs |name100ecs, name102ecs, name103ecs |


<span id="eiB7mzFc"></span>
###
