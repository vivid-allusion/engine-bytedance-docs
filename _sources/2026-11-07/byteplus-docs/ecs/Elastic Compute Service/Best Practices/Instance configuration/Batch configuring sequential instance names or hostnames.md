---
title: "Batch configuring sequential instance names or hostnames"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames"
---

This topic describes how to configure sequential names or hostnames for multiple instances when you create instances in a batch in the ECS console or via OpenAPI. This helps you to better manage your instances.

<span id=".6YWN572u6KeE5YiZ"></span>
## Configuration rules

<span id=".5ZG95ZCN6KeE5YiZ"></span>
### Naming rules

The naming rules for instance names and hostnames are listed below:


|Type |Naming rules |
|---|---|
|Instance name |* Start with a letter or a Chinese character.<br><br>* Only Chinese characters, letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.<br><br>* It must be 1 to 128 characters in length. |
|Host name |* Linux instances:<br><br>   * Letters, numbers, periods ".", and hyphens "\-" are allowed.<br><br>   * Can not start or end with a hyphen or period. Hyphens and periods can not be used consecutively.<br><br>   * The length limit is 2 to 63 characters.<br><br>* Windows instances:<br><br>   * Letters, numbers, and hyphens ("\-") are allowed, but the name cannot consist only of digits.<br><br>   * Can not start or end with a hyphen. Hyphens can not be used consecutively.<br><br>   * The length limit is 2 to 15 characters. |


<span id=".5ZG95ZCN5qC85byP"></span>
### Naming format

**Format**

Parameter format of configuring sequential names: `name_prefix[begin_number,bits]name_suffix`. Detailed field descriptions are listed below.


