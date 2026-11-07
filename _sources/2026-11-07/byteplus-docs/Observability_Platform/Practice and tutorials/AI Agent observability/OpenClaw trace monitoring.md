---
title: "OpenClaw trace monitoring"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/OpenClaw_trace_monitoring"
---

As a phenomenal open\-source AI Agent project, OpenClaw is rapidly becoming a "digital employee" capable of performing file operations, invoking system commands, and controlling browsers through powerful autonomous execution capabilities. However, while effective use can boost productivity, improper use can turn it into a "cost sinkhole". This topic describes how to integrate OpenClaw observability data with APMPlus, enabling your AI applications to transition from "uncontrolled costs" to "controlled costs".

<span id="MTy3xlD2"></span>
## Background

As the autonomy of OpenClaw increases, its internal behaviors become increasingly opaque. Seemingly normal mechanisms, such as heartbeat checks, context accumulation, and multi\-step reasoning, can quietly increase token consumption without the user's knowledge.

APMPlus focuses on solving the "black box" challenge of AI applications by providing end\-to\-end trace monitoring from code to model. APMPlus is the first in the industry to support receiving data reported by this plugin and provides out\-of\-the\-box monitoring dashboards to help users address the following issues:


* **Real\-time insight into token consumption**: Preset dashboards visually display token usage and cost trends, ensuring every expense is traceable.

* **Alert on abnormal behavior**: Customizable cost thresholds allow for immediate alerts when background tasks such as heartbeat checks trigger abnormal consumption.

* **Root cause analysis**: Token consumption is associated with specific traces and context sizes to quickly pinpoint the source of "cost black holes".


<span id="3HtSBMxV"></span>
## Prerequisites


