---
title: "Dolphin Serverless task output JobID"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Dolphin_Serverless_task_output_JobID"
---

When executing Dolphin Serverless tasks on Volcano Engine EMR, the current version supports outputting the task's JobID, making it easier for downstream nodes to retrieve it. This article introduces how to output the JobID of Dolphin Serverless tasks to downstream nodes.

<span id="424243bb"></span>
# context

In certain business scenarios, it is necessary to collect information about running Serverless tasks to facilitate data association (upgrading to lineage). At this point, you can obtain the Serverless JobID of the Serverless task node. In Dolphin's design, it is possible to use custom variables (OUT) so that upstream nodes save certain parameters in the workflow context, allowing downstream nodes to retrieve them during execution. Therefore, for Serverless task nodes, after execution is complete, the Serverless task ID is output to the context to enable downstream nodes to retrieve the task ID for information collection purposes.

<span id="575bd437"></span>
# Dolphin dependency package update

<span id="ea557a84"></span>
## Download dependency package

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8025fd9023e54af8aeb0ad2c7ea4279a~tplv-goo7wpa0wc-image.image" name="dolphinscheduler-task-volcanoemrserverless-3.1.9.jar">dolphinscheduler-task-volcanoemrserverless-3.1.9.jar</Attachment>


&nbsp;

<span id="63678ed5"></span>
## Update Dolphin master\-server

```Bash
# Replace with the package downloaded above
unzip serverless-plugin.zip

# Replace with the actual dolphin user directory
chown -R dolphinscheduler:dolphinscheduler serverless-plugin
# Replace with the actual dolphin_scheduler master-server path
cp -rp serverless-plugin/. /usr/lib/emr/current/dolphin_scheduler/master-server/libs
```


<span id="8dfdead9"></span>
## Update Dolphin worker\-server

```Bash
# Replace with the package downloaded above
unzip serverless-plugin.zip

# Replace with the actual dolphin user directory
chown -R dolphinscheduler:dolphinscheduler serverless-plugin

# Replace with the actual dolphin_scheduler worker-server path
cp -rp serverless-plugin/. /usr/lib/emr/current/dolphin_scheduler/worker-server/libs
```


<span id="1673c6d0"></span>
## Update Dolphin api\-server

```Bash
# Download the package
unzip serverless-plugin.zip

# Replace with the actual dolphin user directory
chown -R dolphinscheduler:dolphinscheduler serverless-plugin

# Replace with the actual dolphin_scheduler api-server path
cp -rp serverless-plugin/. /usr/lib/emr/current/dolphin_scheduler/api-server/libs

# First, back up the original UI artifact
mv /usr/lib/emr/current/dolphin_scheduler/api-server/ui /usr/lib/emr/current/dolphin_scheduler/api-server/ui-bak
# Replace with the UI provided by serverless
mv serverless-plugin/ui /usr/lib/emr/current/dolphin_scheduler/api-server/ui
```


<span id="41d48ec8"></span>
# Output Dolphin Serverless task JobID

After completing the above preparation, you can output the Job ID of the current Serverless task node as follows.

<span id="4ae6600f"></span>
## Task configuration


1. Add custom parameters in the Serverless task node. The requirements for custom parameters are as follows.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37555bd27b19401bb164546de7cab73a~tplv-goo7wpa0wc-image.image) </span>

   * The parameter name can be arbitrary.

   * Set the parameter direction to OUT, which means it will be output to downstream nodes.

   * The parameter type should be VARCHAR.

   * The parameter value must be `${emr_serverless_job_id}` **,**  and after the node runs successfully, the parameter value will be replaced with the corresponding Serverless JobID.

2. When there are multiple Serverless nodes, you can assign different parameter names for the output JobID custom parameter of each node to avoid overwriting.

   For example, as shown in the figure below, there are three Serverless task nodes, each configured with an output Job ID parameter name: spark_1, spark_2, and spark_3.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/481ff6ad076f48bb9517e0d81719a24a~tplv-goo7wpa0wc-image.image) </span>

3. In the final shell node, print all Serverless Job IDs in the workflow.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84ee2ca4fd06407790214a017580b4e1~tplv-goo7wpa0wc-image.image) </span>


<span id="0abafb01"></span>
## View and use the output Job ID


1. After the workflow is completed, you can see the JobID of the current task in the EMR Serverless console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c92c85698665474e92e5db4508c4d59c~tplv-goo7wpa0wc-image.image) </span>

2. At the same time, you can see the JobID of the upstream Serverless task in the logs of the downstream shell node in the workflow.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dadebf411fe249d68e083e3a8f8e2fb8~tplv-goo7wpa0wc-image.image" width="1491px" />   </div>
   

3. The Serverless Query SDK can retrieve task information, logs, and Tracking URL information using the Job ID. For documentation, refer to: [Java Query SDK](https://docs.byteplus.com/docs/E-MapReduce/109180).
