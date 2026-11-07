---
title: "Configure Flink Parameters"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Configure_Flink_Parameters"
---

In task development, you can configure Flink\-related parameters, including resource configurations for Task Manager and Job Manager, as well as configurations for Checkpoint, task failure restart strategies, task failure retry, dependency files, and variable scope.

<span id="19f20c67"></span>
## Precautions


* For tasks that have been launched, if the Flink parameter configuration is updated, it needs to be relaunched to synchronize the update.

* The Flink parameter configurations for streaming tasks and batch tasks differ, mainly because Flink Batch tasks do not support Checkpoints and do not support automatic tuning. When you select the **execution method** as **Streaming** or **Batch**, opening the parameter configuration will automatically switch to the appropriate parameters based on the selected execution method.

* Different engine versions support varied Flink parameter configurations, mainly reflected in Flink 1.11 supporting automatic optimization configurations for tasks, while other engine versions do not.


<span id="a9c80301"></span>
## Feature entry

On the right side of the task editing area, click **Parameter Configuration**, and then configure the Flink parameters according to the task requirements.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also directly refer to a pre\-configured template to quickly set up the Flink parameters for the task. For related documents, see <a href="https://docs.byteplus.com/docs/flink/Quickly_configure_Flink_parameters_using_configuration_templates">Quickly configure Flink parameters using configuration templates</a>.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b92c77ed1834ca6ac8c377318bc3425~tplv-goo7wpa0wc-image.image) </span>

<span id="7f24b982"></span>
## Flink parameter configuration


|**Configuration** |**Description** |
|---|---|
|Parallelism |Total concurrent global tasks, the default value is 2. |
|Individual TaskManager CPU count |The number of CPU cores for an individual TaskManager, the default value is 1, with a minimum support set to 0.5. |
|Individual TaskManager memory size |The memory size of an individual TaskManager will automatically adjust based on the number of CPU cores you set, following a 1C:4G ratio. |
|Number of slots in an individual TaskManager |The number of slots for an individual TaskManager, the default value is 2. |
|JobManager CPU count |The number of CPU cores for a JobManager, the default value is 1, with a minimum support set to 0.5. |
|JobManager memory size |The memory size of the JobManager will automatically adjust based on the CPU cores you set, following a 1C4G ratio. |


<span id="dbeefb26"></span>
## Checkpoint configuration

After enabling Checkpoint, Flink can regularly save the state information of tasks to persistent storage. When a task fails or stops unexpectedly, Flink can recover the state of the task from the latest Checkpoint, enhancing the task's reliability and fault tolerance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only Flink STREAM type tasks support Checkpoint configuration; Flink Batch type tasks do not show Checkpoint configuration.</div>