* Open\-source OpenClaw ** v2026.4.24 ** or later has been deployed. For deployment guidance, see the[ official OpenClaw documentation](https://docs.openclaw.ai/install).

* You have obtained the configuration information required for OpenClaw integration. Details are as follows:

   
   |Parameter |Description |
   |---|---|
   |AppKey |The authentication information of Server\-side Monitoring. Although the App Key credential is independent of the integrated service type and data collection method, the App Key differs across workspaces. To obtain App Key, see [How to obtain the AppKey for Server-side Monitoring authentication?](https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication). |
   |Region |ID of the region for service integration, such as `cn-beijing`. For information about regions currently supported by Server\-side Monitoring, see [Available regions](https://docs.byteplus.com/en/docs/apmplus/server-launching_region). |
   |ServiceName |The service name, such as `openclaw`. The displayed service name in Server\-side Monitoring. You can customize the service name based on your needs. |
   


<span id="EcN6z7AF"></span>
## Procedure

<span id="SMpoM066"></span>
### Step 1: Integrate OpenClaw

This topic provides three OpenClaw integration methods. You can select an appropriate method based on the actual scenario.


<Tabs>
<Tab zoneid="NywOiL04qG" title="One-click integration via CLI">
<TabTitle>One-click integration via CLI</TabTitle>

Execute the following command to install the `apmplus-openclaw-plugin `plugin with one click, and follow the operation guide to complete the configuration.

```Shell
npx @volcengine/apmplus-openclaw-plugin-onboard-cli install
```





</Tab>
<Tab zoneid="oeVAfZBxch" title="Automatic integration via OpenClaw">
<TabTitle>Automatic integration via OpenClaw</TabTitle>

You can send the` apmplus-openclaw-plugin` plugin installation and configuration information to Hermes via conversations directly. This enables an automatic installation and configuration process by OpenClaw. For example:

```Plain Text
npx  @volcengine/apmplus-openclaw-plugin-onboard-cli install --non-interactive --region cn-beijing --appkey xxxxxxxxx --service-name openclaw --enable-streaming-usage
Run the above command to install and configure the apmplus-openclaw-plugin plugin for me. Set the region to cn-beijing, the appkey to xxx, and use openclaw as the service name.
```





</Tab>
<Tab zoneid="WXb7oAZnEW" title="Integration via native command">
<TabTitle>Integration via native command</TabTitle>

1. Execute the following OpenClaw native command to install the `apmplus-openclaw` plugin.


```Shell
openclaw plugins install @volcengine/apmplus-openclaw-plugin
```



2. Refer to the methods in Step 2 to configure the `apmplus-openclaw` plugin parameter in `~/.openclaw/openclaw.json`.


</Tab>
</Tabs>


<span id="Yly9dDb4"></span>
### Step 2: (Optional) Modify the configuration

If you need to modify the configuration after the `apmplus-openclaw-plugin` plugin is installed and configured, select an appropriate configuration update method as needed.


<Tabs>
<Tab zoneid="p4hd1rjTRX" title="Interactive quick configuration">
<TabTitle>Interactive quick configuration</TabTitle>

You can execute the following command for interactive quick configuration based on the configuration guide.

```Shell
npx @volcengine/apmplus-openclaw-plugin-onboard-cli config
```





</Tab>
<Tab zoneid="oh6xI2fXak" title="Configuration via console">
<TabTitle>Configuration via console</TabTitle>

Log in to the gateway webchat on port 18789, go to the **Settings \-\> Config \-\> All Settings** page, switch to Raw mode, and modify the configuration information.

Sample code is provided below:

```JSON
{
  // Do not modify any of the above configurations
  "plugins": {
    "allow": [
      // .....
      "any-other-plugin", // Do not delete any other plugins
      // .....
      "apmplus-openclaw-plugin", // Add apmplus-openclaw-plugin
    ],
    "entries": {
      "apmplus-openclaw-plugin": { // Add the configuration of the apmplus-openclaw-plugin plugin
        "enabled": true,
        "config": {
          "endpoint": "http://apmplus-cn-beijing.volces.com/server_collect/third_party/open_telemetry/v2/{your_app_key}",  // APMPlus reporting endpoint. Replace {your_app_key} with your appkey and cn-beijing with your Region ID.
          "serviceName": "your-service-name", // The custom service name
        }
      }
    }
  }
}
```





</Tab>
<Tab zoneid="zWurSbvqwG" title="Configuration via configuration file">
<TabTitle>Configuration via configuration file</TabTitle>

Edit the OpenClaw configuration file `~/.openclaw/openclaw.json` and modify the configuration in `plugins.allow` and `plugins.entries`. Sample code is provided below:

```JSON
{
  // Do not modify any of the above configurations
  "plugins": {
    "allow": [
      // .....
      "any-other-plugin", // Do not delete any other plugins
      // .....
      "apmplus-openclaw-plugin", // Add apmplus-openclaw-plugin
    ],
    "entries": {
      "apmplus-openclaw-plugin": { // Add the configuration of the apmplus-openclaw-plugin plugin
        "enabled": true,
        "config": {
          "endpoint": "http://apmplus-cn-beijing.volces.com/server_collect/third_party/open_telemetry/v2/{your_app_key}",  // APMPlus reporting endpoint. Replace {your_app_key} with your appkey and cn-beijing with your Region ID.
          "serviceName": "your-service-name", // The custom service name
        }
      }
    }
  }
}
```



</Tab>
</Tabs>


<span id="x06fzCy5"></span>
### Step 2: View observability data

Interact with OpenClaw via WebUI or other methods. After the conversation, navigate to the APMPlus console to view the observability data.


1. Navigate to [Service List](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/service/list) and search for the integrated OpenClaw by service name.

2. Click the service name to access the service details page. On the **Trace analysis** tab, view the list of trace spans corresponding to the OpenClaw service.

3. Click the target Trace ID and switch to the Property tab to view details of this request, such as the request model and token consumption.


<span id="nN46WOS0"></span>
## What to do next


* Navigate to [Preset dashboard](https://console.byteplus.com/observe/dashboard/dashboard/?type=builtin), select **OpenClaw observational disk**, and view the preset dashboard provided by APMPlus for OpenClaw.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the preset dashboards do not meet your monitoring needs, you can also create <a href="https://console.byteplus.com/observe/dashboard/dashboard?">custom dashboards</a> based on your actual requirements. For OpenTelemetry metrics exposed by OpenClaw, see <a href="https://docs.byteplus.com/en/docs/Observability_Platform/OpenClaw_metric_descriptions">OpenClaw metric descriptions</a>.   </div>
   

* Navigate to the [Alerting task](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/alarm/tasklist) page and click ** Create alerting task**. You can configure automated alert monitoring for OpenClaw observability metrics, such as token consumption and session lag, based on your needs. Configuring alert tasks helps monitor target service metrics for exceptions and ensures timely notifications, assisting you in keeping track of OpenClaw's operational status.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Alert tasks allow you to monitor corresponding metric values. An alert notification is automatically sent when the configured conditions are met. For detailed information about alert tasks, see <a href="https://docs.byteplus.com/en/docs/apmplus/Alert_tasks">Alert tasks</a>.   </div>
   

<span id="0ky0xzIV"></span>
## FAQ


* Q: After I have upgraded OpenClaw to v2026.4.24 or later, why are LLM spans missing from Trace statistics without reported token consumption data?

   A: The community v2026.4.24 version contains a breaking change. You must set `hooks.allowConversationAccess` to `true` to allow the plugin to use certain hooks. If you download manually via npm, execute the following command to configure:

   ```JSON
   openclaw config set plugins.entries.apmplus-openclaw-plugin.hooks.allowConversationAccess true
   ```
   

* Q: Why does an error occur when I download the plugin: `(429): Rate limit exceeded`?

   A: After version 323, the OpenClaw community requires all plugin installations to resolve Clawhub first before fallback to npm. For anonymous access, Clawhub rate\-limits every IP address. If the rate limit is triggered, first execute npx clawhub login to log in to clawhub as an individual user, and continue with the installation steps.

   ```JSON
   npx clawhub login
   ```
   

* Q: Why is the collected token count 0?

   A: In the community 3.7 version update, for custom provider models not natively supported by OpenClaw, the `compat.supportsUsageInStreaming` field is forcibly set to `false`. As a result, usage for such models cannot be collected correctly. To fix the issue, set `compat.supportsUsageInStreaming `to `true` and `diagnostics.enabled` to` true `in the provider model.

* Q: How do I configure the plugin if I do not want to collect sensitive information, such as inputs and outputs?

   A: In the configuration, set allowUserDetailInfoReport to false. You can use the following configuration as a reference:

   ```JSON
   
   {
     // Do not modify any of the above configurations
     "plugins": {
       "allow": [
         // .....
         "any-other-plugin", // Do not delete any other plugins
         // .....
         "apmplus-openclaw-plugin", // Add apmplus-openclaw-plugin
       ],
       "entries": {
         "apmplus-openclaw-plugin": { // Add the configuration of the apmplus-openclaw-plugin plugin
           "enabled": true,
           "config": {
             "endpoint": "http://apmplus-cn-beijing.volces.com/server_collect/third_party/open_telemetry/v2/{your_app_key}",  // APMPlus reporting endpoint. Replace {your_app_key} with your appkey and cn-beijing with your Region ID.
             "serviceName": "your-service-name", // The custom service name
             "allowUserDetailInfoReport": false // Collection of sensitive request information is not allowed
           }
         }
       }
     }
   }
   ```
