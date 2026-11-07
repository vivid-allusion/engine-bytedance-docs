---
title: "Hermes Agent trace monitoring"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Hermes_trace_monitoring"
---

Hermes Agent is a core runtime component for LLM\-based agent scenarios. It supports natural language parsing, intelligent task decomposition, LLM inference, and external tool calls. Through multi\-round autonomous reasoning and closed\-loop execution, Hermes Agent automatically completes various complex business tasks and provides the basic runtime capabilities for AI applications such as intelligent Q&A, automated O&M, and intelligent analytics. This topic describes how to integrate Hermes observability data into APMPlus so that each Hermes Agent execution is visible, measurable, and traceable.

<span id="9hr7qnIE"></span>
## Background

The APMPlus Hermes plugin is mainly used to collect conversation records, model call records, tool call records, runtime logs, and core metrics of Hermes Agent. The plugin delivers full observability of the agent execution trace, thoroughly resolving the black\-box issue in agent execution processes.

The plugin requires no changes to your existing agent logic and has very low integration cost. After integration, you can observe the full lifecycle of a single request in APMPlus, covering the entire process from user input and LLM calls to external tool execution and final output. You can also continuously monitor various key runtime metrics, including token consumption, model inference duration, tool call duration, response payload size, and end\-to\-end overall duration.

<span id="j33DMnf6"></span>
## Prerequisites

You have obtained the information about the required configuration parameters for integrating Hermes. The detailed parameters and acquisition methods are as follows:


|Parameters |Required |Description |
|---|---|---|
|\-\-region <region\> |Yes |ID of the region for service integration, such as `cn-beijing`. For information about regions currently supported by Server\-side Monitoring, see [Server-launching region](https://docs.byteplus.com/en/docs/apmplus/server-launching_region). |
|\-\-appkey <appkey\> |Yes |The authentication information of Server\-side Monitoring. Although the App Key credential is independent of the integrated service type and data collection method, the App Key differs across workspaces. To obtain App Key, see [How to obtain the AppKey for Server-side Monitoring authentication?](https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication). |
|\-\-service\-name <name\> |Yes |The service name, such as `hermes-agent`. The displayed service name in Server\-side Monitoring, which can be customized based on your needs. |
|\-\-version <version\> |No |Installs the specified plugin version. The default value is latest. Both 0.1.0 and v0.1.0 formats are supported. |
|\-\-non\-interactive |No |Non\-interactive mode. For the first installation or a configuration change, pass \-\-region, \-\-appkey, and \-\-service\-name together. |
|\-\-config\-only |No |Updates only the Hermes configuration without updating the plugin files. |
|\-\-uninstall |No |Uninstalls the plugin and clears the Hermes configuration without uninstalling Python dependencies. |
|\-\-help |No |Displays script help. |


<span id="tBwugpTv"></span>
## Procedure

<span id="Gnx93CfY"></span>
### Step 1: Integrate Hermes


1. This topic provides three Hermes integration methods. You can select an appropriate method based on the actual scenario.

   
   <Tabs>
   <Tab zoneid="Cs0GrQyZfl" title="One-click integration via script">
   <TabTitle>One-click integration via script</TabTitle>
   
   Execute the following command to install the `apmplus-hermes-plugin` plugin with one click, and follow the operation guide to complete the configuration.
   
   ```Shell
   curl -fsSL "https://apmplus-hermes-plugin.tos-cn-beijing.volces.com/install.sh" | bash
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="oCxh6z7eSY" title="Automatic integration via Hermes">
   <TabTitle>Automatic integration via Hermes</TabTitle>
   
   You can send the `apmplus-hermes-plugin` plugin installation and configuration information to Hermes via conversations directly. This enables an automatic installation and configuration process by Hermes. For example:
   
   ```Plain Text
   Execute the following command to install and configure the apmplus-hermes-plugin plugin. Set the region to cn-beijing, the appkey to xxxxxxxxxxx, and use hermes-agent as the service name.
   
   curl -fsSL "https://apmplus-hermes-plugin.tos-cn-beijing.volces.com/install.sh" \
     | bash -s -- --non-interactive --region cn-beijing --appkey xxxxxxxxx --service-name hermes-agent
   ```
   
   
   
   </Tab>
   <Tab zoneid="D2U0DbCjug" title="Script-based integration">
   <TabTitle>Script-based integration</TabTitle>
   
   Install and configure the `apmplus-hermes-plugin` plugin directly via a script and automatic parameter passing. This method is applicable to non\-interactive modes, such as CI and automated environments.
   
   ```Shell
   curl -fsSL "https://apmplus-hermes-plugin.tos-cn-beijing.volces.com/install.sh" \
     | bash -s -- --non-interactive --region cn-beijing --appkey xxxxxxxxx --service-name hermes-agent
   ```
   
   
   &nbsp;
   
   
   
   
   </Tab>
   </Tabs>
   

2. After the installation is complete, manually restart Hermes to ensure that the plugin runs properly. Restart methods vary by environment, and the specific operations are as follows:

   * If you use Hermes Gateway, manually execute the `hermes gateway restart` command to make the plugin take effect.

   * If you use the command line, exit the current session and execute the `hermes` command in a new session.

3. Execute the following command to check the plugin status. If the plugin list contains `apmplus_hermes_plugin` and its status is `enabled`, the integration succeeds.

   ```Shell
   hermes plugins list
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d454d20234bedea6b805595af50e45f6.png) </span>


