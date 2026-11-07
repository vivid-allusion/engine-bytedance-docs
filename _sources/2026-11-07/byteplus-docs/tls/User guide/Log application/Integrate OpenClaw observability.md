---
title: "Integrate OpenClaw observability"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Integrate_OpenClaw_observability"
---

This section uses OpenClaw, which integrates large model observability, as an example to explain how to integrate log applications.

<span id="a5b07e4e"></span>
## Overview

TLS supports one\-click integration with OpenClaw, enabling you to quickly obtain OpenClaw application log data, automatically create log topics, and categorize data for storage.

Through dashboards such as the OpenClaw observability dashboard, operations observability, Trace call chain, and CacheTrace log analysis provided by log applications, you can quickly monitor the running status of OpenClaw, perform troubleshooting, analyze token usage, and more.

<span id="30417856"></span>
## Instructions


|Category |Description |
|---|---|
|Version restrictions |* OpenClaw: version 2026.3.8 and later.<br><br>* Node.js: version 22.x and later (if a higher version is required, follow the OpenClaw prompt). |
|Region restrictions |The server where OpenClaw is deployed and TLS must be in the same region. |
|Authentication method |Configuring OpenClaw access to TLS supports the following authentication methods:<br><br><br>* AK/SK: AccessKey ID and AccessKey Secret of the BytePlus account.<br><br>   * Supports automatic creation of TLS resources (Project/App/Topic) and automatically generates log topic IDs.<br><br>   * Suitable for single\-machine trial and joint debugging.<br><br>* API Key: An important credential for requesting BytePlus TLS, used only for reporting Log, Metric, and Trace data.<br><br>   * Permissions are strictly limited and automatic creation of TLS resources is not supported.<br><br>   * Suitable for multi\-data center and scenarios with strict permission control.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>API Key</strong> is an invitation\-only feature. If you have related business requirements, contact your account manager to be added to the allowlist.   </div><br>    |
|Sensitive information handling |TLS will perform best\-effort masking for common sensitive fields and truncate excessively long content to reduce risk. |


<span id="107fbe80"></span>
## Prerequisites


* OpenClaw has been deployed. 

