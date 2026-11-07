---
title: "MaaS high-code trace monitoring"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/MaaS_high-code_link_monitoring"
---

Server\-side Monitoring now supports Arkitect, the open\-source architecture of ModelArk. For application functions built on Arkitect, Server\-side Monitoring can automatically generate LLM\-related traces and metrics, thereby enabling trace monitoring for agents. This topic provides a detailed walkthrough of the entire workflow for using MaaS high\-code trace monitoring, covering everything from agent creation to trace/metric monitoring.

<span id="TH2LltnY"></span>
## Background

APM is deeply integrated with veFaaS. For functions deployed on veFaaS, simply enabling APM allows for the automatic ingestion of function monitoring data. In this case, APM can automatically collect trace information, generate metrics, and retrieve call chains and logs.

The MaaS high\-code agent is essentially a Python function deployed on veFaas. APM already supports Arkitect, the open\-source architecture of ModelArk. Therefore, function monitoring data can be automatically ingested to APM for automatic generation of LLM\-related traces and metrics.

<span id="cWPLXVH5"></span>
## Prerequisites


* You have activated ModelArk and related high\-code services, such as veFaaS.

* APM has been activated. For detailed steps, refer to [Activating APM](https://docs.byteplus.com/en/docs/apmplus/Activate_server-side_monitoring).


<span id="sYkNG4B3"></span>
## Procedure

<span id="tgbWVoiS"></span>
### Step 1: Deploy a high\-code application


1. Log in to the [ModelArk console](https://console.byteplus.com/ark) and select **Agent builder \> My apps** in the left navigation bar.

2. On the application management page, click **Create app**, and select **High\-code** to create the application.

3. Configure the application information based on your actual scenario, including the custom application name, IAM role, and application function. In this scenario, the **function creation** method is used to add an application function. After the function is added, release the application. 

4. In the application function configuration section, click **Create new function** to go to the function creation page. Configure the information as needed, such as the function name and IAM role. After you configure the information, click **Create**. The veFaaS application is automatically deployed, and the veFaaS function is created.


<span id="aXVaQInw"></span>
### Step 2: Enable AI application monitoring


1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas) and select **Function** in the left navigation bar. The function management page is displayed.

2. Locate the function created in Step 1 by its name. After the target function is located, click the function name to go to the function details page.

3. On the **Function configuration** tab, click "Edit" next to **Application Monitoring**, enable application monitoring, and save and publish the application monitoring configuration information. After the application monitoring service is enabled, the monitoring data of the function will be delivered to APM. This enables integrated monitoring of metrics, traces, and logs and display of the monitoring dashboard. In addition, agent\-based monitoring is supported for ModelArk high\-code applications and LangChain frameworks.


<span id="xKOAyZNx"></span>
### Step 3: Initiate an agent conversation


1. Return to the [ModelArk console](https://console.byteplus.com/ark) and select **Agent builder \> My apps** in the left navigation bar.

2. Find the AI application created in Step 1 and click **Try now ** to go to the agent interaction page.

3. Enter your question and send it, and the agent will return a corresponding response. The metrics, traces, logs, and other monitoring information generated during this process will be delivered to APM.


<span id="bnYGy4Fb"></span>
### Step 4: View AI application trace monitoring


<Tabs>
<Tab zoneid="I9KI3JWsMn" title="View trace monitoring in the Function Service Console">
<TabTitle>View trace monitoring in the Function Service Console</TabTitle>

1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas) and select **Function** in the left navigation bar. The function management page is displayed.

2. Locate the function created in Step 1 by its name. Once the target function is filtered out, click the function name to access the function details page.

3. On the **Application monitoring** tab, switch to **AI Application Trace Analysis**, and filter the traces related to the conversation in Step 3 by using Span attributes. In this scenario, the trace information of the current request is filtered by the conversation input information `apmplus.entity.input`.

4. On the **Trace analysis** tab, you can view the filtered traces. Hover over the **Input/output** button to automatically display details of the agent input and output information.

5. Click the trace ID to view the complete trace and topology map of the entire request chain. Three display modes are supported: flame graph, list view, and topology map.

6. Click **LLM** on the right\-side **Metric** tab to view the trend chart of LLM metrics associated with the current trace. Examples of such metrics include token usage, large model response latency, TPOT, and TTFT.

7. In the flame graph, select the `ark_runtime.chat` Span. You can view the input and output details of the current conversation on the "Attributes" tab of the right\-side "Details" tab. Scroll down further to check more agent\-related data in the "Tags" section, such as token usage, TPOT, and TTFT.

8. In the flame graph, select the Span with alerts. The "Events" tab of the right\-side "Details" tab displays the error stack trace and event list, facilitating trace tracking and fault localization.

9. Return to the **Application monitoring** tab. On the **Runtime monitoring** tab, you can view agent runtime monitoring information, including CPU duration, CPU usage, memory usage, number of GC objects, number of threads, and number of context switches.


</Tab>
<Tab zoneid="umQ8019wUG" title="View trace monitoring in the Server-side Monitoring console">
<TabTitle>View trace monitoring in the Server-side Monitoring console</TabTitle>

1. Log in to the [APM console](https://console.byteplus.com/observe/apmplus-server), and select the project and region in the top navigation bar.

2. In the left navigation bar, select **Service Monitoring \> Service List** to go to the service list page.

3. Perform a fuzzy search for the target service using the function name created in Step 1. After the service corresponding to the function is located, click the service name to navigate to the service details page.

4. Switch to **AI Application Trace Analysis**, and filter the traces related to the conversation in Step 3 by using Span attributes. In this scenario, the trace information of the current request is filtered by the conversation input information `apmplus.entity.input`.

5. On the **Trace analysis** tab, you can view the filtered traces. Hover over the **Input/output** button to automatically display details of the agent input and output information.

6. Click the trace ID to view the complete trace and topology map of the entire request chain. Three display modes are supported: flame graph, list view, and topology map.

7. Click **LLM** on the right\-side **Metric** tab to view the trend chart of LLM metrics associated with the current trace. Examples of such metrics include token usage, large model response latency, TPOT, and TTFT.

8. In the flame graph, select the `rutime.chat` Span. You can view the input and output details of the current conversation on the "Attributes" tab of the right\-side "Details" tab. Scroll down further to check more agent\-related data in the "Tags" section, such as token usage, TPOT, and TTFT.

9. In the flame graph, select the Span with alerts. The "Events" tab of the right\-side "Details" tab displays the error stack trace and event list, facilitating trace tracking and fault localization.

10. Go to the **Runtime monitoring** tab, you can view agent runtime monitoring information. The information includes CPU duration, CPU usage, memory usage, number of GC objects, number of threads, number of context switches, and more.


</Tab>
</Tabs>
