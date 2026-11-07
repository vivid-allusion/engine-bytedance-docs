---
title: "Notebook"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/notebook"
---

An interactive development environment designed to support user data development and data exploration scenarios. The Notebook is custom\-developed based on the open\-source JupyterLab platform. It supports Python, Bash, and Markdown languages, enables integration of third\-party libraries for data and algorithm development, and allows publishing data and algorithm development results as tasks for scheduled execution. This article will introduce how to create a Notebook scheduling task on the DataLeap platform.

<span id="_2-前提条件"></span>
## 1. Usage restrictions


* The Kernel type of Spark on EMR Serverless can only be executed via **Public Computing Resource Group**. For practical implementation, refer to [4 Configure tasks](https://docs.byteplus.com/docs/undefined/689db5998d8d50053b67195e#_5-%E9%85%8D%E7%BD%AE%E4%BB%BB%E5%8A%A1).


<span id="_3-新建任务"></span>
## 2 Create a task


1. Log in to the [DataLeap tenant console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/overview?) **.** 

2. In a specific project, enter the **data development** interface to perform the creation operation for a new **Interactive analysis** task type.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Task names may only contain period (.), letters, numbers, underscore (_), hyphen (\-), [],【】, ( ), （）, and Chinese characters. The name must not exceed 127 characters.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b052c9fe23c4a6382a9516e3efaeb6d~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-任务配置"></span>
## 3 Task configurations

<span id="_4-1-配置环境启动信息"></span>
### 3.1 Configure the environment startup information

After creating a new task, when opening Notebook for the first time, you must first configure the environment startup information.

Parameters with an asterisk (\*) before the name are required, while those without an asterisk are optional.


<Tabs>
<Tab zoneid="yfuhq1GVxB" title="Python on K8s">
<TabTitle>Python on K8s</TabTitle>


|Parameter |Description |
|---|---|
|\*Select kernel |A Notebook Kernel is a computing engine that executes the code contained in a notebook file. For example, the ipython kernel executes Python code.<br><br>Supports selecting the Python on K8s, and Spark on EMR Serverless kernel types.<br><br>After opening a Notebook task and configuring the environment, the Kernel will start automatically by default. Alternatively, you can select the option below, "Do not start the Kernel automatically by default when opening a Notebook task," so that the Kernel will not start automatically for now. Start the Kernel. When running code, the Kernel performs computations and produces results. |
|\*Computing resource group |Supports selecting a public computing resource group and a [dedicated computing resource group](https://docs.byteplus.com/en/docs/dataleap/exclusive_computing_resource_group). |
|\*Image |Supports entering a custom image address for the dependencies required by the task. The default image address filled by the platform is dataleap\-johor\-ap\-southeast\-1.cr.volces.com/studio/notebook_runtime:online. It comes with commonly used third\-party libraries pre\-installed. To install additional Python third\-party libraries, you can execute pip commands via tasks. For example: `pip install emoji`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the default image address, the value {region} must be replaced with the actual region information according to your actual region, for example, johor\-ap\-southeast\-1.</div><br> |
|\*Resource configuration |You can configure resources according to your actual requirements, using CU as the unit. The default configuration is 1 CU (1 CU = 1 Core, 4 GB). You can select additional resource specifications.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the 0.25 and 0.5 CU specifications, only the <strong>Exclusive computing resource group</strong> can be selected.</div><br> |



</Tab>
<Tab zoneid="OJhra5RRBN" title="Spark on EMR Serverless">
<TabTitle>Spark on EMR Serverless</TabTitle>


|Parameter |Description |
|---|---|
|\*Select kernel |A notebook kernel is the computational engine that executes the code contained in a notebook file, for example, the IPython kernel executes Python code.<br><br>Supports selecting the following kernel types: Python on K8s, and Spark on EMR Serverless.<br><br>When you open a Notebook task and configure the environment, the Kernel will start automatically by default. Alternatively, you can select the "Do not start Kernel automatically when opening Notebook task" option below to temporarily prevent the Kernel from starting. Start the Kernel. When you run code, the Kernel performs computations and produces results. |
|\*Compute resource group |Supports selecting a public compute resource group.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Can only be executed via the <strong>public compute resource group</strong>.</div><br> |
|\*Image |Supports entering a custom image address for the dependencies required by the task. The default image address pre\-filled by the platform is dataleap\-{region}.cr.volces.com/studio/notebook_runtime:online, which comes with commonly used third\-party libraries pre\-installed. To install additional Python third\-party libraries, you can run pip commands in tasks. For example: `pip install emoji`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the default image address, the value of {region} must be replaced with the actual region information as appropriate, for example, johor\-ap\-southeast\-1.</div><br> |
|\*Queue |Select Spark compute queue information that has already been added to the project from the dropdown menu.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">In Notebook query jobs, for Spark queue information, you must select a queue with sufficient resource capacity from the <strong>Default Compute Group</strong> to start the Kernel. Notebook tasks do not support using SQL Compute Group resource capacity. You also need to add the parameter <code>tqs.query.engine.type = sparkcli</code> to the Spark parameters below. <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3b9b04a3e714b6cb958c275c3c89156~tplv-goo7wpa0wc-image.image" width="2044px" /></div><br> |
|Spark parameters |Enter the Spark parameters that are required for the task execution environment. You can configure them as follows:<br><br><br>* Single\-line edit mode: Enter parameter key\-value pairs in the corresponding input field.<br><br>   Here, the value can be configured either by custom definition or in the form of a project parameter {{value}}. If you want the same codebase to automatically distinguish between different engine environment parameters and project parameters across different execution environments, or if you need to transmit sensitive information using encrypted parameters, you can address these scenarios by configuring project parameters in the value.<br><br>   Project parameters can be configured in the This **Project Console \> Parameter Information** interface. For detailed instructions, see [Parameter Information Settings](https://docs.byteplus.com/en/docs/dataleap/parameter_information_setting).<br><br>* Script editing mode: Supports JSON and YAML formats, allowing you to configure parameters directly using scripts. When configuring project parameters, you can also use the {{value}} format.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When running Spark query tasks on EMR Serverless and accessing TOS resources or Spark queue resources, sub\-users must perform the required authentication operations. Therefore, you must add the AK/SK information of an account with permissions to access TOS buckets and Spark queues to the parameters, using the following format:</div><br><br><br><div data-tips="true" data-tips-type="warning"><code>serverless.spark.access.key: xxxxxxx</code></div><br><br><br><div data-tips="true" data-tips-type="warning"><code>serverless.spark.secret.key: xxxxxxx</code></div><br><br><br><div data-tips="true" data-tips-type="warning">You can obtain the AK/SK information by going to the <a href="https://console.byteplus.com/iam/keymanage">key management interface</a> in the access console and copying the Access key ID and Secret Access Key information. If you are a sub\-user, please contact the main account to obtain the key. For details on TOS authentication, see <a href="https://docs.byteplus.com/en/docs/tos/docs-permission-configuration-guide">TOS Permission Configuration</a>.</div><br> |



</Tab>
</Tabs>


After completing the startup information configuration, click the **OK** button to initiate the Kernel connection. Wait until the Kernel status in the navigation bar is Idle; this indicates that the startup was successful. You can then proceed with subsequent debugging and running your code.


* Kernel status description:

   * Idle state: The kernel is in idle state and can run tasks at any time.

   * Busy status: Code is currently running and the kernel is busy. Please wait until the current code execution is complete before running subsequent tasks.

   * Disconnected state (network disconnected): There are situations where the Kernel is disconnected from the network. You need to manually refresh the interface. After starting the Kernel, execute the task.

   * Connection status: connected. The Kernel is currently connected.

   * Dead state: Connection failed state. You can view the failure reason on the right.

* You can click the Kernel button to replace the advanced **Kernel** settings.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a671b310a974829b867b260837b0d76~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-编辑任务"></span>
### 3.2 Edit tasks

After the Kernel has started and its status is normal, you can begin code development. Python, Markdown, Bash, and Raw are currently supported.


* You can enter code logic for the corresponding language in the current cell. For example, using Python:

   ```python
   View pre-installed third-party packages
   Set the cell type to Python and perform the following operations
   !pip3 list
   
   # How to install third-party packages
   # Select the Python cell type and perform the following operations, using the installation of library_name as an example
   !pip3 install  library_name
   ```
   

* Example code – use Plotly to create plots

   ```plaintext
   !pip3 install plotly
   
   import plotly.express as px
   df = px.data.iris()
   fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species")
   fig.show()
   ```
   

* Parameters:

   In the code editor, you can enter dynamic variables, system variables, project parameters, and so on, such as time parameters ${date} and ${hour}. For usage of time parameters, refer to [Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252); for details on how to use project parameters, see [Input and Output Parameter Settings](https://docs.byteplus.com/docs/dataleap/input_and_output_parameter_settings).

   You can select the business date at the bottom of the interface, then click the **Run** button at the top of the interface to complete the time parameter replacement operation during the query.

* Cell box function buttons:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/974db79a5b85498983e9f1d8eaa8ef6d~tplv-goo7wpa0wc-image.image) </span>

   
   |No. |Parameters |Note |
   |---|---|---|
   |1 |Language selection |You can select Python, Bash, Markdown, or Raw as the language. |
   |2 |Format Cell |Format the written code |
   |3 |New Cell |Add a new Cell. |
   |4 |Copy Cell and Paste Below Cell |Copy the content and paste it after the current cell. |
   |5 |Cut Cell |Cut the current cell. |
   |6 |Paste Below Cell |Paste content after the current cell. |
   |7 |Delete Cell |Delete the current cell. |
   |8 |Right\-click actions for cells |To access more quick actions for the unit box, right\-click inside the Cell box to view additional options.<br><br>Among them, the **Enable Notebook Vim mode** option can **enable or disable** Vim mode for the editor. |
   


<span id="_4-3-执行设置"></span>
### 3.3 **Execution settings**


1. Click to open the **Execution Settings** window in the right sidebar.

2. Select a computing resource group: For different Kernel types, you can select or modify the public computing resource group and [Exclusive Computing Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group).

3. Image address: For the Python on K8s and Spark on EMR Serverless kernel types, you can select the default image address, which comes with commonly used third\-party libraries pre\-installed.

4. Resource configuration: Resources can be configured according to actual requirements, using CU as the unit. The default configuration is 1 CU (1 CU = 1 Core and 4 GB). Additional resource configurations can be selected from the dropdown menu.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Among them, only dedicated compute resource groups support the selection of the 0.25 CU and 0.5 CU specifications.   </div>
   

5. Spark parameters: For the Kernel types **Python Spark on EMR and Spark on EMR Serverless**, you can add the Spark parameters required by the task in the task execution environment. You can configure them in the following ways:

   * Single\-line edit mode: In the corresponding input field, enter the parameter key\-value pair. The value can be configured in the form of **custom**, **project parameter**, or `{{value}}`. For details, see [4 Configure tasks](https://docs.byteplus.com/docs/undefined/689db5998d8d50053b67195e#_5-%E9%85%8D%E7%BD%AE%E4%BB%BB%E5%8A%A1).

   * Script editing mode: Supports JSON and Yaml formats, allowing parameters to be configured directly using scripts.

6. Task output data registration:

   Output data registration is used to record the data lineage of a task and does not affect code logic. If a Notebook task contains output corresponding to engine database table data, it is strongly recommended to provide this information to facilitate subsequent maintenance of task data lineage.

   * Engine type: Select the appropriate data engine type based on the actual situation, such as EMR (EMR Hadoop, EMR Doris, EMR StarRocks engines), ByteHouse, EMR Serverless Spark, EMR Serverless StarRocks, or Default (no output registration).

   * Associate instances: Select the instance information under the corresponding engine for association.

   * Data type: Select the output data type for the corresponding engine type.

   * Database tables: Select the detailed name information of the databases and tables generated by the corresponding engine.


<span id="_4-4-调度设置"></span>
### 3.4 Scheduling settings

Go to the right sidebar **Scheduling settings**. Configure properties related to node scheduling. For details on configuration operations, see [scheduling settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_settings).

<span id="_6-提交发布任务"></span>
## 4. Debug and submit the release task


1. After task configuration is complete, you can click the **Save** and **Run/Run All** buttons in the operation bar to debug the task.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After debugging is successful and the kernel becomes idle, if no one initiates another debugging session afterwards, or if the debugging Tab is closed, resources will be released within three hours for use by other tasks.   </div>
   

2. After confirming that the debugging results are correct, click the **Submit for launch** button in the toolbar above. In the **Submit for launch** dialog box, select parameters such as **Backtracking Data, Monitoring Settings, Submission Settings**, and other parameters. Finally, click the **Confirm** button to complete the job submission. For detailed instructions on submitting and releasing, see [4.1 Submit Batch Task](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-1-%E7%A6%BB%E7%BA%BF%E4%BB%BB%E5%8A%A1%E6%8F%90%E4%BA%A4).


For details on the operation and maintenance of subsequent tasks, see [Task Operation](https://docs.byteplus.com/docs/dataleap/task_operation).