<span id="ahRE66pb"></span>
### Step 2: View observability data

Interact with Hermes via WebUI or other methods. After the conversation, navigate to the APMPlus console to view the observability data.


1. Navigate to [Service List](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/service/list) and search for the integrated Hermes by service name.

2. Click the service name to access the service details page. On the **Trace analysis ** tab, view the Span list corresponding to the Hermes service.

3. Click the target trace ID and switch to the LLM data or Properties tab to view the details of this request, such as trace details, request model, token consumption, and LLM, tool, and agent turn duration and token consumption.

4. Switch to the **Detailed logs of traces** tab to view detailed logs of the Hermes runtime process.


<span id="mIusp6MK"></span>
## What to do next


* Navigate to[ Preset dashboard](https://console.byteplus.com/observe/dashboard/dashboard/?type=builtin), select ** Hermes observational disk**, and view the preset dashboard provided by APMPlus for Hermes.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the preset dashboards do not meet your monitoring needs, you can also create <a href="https://console.byteplus.com/observe/dashboard/dashboard?">custom dashboards</a> based on your actual requirements.   </div>
   

* Navigate to the [Alerting task](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/alarm/tasklist) page and click **Create alerting task**. You can configure automated alert monitoring for Hermes observability metrics based on your needs, such as token consumption, session lag, LLM duration, tool duration, agent turn duration, and error calls. Configuring alert tasks helps monitor target service metrics for exceptions and ensures timely notifications, helping you keep track of Hermes operational status.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Alert tasks allow you to monitor corresponding metric values. An alert notification is automatically sent when the configured conditions are met. For detailed information about alert tasks, see <a href="https://docs.byteplus.com/en/docs/apmplus/Alert_tasks">Alert tasks</a>.   </div>
   

* The following management operations are available for the` apmplus-hermes-plugin `plugin.

   
   <Tabs>
   <Tab zoneid="Al9WiTPwa1" title="Update plugin">
   <TabTitle>Update plugin</TabTitle>
   
   Execute the plugin installation command again. After completion, restart Hermes to update the plugin.
   
   
   * If the plugin has been installed, only the plugin itself is updated by default, and the existing region, appkey, service name, and other configurations will be retained. Execute the following command:
   
      ```Shell
      curl -fsSL "https://apmplus-hermes-plugin.tos-cn-beijing.volces.com/install.sh" | bash
      ```
      
   
   * To update the plugin to a specified version, for example, version 0.1.0, execute the following command:
   
      ```Shell
      curl -fsSL "https://apmplus-hermes-plugin.tos-cn-beijing.volces.com/install.sh" \
        | bash -s -- --version 0.1.0
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="AiarVNf1Ef" title="Modify configuration">
   <TabTitle>Modify configuration</TabTitle>
   
   * To modify the reporting configuration without updating the plugin file, execute the following command:
   
      ```Shell
      curl -fsSL "https://apmplus-hermes-plugin.tos-cn-beijing.volces.com/install.sh" \
        | bash -s -- --config-only --region cn-beijing --appkey xxxxxxxxx --service-name hermes-agent
      ```
      
   
   * To update the plugin and overwrite the configuration, execute the following command:
   
      ```Shell
      curl -fsSL "https://apmplus-hermes-plugin.tos-cn-beijing.volces.com/install.sh" \
        | bash -s -- --region cn-beijing --appkey xxxxxxxxx --service-name hermes-agent
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="bdLFVZMTYZ" title="Uninstall plugin">
   <TabTitle>Uninstall plugin</TabTitle>
   
   To uninstall the `apmplus-hermes-plugin` plugin, execute the following command and restart Hermes in sequence.
   
   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
   
   
   
   * <div data-tips="true" data-tips-type="warning">Uninstalling the plugin deletes the plugin directory and removes the plugin name from <code>plugins.enabled</code>, <code>plugins.disabled</code>, and the <code>apmplus_hermes_plugin</code> configuration in Hermes.</div>
   
   
   * <div data-tips="true" data-tips-type="warning">Since Python dependencies may be reused by other plugins, they will not be uninstalled.</div>
   
   
   
   ```Shell
   curl -fsSL "https://apmplus-hermes-plugin.tos-cn-beijing.volces.com/install.sh" \
     | bash -s -- --uninstall
   ```
   
   
   
   </Tab>
   <Tab zoneid="EypbnzfVJD" title="Common toggles">
   <TabTitle>Common toggles</TabTitle>
   
   * You can disable input and output body collection. Sensitive fields are masked by default. After disabling, common fields such as Token, Password, Secret, Authorization, api_key, and other fields will not be directly exposed in plain text.
   
      ```YAML
      apmplus_hermes_plugin:
        trace_content: false
      ```
      
   
   * You can disable log or metric collection. Log or metric collection is enabled by default. You can disable this configuration based on your needs.
   
      ```YAML
      apmplus_hermes_plugin:
        logs: false
        metrics: false
      ```
      
   
   
   
   
   
   </Tab>
   </Tabs>
