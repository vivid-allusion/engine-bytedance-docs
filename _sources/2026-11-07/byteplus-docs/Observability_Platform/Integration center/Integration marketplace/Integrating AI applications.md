---
title: "Integrating AI applications"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Integrating_AI_applications"
---

Integration center provides multiple AI application integration solutions, supporting one\-click generation of installation commands based on basic parameters. This simplifies AI application integration and enables rapid construction of an end\-to\-end trace observability system for AI applications. This topic uses Codex as an example to describe how to integrate AI applications into AI application monitoring.

<span id="NCv5HSiz"></span>
## Background

Currently supported AI applications for integration include: Codex, Claude, Cursor, OpenCode, OpenClaw, DeepSeek Harness, and Hermes.

<span id="MoYkLgfV"></span>
## Prerequisites

The AI application to be integrated has been deployed, for example, Codex. The specific deployment method is subject to the official instructions of each AI application.

<span id="l2uT4WJv"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select ** Integration Center \-\> Integration marketplace**.

3. Click **Codex** in the **AI application** category.

4. Configure integration parameters according to actual needs. The installation command will be generated automatically.

   
   |Parameter |Description |
   |---|---|
   |Region |Select the region to which the application belongs after being connected to AI application monitoring. |
   |workspace |Select the workspace to which the application belongs after being connected to AI application monitoring.<br><br>Workspaces are a data management and isolation method provided by Server\-side Monitoring. Each workspace has independent data reporting credentials and can centrally manage traces, logs, and metrics for different application ownership scenarios. |
   |Service name |Customize the display name of the application after being connected to AI application monitoring. |
   

5. Go to the AI application (for example, Codex client) and execute the automatically generated install command above to install the collection add\-on and complete the application integration.

   The following is an example of an add\-on installation for Codex. Select the appropriate method based on your actual scenario:

   
   <Tabs>
   <Tab zoneid="aXT8yuYTZ0" title="Automatic integration via conversation">
   <TabTitle>Automatic integration via conversation</TabTitle>
   
   You can send the `apmplus-codex-plugin` add\-on installation and configuration information to Codex via conversations directly. This enables an automatic installation and configuration process by Codex. For example:
   
   ```Bash
   Use the following command to install and configure apmplus-codex-plugin for me. The region is cn-beijing, the appkey is xxxxxxxxx, and the service name should be Codex.
   
   curl -fsSL "https://apmplus-codex-plugin.tos-cn-beijing.volces.com/install.sh" \
     | bash -s -- --non-interactive \
         --region cn-beijing \
         --appkey 742xxxxx48e225xxxxx40f565f1xxxxx \
         --service-name Codex
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="rJsUvXVfoB" title="Script-based integration">
   <TabTitle>Script-based integration</TabTitle>
   
   Install and configure the` apmplus-codex-plugin` add\-on directly via a script and automatic parameter passing. This method is applicable to non\-interactive modes, such as CI and automated environments.
   
   ```Bash
   curl -fsSL "https://apmplus-codex-plugin.tos-cn-beijing.volces.com/install.sh" \
     | bash -s -- --non-interactive \
         --region cn-beijing \
         --appkey 742xxxxx48e225xxxxx40f565f1xxxxx \
         --service-name Codex
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

6. After the installation is complete, manually restart Codex to ensure that the add\-on runs properly.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The restart command varies for different AI applications. Refer to the official instructions of the AI application for details.   </div>
   

<span id="EWdv7fO5"></span>
## Validate results

Go to the [AI app monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/ai_service/list), search for the AI application by name in the service list, and check the data reporting status. "**Normal**" indicates that data was reported successfully recently.

<span id="rZJK4QOm"></span>
## Other operations

To discontinue observability services for your AI application, go to the access configuration page of the target application to obtain the uninstall command. Then, execute the uninstall command in the AI application to uninstall the add\-on.
