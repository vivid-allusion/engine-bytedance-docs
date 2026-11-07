---
title: "Updating runtime instance count"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_runtime_instance_count"
---

Setting an appropriate instance count range helps you balance service capacity against resource costs: if the upper limit of the range is too low, scale\-out is restricted during peak hours, and sessions are rejected by throttling. If the upper limit of the range is too high, resources may remain idle and be wasted. This topic describes how to adjust the ** instance count range** of an AgentKit agent runtime.

<span id="0pmk4OZi"></span>
## Typical scenarios


|**Scenarios** |**Typical signals** |**Recommendation** |
|---|---|---|
|Increase the maximum number of instances |* The number of instances reaches the maximum value during peak hours.<br><br>* Sessions are rejected by throttling.<br><br>* The load on a single instance approaches the threshold, but the instance still cannot handle more requests. |Increase the maximum number of instances to allow more room for automatic scale\-out and support more concurrent sessions. |
|Decrease the maximum number of instances |* Service traffic remains low for a long time.<br><br>* The number of instances stays below the maximum value for a long time.<br><br>* Downstream dependencies have an overall concurrency limit. |Decrease the maximum number of instances to reduce resource waste and protect downstream services from being overwhelmed. |
|Adjust the minimum number of instances |* Cold start duration affects your services.<br><br>* The scale\-out speed cannot keep up with traffic growth during peak hours, or you want to release resources during off\-peak hours to reduce costs. |If your services are latency\-sensitive, increase the minimum number of instances to ensure always\-on compute capacity. If your services are cost\-sensitive, decrease the minimum number of instances. We recommend that you keep the minimum number of instances at 2. |


<span id="ovWfg9Od"></span>
## Usage notes


* For an agent runtime that has preview mode enabled, you can set an independent instance count range (that is, the minimum number of instances and the maximum number of instances) for the **Latest version** and for the **current online version** separately. The two ranges take effect independently and do not affect each other.

* For an agent runtime that does not have preview mode enabled, you can set an instance count range (that is, a minimum number of instances and a maximum number of instances) only for ** the current online version**.


<span id="qQgDKXoO"></span>
## Prerequisites

You have [created an agent runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

<span id="OJDbx5NI"></span>
## Procedure


1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. Click the "Resource management" tab. Then, for the instance count range that you want to modify, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b281eee9abde27dd1ee5cd367007a8e.png) </span>****.

   * **Instance count range (Latest)** : The instance count range used by the Latest Version, typically for preview or testing. You specify a smaller range to save resources.

   * **Instance count range (V0 / V1 / …)** : The instance count range used by the current online version. The version number changes automatically as versions iterate. The online version handles production traffic. You can specify a wider range to handle traffic peaks.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The instance count range (Latest) card is displayed and you can modify it only after preview mode is enabled for the agent runtime. If preview mode is not enabled, the card is not displayed.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In preview mode, changes to the minimum and maximum instance counts on the <strong>Configuration information</strong> page apply only to the <strong>Latest version</strong>.   </div>
   

5. In the dialog box, enter the new minimum and maximum instance counts. Set the minimum to **at least 2** and ** no greater than the maximum**.

6. Click "Confirm". The new configuration takes effect immediately.

   If the new configuration does not meet your expectations, you can edit the instance count range again without rolling back the version.