* The BytePlus managed Prometheus service (VMP) has been enabled. For details, see [Managed Prometheus quick start](https://docs.byteplus.com/en/docs/vmp/Quick-start).

* A log project has been created (such as `demo-openclaw-project`). For details, see [Log project](https://docs.byteplus.com/docs/tls/Managing_projects).

* Depending on the authentication method, you have obtained the user's Access Key ID, Secret Access Key, or APIKey. For details, see [Preparation before installation](https://docs.byteplus.com/docs/tls/Integrate_OpenClaw_observability#ca685f17).


<span id="ff00da95"></span>
## 1 Integrate TLS log applications


1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the TLS region.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **App Marketplace** tab, select the log application to be integrated. For example, on the **OpenClaw** card, click **Integrate**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using the OpenClaw log application for the first time, you need to enable the managed Prometheus service (VMP). You can follow the prompts on the interface to proceed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Using the managed Prometheus service will incur charges. For details, please refer to <a href="https://docs.byteplus.com/en/docs/vmp/billing-overview">Prometheus billing overview</a>.   </div>
   

5. Configure the following integration parameters, then click **Integrate**.

   
   |Parameter |Example |Description |
   |---|---|---|
   |Name |openclaw_observability |The name for application integration.<br><br><br>* Can only contain Chinese, letters, numbers, underscores`_`, and hyphens`-`.<br><br>* Cannot start or end with a hyphen`-`.<br><br>* Length must be 3–64 characters. |
   |Description |Integrate openclaw logs. |Description information for application integration.<br><br><br>* Length limit is 0–64 characters.<br><br>* Angle brackets <\>, apostrophes ', backslashes , double quotation marks ", and emojis are not supported. |
   |Project |demo\-openclaw\-project |Select the log project for storing data. |
   

6. After successful integration, you will be directed to the log application's dashboard page by default.


<span id="ac4b166c"></span>
## 2 Install the TLS OpenClaw plugin

<span id="ca685f17"></span>
### Preparation before installation

The TLS OpenClaw plugin `diagnostics-tls` supports both interactive installation and one\-click installation. You can choose the appropriate method depending on your needs. Prepare the following information before installation and configure as needed:


* Interactive installation: After entering the installation command, follow the prompts to manually configure authentication methods, log topics, and other information to install the plugin.

* One\-click installation: Configure authentication methods and log topics in the installation command. The system will automatically install the plugin with minimal system interaction.



|Parameters |Required |Description |
|---|---|---|
|region |Required |Region ID information for storing observable data.<br><br><br>* For supported Region information, refer to [Service address](https://docs.byteplus.com/docs/tls/endpoint).<br><br>* Ensure that the server where OpenClaw is deployed and TLS are in the same region. |
|ApiKey or AK/SK |Required |Select one authentication method for accessing TLS:<br><br><br>* ApiKey: This is an invite\-only feature. For related business needs, contact your account manager to enable allowlist access.<br><br>* AK/SK: Obtain from the BytePlus console [Key Management page](https://console.byteplus.com/iam/keymanage/). It is recommended to use IAM user keys. Ensure that the user has the necessary permissions. For details, refer to [IAM overview](https://docs.byteplus.com/docs/tls/Managing_permissions_on_Identity_and_Access_Management). |
|Log application topic list |Optional |Configure the log topics to be collected for this log application as needed.<br><br>After integrating the OpenClaw log application, select **Common features** \> **Log application**, click the corresponding log application name in **My applications**, and retrieve it from the **Topic list** tab.<br><br><br>* topic\-id\-app\-log: Log topic ID for **App logs**.<br><br>* topic\-id\-audit\-log: Log topic ID for **Configuration logs**.<br><br>* topic\-id\-session: Log topic ID for **Session logs**.<br><br>* topic\-id\-trace: Log topic ID for **Trace logs**.<br><br>* topic\-id\-metric: Log topic ID for **Metric**.<br><br>* topic\-id\-cache\-trace: Log topic ID for **CacheTrace logs**. Ensure that Cache\-Trace log collection is enabled. <br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only data from configured log topics is collected. At least one corresponding log topic must be configured; otherwise, no data may be displayed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you are not sure which log topic data to collect, you can select <strong>App log</strong>, <strong>configuration log</strong>, and <strong>Trace log</strong>. This is a combination of high information density for troubleshooting and root cause analysis.</div><br> |


<span id="4a5e575b"></span>
### One\-click installation

On the server where OpenClaw is deployed, execute the following command:


* ApiKey authentication method

   ```Shell
   npm exec -y --package=@volcengine/diagnostics-tls-install -- diagnostics-tls-install \
     --non-interactive \
     --region <your-region> \
     --api-key <your-api-key> \
     --topic-id-app-log <Applog TopicID> \
     --topic-id-audit-log <configuration log TopicID> \
     --topic-id-cache-trace <CacheTracelog TopicID> \
     --topic-id-session <Sessionlog TopicID> \
     --topic-id-trace <Tracelog TopicID> \
     --topic-id-metric <Metric TopicID>
   ```
   

* AK/SK authentication method

   ```Shell
   npm exec -y --package=@volcengine/diagnostics-tls-install -- diagnostics-tls-install \
    --non-interactive \
    --region <your-region> \
    --project-name <project-name> \
    --app-name <app-name> \
    --ak <your-ak> \
    --sk <your-sk>
   ```
   


<span id="fb5c4f79"></span>
### Interactive installation


1. On the server where OpenClaw is deployed, execute the following command (from any directory):

   ```Bash
   npm exec -y --package=@volcengine/diagnostics-tls-install -- diagnostics-tls-install
   ```
   

2. Configure installation parameters and wait for the plugin installation to complete.

   Follow the prompts to select Region, authentication method (ApiKey, AK/SK), App log ID, log configuration ID, and other parameters. For parameter details, please refer to [Preparation before installation](https://docs.byteplus.com/docs/tls/Integrate_OpenClaw_observability#ca685f17).

3. After the plugin installation is complete, run the following command to restart the OpenClaw Gateway.

   ```Shell
   openclaw gateway restart
   ```
   


<span id="014bdec0"></span>
## Step 3: View the OpenClaw observability dashboard


1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **My applications** tab, click the name of the OpenClaw log application that has been integrated.

5. On the log application dashboard page, view the dashboard.

   The OpenClaw log application dashboard includes the following dashboard charts:

   
   |Dashboard |Note |
   |---|---|
   |OpenClaw observability dashboard |Displays data such as cost analysis, performance analysis, security audit, conversation count, total tokens, average token consumption per conversation, total cost, host cost distribution, and more.<br><br>Suitable for viewing trends first, then confirming exception metrics. |
   |Operations observability |Exception log analysis, Gateway configuration change statistics, exit count, error trends, and root cause drill\-down.<br><br>Suitable for troubleshooting during on\-call shifts. |
   |Trace call chain |Tracks the call chain for a single conversation, identifies slow points and error points, and supports span\-level analysis and attribute viewing.<br><br>Used for in\-depth analysis of the duration and detailed process of a single conversation. |
   |CacheTrace analysis |Based on CacheTrace logs, assists in analyzing context cache and performance issues. |
   |Topic list |View the Topic list and associated resources for the corresponding OpenClaw application. |
   |Access management |View access instance information. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Common analysis workflow:   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Use <strong>Operational Observability</strong> to identify the exception time window and scope of impact (such as instances, channels, models, sessions, and more).   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the <strong>distributed trace</strong>, determine in which span the slowdown occurs—whether in agent, tool, llm, or subagent—and confirm whether there are retries, timeouts, or exception markers.   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">View log details and use fields such as <code>sessionKey</code>, <code>agentId</code>, and <code>kind</code> to locate the original evidence, such as error stacks, command audits, configuration changes, and more.   </div>