|Field |Description |Examples |
|---|---|---|
|name_prefix |Indicates the prefix of instance names or hostnames. You are required to specify this field based on the [naming rules](https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames#.5ZG95ZCN6KeE5YiZ). |name |
|[begin_number,bits] |* begin_number: Specifies the starting number of instance names or hostnames.<br><br>   * Value range: [0,9999]<br><br>   * Default value: 0<br><br>* bits: Specifies the number of bits that value(s) occupy in instance names or hostnames.<br><br>   * Value range: [1,4]<br><br>   * Default value: 4<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only English commas (,) are supported to separate values of "begin_number" and "bits", and no spaces are allowed between.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If [begin_number,bits] is specified as <code>[]</code> or <code>[,]</code>, the value of "begin_number" starts from 0, and "bits" takes the default value 4.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the total digits of begin_number plus Count (instance number) exceed the specified bits, the names are created based on the actual total digit count. This total cannot exceed the maximum allowed bits. Otherwise, the creation fails.</div><br> |[99,3] |
|name_suffix |Indicates the suffix of instance names or hostnames. |ecs |


**Examples**


|Description |Input parameter |Instance names (three instances) |
|---|---|---|
|Standard format |name[1,3]ecs |name001ecs, name002ecs, name003ecs |
|Standard format. Digits of begin_number + Count: \> specified value of "bits" |name[99,2]ecs |name099ecs, name100ecs, name101ecs |
|"begin_number" and "bits" are left empty |name[]ecs or name[,]ecs |name0000ecs, name0001ecs, name0002ecs |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="J9wsrH0fYS" title="ECS console">
<TabTitle>ECS console</TabTitle>

The following mainly describes how to configure instance names and hostnames. For more instance configurations, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. Click the "Create instance" button to purchase an ECS instance.

3. Configure the information in **Basic configuration and Network configuration**.

4. On the "Custom configuration" tab, in the "Instance name" (required) or "Hostname" field, enter the desired sequence in the format `name_prefix[begin_number,bits]name_suffix`. For configuration rules, see [Naming format](https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames#.5ZG95ZCN5qC85byP). Then complete the remaining configurations.

   In the example provided in this topic, name[1,3]ecs is entered in "Instance name", and name[1,3]host in "Hostname".

5. Set the number of instances to 3 to complete the purchase.


**Operation results:** 

After the purchase, you can view the three newly created instances on the Instances page. Their sequential instance names are name001ecs, name002ecs, and name003ecs, and sequential hostnames are name001host, name002host, and name003host.


</Tab>
<Tab zoneid="xxFDLd5uwO" title="OpenAPI">
<TabTitle>OpenAPI</TabTitle>

When you create instances in a batch by calling the RunInstances interface, the sequential suffix parameter `UniqueSuffix` can affect the sequential names of instances. Details are as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The following mainly introduces arguments for configuring sequential names. For information about other arguments, refer to <a href="https://docs.byteplus.com/en/docs/ecs/RunInstances">RunInstances</a>. </div>


* <div data-tips="true" data-tips-type="tip">To configure sequential names for parameters <code>InstanceName</code> and <code>Hostname</code>, specify the parameters in the format <code>name_prefix[begin_number,bits]name_suffix</code>. For configuration rules, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames#.5ZG95ZCN5qC85byP">Naming format</a>.</div>




<Tabs>
<Tab zoneid="GlkwpVsQsp" title="Disable sequential suffix feature, with [begin_number,bits] specified only">
<TabTitle>Disable sequential suffix feature, with [begin_number,bits] specified only</TabTitle>

After disabling the sequential suffix feature (disabled by default), you can sequence names of the instances created in a batch by specifying values in the format of [begin_number,bits]. Detailed argument configurations are as follows:


* `UniqueSuffix`: false (default). This means not adding sequential suffixes for specified values of `InstanceName` and `Hostname`.

* `Count`: 3

* `InstanceName`: name[1,3]ecs

* `Hostname`: name[1,3]host


Based on the operations above, the sequential names of the three newly created instances are name001ecs, name002ecs, and name003ecs. Their sequential hostnames are name001host, name002host, and name003host.


</Tab>
<Tab zoneid="rvNJrgcLeA" title="Enable sequential suffix feature, with [begin_number,bits] not specified">
<TabTitle>Enable sequential suffix feature, with [begin_number,bits] not specified</TabTitle>

When creating multiple instances, you can enable the sequential suffix feature to automatically sequence instance names and hostnames. The parameters are configured as follows:


* `UniqueSuffix`: true. This means adding suffixes automatically sequenced for what is specified in `InstanceName` and `Hostname`, respectively. The number of added suffixes starts from 1 by default and increases sequentially based on the number of instances.

* `SuffixIndex` (optional): Specifies the starting number of sequential suffixes. Default value: 1. Value range: 1 ~ 999.

* `Count`: 3

* `InstanceName`: ecs

* `Hostname`: host


Based on the operations above, the sequential names of the three newly created instances are ecs\-1, ecs\-2, and ecs\-3. Their sequential hostnames are host\-1, host\-2, and host\-3.


</Tab>
<Tab zoneid="Gn0FzwCK4u" title="Enable sequential suffix feature, with [begin_number,bits] specified">
<TabTitle>Enable sequential suffix feature, with [begin_number,bits] specified</TabTitle>

When you enable the sequential suffix feature and specify `InstanceName` or `Hostname` in parameter format [begin_number,bits] at the same time, configuration in  **[begin_number,bits] takes precedence over that of the** **`UniqueSuffix`** parameter. Details are listed below.


|Enabled sequential suffix feature |Whether InstanceName/Hostname specified in format [begin_number,bits] |Whether `UniqueSuffix` is valid |Examples |
|---|---|---|---|
|`UniqueSuffix=true`, and `SuffixIndex` takes the default value 1 |Both specified |Invalid for both parameters |Specify `InstanceName` and `Hostname` as name[666,3]ecs<br><br>Final generated names:<br><br>The instance names and hostnames are the same: name666ecs, name667ecs, name668ecs |
||Specify `InstanceName`, not `Hostname` |Valid for `Hostname` |Specify `InstanceName` as name[666,3]ecs and `Hostname` as host<br><br>Final generated names:<br><br><br>* Instance names: name666cs, name667ecs, and name668ecs<br><br>* Hostnames: host\-1, host\-2, and host\-3 |
||Specify `Hostname`, not `InstanceName` |Valid for `InstanceName` |Specify `InstanceName` as ecs and `Hostname` as name[666,3]host<br><br>Final generated names:<br><br><br>* Instance names: ecs\-1, ecs\-2, and ecs\-3<br><br>* Hostnames: name666host, name667host, and name668host |


<span id=".55u45YWz5paH5qGj"></span>
## 


</Tab>
</Tabs>



</Tab>
</Tabs>
