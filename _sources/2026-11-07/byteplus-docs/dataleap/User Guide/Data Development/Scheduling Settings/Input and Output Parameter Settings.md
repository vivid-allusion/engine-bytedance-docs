---
title: "Input and Output Parameter Settings"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/input_and_output_parameter_settings"
---

DataLeap supports the transfer of parameters between upstream and downstream tasks by setting input and output parameters for tasks. The content values of these parameters can be sourced from the execution results of upstream tasks, project parameters, or custom parameter values. This document will introduce how to configure upstream task output parameters and downstream task input parameters.

<span id="fd30f4e2"></span>
## 1 Usage Restrictions

Only supported for Shell and Python tasks. The execution result obtained from the last line of stdout/error is set as the output variable parameter and passed to downstream tasks through the "outputs" parameter as input parameter variables.

<span id="b27b59f4"></span>
## 2 Usage Preconditions


* When using the running results of upstream tasks as input parameters for downstream tasks, it is required to first set up the upstream and downstream task scheduling dependencies. Scheduling dependency configuration operations are detailed [Task scheduling depends on](https://docs.byteplus.com/docs/dataleap/scheduling_dependencies)here.

* When using project parameters as input parameters for downstream tasks, it is first necessary to set project parameters in the Project Console. See details in [Parameter Information Settings](https://docs.byteplus.com/docs/dataleap/parameter_information_setting).


<span id="e03f7ab1"></span>
## 3 Input and output parameter configuration entry


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. In the **Task Development** interface, access the **Schedule Settings** button for a specific batch task. Find the **Input and Output Parameters** section to perform configuration.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4299049c8ba846be8cbb0bfc59cf40e5~tplv-goo7wpa0wc-image.image) </span>

<span id="2023ff35"></span>
## 4 Usage of Parameters

After setting input parameters in the task, they can be used internally in the task, which is different from the usage of time parameters:


* Time parameters are used through the ${} approach, see [Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252);

* Other input parameters are used through the {{Parameter name}} approach.


<span id="6c5b50c3"></span>
## 5 Configuration of Input Parameters

Configuration of input parameters is specifically divided into the following three categories:

<span id="55748d5c"></span>
### 5.1 Use the execution results of upstream tasks as output parameters

Support passing the last line of stdout/err execution results of Shell and Python tasks as output variable parameters through "outputs".


1. In the **Schedule Settings \> Task Output Parameters** of upstream task A, select "**Use the running results as output**" and use "**outputs**" to treat the execution result as an output.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The content of the last line of stdout/err will be saved in the output parameters.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The remote shell only stores the contents of stdout in the output parameters.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae55fb2d34754a7f8834c5baea3868bb~tplv-goo7wpa0wc-image.image) </span>

2. For downstream task B, manually add upstream task A as a parent dependency in **Schedule Settings \> Dependencies**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4a96e3fa8644fc98197e2c941f071e1~tplv-goo7wpa0wc-image.image) </span>

3. For downstream task B, in the **Schedule Settings \> Task Input Parameters**, click the **add manually** button to enter the input parameter adding window.

4. Set the following information in the window:

   * Parameter name: Enter the parameter name used in task B.

   * Parameter type: Select the **task** type from the dropdown.

   * Source task: Choose the upstream task A that has been added as a dependency from the dropdown.

   * Specific parameters: Select or input vaguely the name of the upstream output from the dropdown: **outputs;** 

   * Parse Replacement Values: During debug parsing, the system does not fetch the real content of outputs from upstream; it uses "**Parsed replacement values**" instead. The default value is 1, and users can replace it as needed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da74c7d9bc384b03bade4a9dace5c35b~tplv-goo7wpa0wc-image.image) </span>

5. Once parameters are added, you can use them in the code editing interface in the form of {{Parameter name}}; time parameters are used in the format ${}.


<span id="fa635609"></span>
### 5.2 Treat parameters set in the project as inputs

Manually add parameters in the input parameters, making them available globally for the project.


1. In the **Project Console \> Parameter Information**, create new project parameters; see details [Parameter Information Settings](https://docs.byteplus.com/docs/dataleap/parameter_information_setting).

2. In the **Task Input Parameters** interface, click the **add manually** button to enter the input parameters addition window:

   1. Parameter Name: Enter the name of the parameter used in the task;

   2. Parameter Type: Select the **Project** type from the dropdown;

   3. Source: Choose or type in the name of a newly created project parameter from the dropdown.


For detailed use cases of project parameters, see [Use Case](https://docs.byteplus.com/docs/dataleap/parameter_information_setting#_3-%E4%BD%BF%E7%94%A8%E6%A1%88%E4%BE%8B) details.

<span id="06dd4020"></span>
### 5.3 Input custom parameters as input.

Input parameters also support passing values upstream and downstream through custom parameter content.

In the **Task Input Parameters** interface, click the **add manually** button to enter the parameter addition window.


* Parameter name: The name of the parameter used in the input task.

* Parameter type: Choose from the dropdown **Custom** type.

* Value: Enter the custom parameter value.


For custom parameter use cases, see [3.4 Parameter settings](https://docs.byteplus.com/docs/dataleap/serverless_flink_sql#_3-4-%E5%8F%82%E6%95%B0%E8%AE%BE%E7%BD%AE).

<span id="b832c15c"></span>
## 6 **Output Parameters**.

Set the output parameters of the task. Once the output parameters are defined and the task is activated, they can be used in downstream nodes as the value of input parameters. Output parameters are categorized into two types: constants and variables.


* Constant values: Constants are fixed strings and need to be defined in the task's output parameters.

* Variable values: Include [5 Configuration of Input Parameters](https://docs.byteplus.com/docs/dataleap/input_and_output_parameter_settings#6c5b50c3) and globally supported variables by the system.

   The globally supported variables by the system do not need to be defined in the output parameters; they are provided by the system and specifically include the following:

   * {{taskId}}: Task ID

   * {{taskType}}: Task type

   * {{taskName}}: Task name

   * {{taskOwner}}: Task owner

   * {{instanceId}}: Instance ID

   * {{taskTime}}: The corresponding Task time for the instance

   * {{scheduleRunTime}}: Scheduled run time of the instance

   * {{startTime}}: Actual start time of the instance

   * {{endTime}}: Actual end time of the instance

   * {{instanceStatus}}: Instance state

   * {{triggerType}}: Trigger type, including system scheduling and reruns

   * {{trackingUrl}}: Execution Tracking URL of the instance


<span id="c18e09e9"></span>
## 7 Subsequent Actions

Once the input and output parameter configurations are complete, you can start debugging the task or submit it for release. See details [4 Commit for Deploy](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-%E6%8F%90%E4%BA%A4%E4%B8%8A%E7%BA%BF).