|**Configuration** |**Description** |
|---|---|
|Enable Checkpoint |Whether to enable Checkpoint; Checkpoint is enabled by default.<br><br>Once Checkpoint is enabled, Flink can periodically save the state information of tasks to persistent storage and also supports manually creating snapshots. Related documentation, please refer to [Create Task Savepoint](https://docs.byteplus.com/docs/flink/Create_Task_Savepoint). |
|Checkpoint Interval |The automatic execution interval of Checkpoint by the system. |
|Checkpoint Timeout |Checkpoint Timeout. |
|Region Checkpoint |In situations with high task concurrency, individual node failures leading to global Checkpoint failures, obvious impacts due to network delays, and write timeouts, this feature can be enabled to improve the success rate of Checkpoints.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Region Checkpoint configuration is only supported in the Flink 1.11\-byted version.</div><br><br><br><br>* Region Checkpoint divides unconnected Task sets in a task into separate Regions and manages Checkpoints by Region. When a Checkpoint failure occurs, the smallest set of Regions that need to be restarted is identified, ensuring that fewer Tasks need to be restarted.<br><br>* When a Checkpoint failure occurs in a Region, the successful state file for the corresponding Region from the last successful Checkpoint file is retrieved and logically mapped.<br><br>   Supports setting the maximum allowed percentage of Region Checkpoint failures. For example, if 50% is allowed and there are 4 Regions, then up to two Regions can fail.<br><br>* Supports setting the allowed number of consecutive failures for Region to avoid storing too much Checkpoint historical data. If 2 failures are allowed, it means that the system can fetch the state files from the previous two successful instances.<br><br><br>For a more detailed understanding of the Region Checkpoint principle, please see [Regional Checkpoint Practices](https://juejin.cn/post/7111988098229075976#heading-7). |
|Backend Cache Enable |The Flink platform currently uses RocksDB as its StateBackend. Since interaction with the RocksDB StateBackend requires serialization or deserialization of data for each State access, it consumes a significant amount of CPU, leading to low throughput.<br><br>You can enable this feature and set the maximum heap memory to significantly improve task throughput and resource utilization.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Backend Cache configuration is only supported in the Flink 1.11\-byted version.</div><br><br><br><br>* By splitting the Cache, implement a pluggable caching strategy with data storage abstracted into a separate StateStore to adapt to different business scenarios.<br><br>* By controlling the maximum value of all Cache memory in TaskManager, and implementing automatic allocation and recycling of Cache memory, ensure the total use of Cache does not exceed the maximum value, thus preventing memory overflow and leakage.<br><br>* Based on the frequency and duration of GC, it determines whether memory resources are tight and whether automatic scaling is needed to reduce the JVM's GC pressure.<br><br>* During the synchronization stage, flush dirty data to the underlying StateBackend, and use the high and low watermark mechanisms to divide intervals, ensuring that the data in the Cache during the snapshot synchronization phase is below the high watermark, thus reducing snapshot synchronization time.<br><br><br>To learn more detailed Backend Cache information, please refer to [StateBackend Performance Improvements](https://juejin.cn/post/7146142717934829605).<br><br>Backend Cache MaxHeapSize (Maximum Heap Memory): Indicates the maximum allowable memory usage of all Caches in the TaskManager. When this limit is exceeded, Cache will be unable to allocate memory. You can calculate the maximum heap memory size by using "backend.cache.initial.size \* total number of states in a single TM". Due to the on\-demand allocation mechanism, it is also possible to set a larger memory upper limit. |


<span id="74e9d6ff"></span>
## Task restart strategy configuration

Used to control the restart behavior of Tasks within a job in the event of failures or abnormalities. By configuring the Task's restart strategy, it is possible to specify how Flink handles Task failures to ensure the stable and reliable operation of the task.


|**Configuration** |**Description** |
|---|---|
|No Restart Strategy |Choosing this strategy indicates that tasks will not restart in the event of a failure. |
|Fixed Delay Restart Strategy |Selecting this strategy indicates that the task will not restart within a fixed time interval after a failure.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Fixed Time Interval Restart Strategy is the default restart strategy for the <strong>Flink 1.16\-byted</strong> version.</div><br><br><br><br>* Maximum number of restarts: The maximum number of restart attempts a task can make, which can be set to an integer greater than 0, with a default value of 10.<br><br>* Time interval between restarts: The interval between one failed restart and the next. Available time units include second, minute, hour, and day, with a default value of 20 seconds. |
|Failure Rate Restart Strategy |Selecting this strategy means that the restart will be based on the task failure rate.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Failure Rate Restart Strategy is the default restart strategy for the <strong>Flink 1.17\-byted</strong> version.</div><br><br><br><br>* Failure rate statistics time interval: The time interval for calculating the task's failure rate. Available time units include seconds, minutes, hours, and days, with the default being 10 minutes.<br><br>* Maximum number of failures within the time interval: The maximum number of restarts supported within the time interval, which can be set to an integer greater than 0, with a default value of 20.<br><br>* Interval between each restart: The time interval between a restart failure and the next restart. Available time units include seconds, minutes, hours, and days, with the default being 20 seconds. |
|Exponential Delay Restart Strategy<br><br>Exponential Delay Restart Strategy |When selecting this strategy, if the task fails, it will restart the task infinitely in an exponentially increasing manner according to the delay rules until the task recovers.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Exponential Backoff Restart Strategy is only supported in Flink versions 1.16 and 1.17.</div><br><br><br><br>* Initial restart interval after the first failure (exponential\-delay.initial\-backoff): The initial delay between restarts. The unit is seconds, with a default of 1s.<br><br>* Maximum Restart Interval (Exponential\-delay.max\-backoff): The maximum delay between restarts. The unit is seconds, defaulting to 300s.<br><br>* Growth Factor for Restart Interval (Exponential\-delay.backoff\-multiplier): The growth factor for the restart interval, defaulting to 2. The delay time is multiplied by this value as the new delay time until the maximum delay is reached.<br><br>* Time Threshold to Reset Failure Restart Interval (Exponential\-delay.reset\-backoff\-threshold): The duration for which a task has continued running. After reaching this duration, the delay time is reset to the initial delay. The default is 3600s.<br><br>* Maximum Jitter Value for Restart Interval (Exponential\-delay.jitter\-factor): A random value added to or subtracted from the delay time to avoid simultaneous restarts of multiple tasks, thereby reducing peak loads. The default value is 0.1. |
|Aggregation Failure Rate Restart Strategy |This strategy is a self\-developed task failure restart strategy by BytePlus Engine.<br><br>When this strategy is selected, it counts the number of failures within a specified time, blocks Application Failure after reaching the threshold, and delays the specified time before Task Failure; it aggregates multiple Task Failures within the delay time to reduce a large number of Task Failures causing premature Application exit.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Aggregation Failure Rate Restart Strategy is the default restart strategy for the <strong>Flink 1.11\-byted</strong> version and is only supported in the <strong>Flink 1.11\-byted</strong> version.</div><br><br><br><br>* Delay time before restart: The delay time before Task Failover restart, which is the time multiple Task Failures can be aggregated. Available time units include second, minute, hour, day, with the default being 20 seconds.<br><br>* Time interval for aggregating Failure counts: The time interval used to count task failure numbers. Available time units include second, minute, hour, day, with the default being 10 minutes.<br><br>* Maximum restart attempts: The maximum number of restarts allowed within the aggregation time interval. Can be set to an integer greater than 0, default value is 20. |


<span id="31d080af"></span>
## Retry task failure recovery launch

When the Task restart strategy takes effect, if the task still fails, the configured task failure recovery rules will launch operations across the entire task dimension.

The Flink platform has provided task restart strategy configuration functions, but the Failover strategy has a certain learning threshold and is relatively difficult to configure. You can use the task failure retry recovery function, which is easy to configure and understand.


|**Configuration** |**Description** |
|---|---|
|Activate |Whether to activate the Task Failure Retry Launch feature, which is enabled by default.<br><br>To activate this feature, you need to configure the task failure restart rule based on the business scenario, which includes configuring **maximum retry launch attempts** and **retry launch interval**. |
|Maximum Retry Launch Attempts |During task execution, if an abnormality causes the entire task to fail, the system allows a maximum number of retry launches within that task failure's life cycle.<br><br>The default value is 3 times, and it can be set to an integer value within the range (0, 100]. |
|Retry Launch Interval |The interval between two retry launches when a task fails to launch and then fails again.<br><br>The default value is 1 min, and it can be set to an integer value within the range [1, 300]. |


It is important to note that the task failure retry recovery strategy can only be effective if the following conditions are met:


1. The job must have the task failure retry strategy enabled;

2. The job must enable Checkpoint;

3. The job's current instance must have successfully generated at least one Checkpoint or Savepoint.

> Note: If the job failure retry strategy is enabled but the task is not recovered through retry, you can check from several aspects:

> 1. Refer to [Checkpoint 配置](https://docs.byteplus.com/docs/flink/Configure_Flink_Parameters#dbeefb26) check whether Checkpoint is enabled for the task;

> 2. Check for key information in the event logs, such as "Automatic restart is suppressed because the job can only be initiated from new." If found, it may indicate failure to retry bringing up the job instance due to the inability to successfully produce Checkpoint or Savepoint.


<span id="7382afd9"></span>
## Custom Parameters

By setting custom parameters, you can fine\-tune and optimize Flink tasks to better adapt to different business needs and environmental changes. This also enhances the maintainability and flexibility of the tasks. The effectiveness of custom parameters is of lower priority than configurations already filled in the configuration panel.

Here are some example parameter configurations; please set them according to the actual situation.


|**Category** |**Parameter** |**Description** |
|---|---|---|
|Snapshot |savepoint.scheduler.default.interval |The interval for the system to automatically create Savepoints, measured in milliseconds, with a minimum value of 60000 milliseconds.<br><br>After setting the system snapshot interval, the system snapshot feature is activated. The system automatically triggers the creation of task snapshots at each snapshot interval.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only the <strong>Flink 1.11\-byted</strong> version supports system snapshots.</div><br> |
|Access to public networks |kubernetes.jobmanager.annotations.gro.openstudio/network\-policy |When Flink needs to access the internet, you can set this parameter to `external-internet`.<br><br>For information on how to enable Flink to access internet data sources, please refer to [Flink Accessing the Public Internet](https://docs.byteplus.com/docs/flink/Flink_Accessing_the_Public_Internet). |
||kubernetes.taskmanager.annotations.gro.openstudio/network\-policy |When Flink needs to access the internet, you can set this parameter to `external-internet`.<br><br>For information on how to enable Flink to access internet data sources, please refer to [Flink Accessing the Public Internet](https://docs.byteplus.com/docs/flink/Flink_Accessing_the_Public_Internet). |
|Restrict Log Log Levels |env.log.level |Specify the log level for task output, supporting values: trace, debug, info, warn, error, fatal. Once a specific output log level is set, only logs at that level and higher will be displayed in the task log.<br><br>For example, if the log level is set to debug, logs from debug to fatal level will be output.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To update the task output log level, you need to re\-launch and start the task for the configured log level to take effect.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only the log levels output by TaskManager and JobManager can be specified; Client logs are uncontrollable.</div><br> |
|Infer Source parallelism |table.exec.hive.infer\-source\-parallelism<br><br>Or<br><br>table.exec.iceberg.infer\-source\-parallelism |**Flink Batch** jobs that read Hive or Iceberg data will automatically infer Source parallelism.<br><br>The default value is true, indicating automatic inference of parallelism. You can set it to false to disable automatic parallelism inference, in which case the parallelism is determined by the configured settings. |
||table.exec.hive.infer\-source\-parallelism.max<br><br>Or<br><br>table.exec.iceberg.infer\-source\-parallelism.max |**Flink Batch type** tasks reading Hive or Iceberg data, the maximum inferred parallelism of the Source. The default value is 1000. |


<span id="d0115a6a"></span>
## Auto\-tuning

The Flink platform now supports auto\-tuning for Stream type tasks. Once enabled, the system will automatically analyze running tasks and adjust the resource usage of the Flink computation tasks based on the upstream Kafka's Lag, thereby reducing resource consumption.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before enabling task auto\-tuning, the following considerations need to be understood:</div>



* <div data-tips="true" data-tips-type="warning">Only supports activating auto\-tuning for <strong>Flink 1.11</strong> engine version’s <strong>Stream</strong> type tasks.</div>


* <div data-tips="true" data-tips-type="warning">Only supports tasks with <strong>Kafka</strong> as the Source side to enable auto\-tuning.</div>


* <div data-tips="true" data-tips-type="warning">Tasks with auto\-tuning enabled only support running on resource pools charged on a pay\-as\-you\-go basis.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f86398868a849038d3a0a3072981a58~tplv-goo7wpa0wc-image.image) </span>

If you need to enable auto\-tuning for tasks, please configure the relevant parameters according to business conditions.


|**Configuration** |**Description** |
|---|---|
|Ineffective Times |Set the inactive time period for automatic daily tuning, during which smart tuning operates normally but makes no adjustments. |
|Maximum Resource Limit |Set the maximum resource limit that can be expanded when automatically adjusting resources, measured in CU.<br><br>The default value is 100 CU. |
|Adjustment Interval |Set the time interval for tuning to become effective after one restart, measured in minutes.<br><br>The default value is 30 minutes. |


<span id="21fc79c4"></span>
## Dependency Files

Dependency file configuration primarily serves to specify the paths to external files or resources needed for a task. During task execution, required files or resources are automatically loaded and passed on to the relevant components or functions for use.

Click **add**, then choose the method to add dependency files:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15252dc0091348eb8e881edacea9e4ff~tplv-goo7wpa0wc-image.image) </span>


* Select Resource: Choose the target file from the resource library. If files have not been uploaded yet, please see [资源文件管理](https://docs.byteplus.com/docs/flink/Upload_Resource_Files).

* Enter TOS address: Fill in the TOS address to read dependency files from the TOS Bucket, in the format `tos://bucket/path/dependency_file_name`. Example: `tos://test-init/tos_jar/flink-faker-0.5.3.jar`

   When you choose to read dependency files from the TOS Bucket, the Bucket you set needs to be consistent with the Bucket used during Flink product initialization, otherwise the dependency files cannot be read correctly.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When filling out the Bucket, please be aware of the following two notes:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Flink platform historical users: Stay consistent with the TOS Bucket selected during product initialization. You can confirm the Bucket name on the resource pool creation page.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">New Users on the Flink Platform: If you activated a Flink product after February 4, 2024, a TOS Bucket will be automatically generated and bound during product initialization. The format is fixed as <code>byteplus-flink-meta-{account ID}-{region}</code>. Example: <code>byteplus-flink-meta-2100xxxx-cn-beijing</code>.   </div>
   


<span id="386f0c44"></span>
## Variable Scope

When a domain\-specific variable is referenced in SQL code, it is necessary to select the effective variable scope in the Flink parameter configuration. For information on how to create variables, see [Create Variables](https://docs.byteplus.com/docs/flink/Create_Variables).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb58062671724734b3421e9a8c0cc972~tplv-goo7wpa0wc-image.image) </span>

The system will first search for variables in the scope you specify before searching for global variables, with a higher priority given to local scoped variables. If the variable does not exist, an error will occur during execution.


* Global variables: Effective for all task references.

* Scoped variables: Effective only when specified in the task parameter configuration.
