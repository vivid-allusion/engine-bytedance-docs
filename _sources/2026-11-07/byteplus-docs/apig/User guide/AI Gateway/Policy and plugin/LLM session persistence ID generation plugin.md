---
title: "LLM session persistence ID generation plugin"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/LLM_session_persistence_ID_generation_plugin"
---

The plugin for generating LLM session persistence IDs creates a session persistence ID based on the Prompt in the request and achieves session persistence by applying a consistent Hash policy. This article describes how to create a plugin for generating session persistence IDs for LLMs.

<span id="g1rN66iJ"></span>
## Background information

The LLM session persistence ID generation plugin is designed to achieve session persistence in large model sessions by routing requests with the same Prompt Message segment to the same inference engine instance, reusing session cache information, reducing session creation time, and enhancing the user experience.

<span id="uFC5V59s"></span>
## Prerequisites


* The APIG instance has been created. For details, refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* A service has been created. For details, see [Creating services](https://docs.byteplus.com/en/docs/apig/Creating_a_service#.5Yib5bu65pyN5Yqh).

* Routes have been created. For details, refer to [add route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

* An Upstream has been created, and the consistent hashing load balancing algorithm is used based on the header. The header used for load balancing is X\-Digest\-Session\-ID. For details about actions, refer to [Upstream Management](https://docs.byteplus.com/en/docs/apig/Upstream_Management).


<span id="yrikOtDJ"></span>
## Limit


* Within the same route, the LLM session persistence ID generation plugin is mutually exclusive with the LLM load\-aware routing plugin, the LLM session affinity routing plugin, and the MCP session persistence plugin.

* The same plugin can only be bound once on the same resource.


<span id="BQ1HofjC"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. Select the target instance in **Instance Management**.

3. In the left navigation bar, click **Plugin Center **  \> **LLM Session persistence ID generation plugin** \> **Create plugin**.

4. Configure plugin rules.

   
   |Parameter |Description |
   |---|---|
   |Service |Select the service for the plugin. |
   |Associated route |Select the route of the Plugin. |
   |Generation method |The system currently only supports **generation based on Prompt content**. |
   |Generate source |Select one or more segments of content in the session to generate a Session ID. Click **View example**. View the naming convention for Content in Message. |
   

4. Click **Confirm**.


<span id="g0qsWUAb"></span>
##
