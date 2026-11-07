---
title: "AI application observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/AI_application_observability"
---

ServingKit supports custom configuration of AI application observability dashboards through cloud\-native basic observability and deep observability capabilities. Basic observability provides the monitoring metrics for AI resources and inference services. Deep observability provides an end\-to\-end performance monitoring service for inference applications.

This topic uses an SGLang\-based AI application as an example to demonstrate how to create your own AI application observability dashboard.

<span id="pPZjd3PA"></span>
## Basic observability


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the cluster list, find the heterogeneous computing cluster in which the AI application was deployed, and click the cluster name.

3. In the left navigation pane of the cluster management page, click **Cloud native observability** \> **Overview**. On the page that appears, click **Enable basic observability** to enable cloud\-native observability and VKE observability. For more configuration details, refer to [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

4. After turning on observability, the application metrics of SGLang will be collected into the Vital Managed Service for Prometheus (VMP). You can use Explore to query metrics in the VMP console. An example is as follows:

   * There is a built\-in VMP dashboard that allows you to view the metrics collected from SGLang\-based applications. To do that, you can go to the [VMP console](https://console.byteplus.com/prometheus), select **Monitoring dashboard** in the left navigation bar and search for `SGlang` to open dashboard as shown below:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee08ac4b96e555506273b350e2c3a30e.png) </span>

   * You can also use self\-built Grafana and set up an SGLang monitoring dashboard. For more details, see [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

      1. Log in to the above Grafana and select Import the JSON file of the following dashboard:

         <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8a819899c3bab3f2b507a0d738b02aa.json" name="SGLang Dashboard-1747206543364.json">SGLang Dashboard-1747206543364.json</Attachment>
         

      2. The effect after importing is shown in the figure:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7817f01eac7e278f43ffc08f3dcd5da4.png) </span>

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a40d0b078d252304401d12dc08fd843.png) </span>


<span id="quLysUgM"></span>
## Deep observability


1. Log in to the [APMPlus console](https://console.byteplus.com/apmplus-server/region:apmplus-server+cn-beijing/console/overview/server?monitorType=server). In the left navigation pane, click **Server\-side Monitoring**.

2. Search for `SGlang` and click the service name in the results to open the monitoring dashboard page.

3. View metrics.

   * LLM metrics

      On tabs such as **Service Overview**, **LLM performance**, and **Token usage**, you can view large model core metrics and key service metrics, such as the number of large model calls, the token usage, response latency, time to first token (TTFT), time per output token (TPOT)​​, queries per second (QPS), and request error rate.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">TTFT and TPOT are effective only when LLMs are called with streaming\-enabled requests.      </div>
      

      The example of a streaming call is as follows:

      ```bash
      curl localhost:8080/v1/chat/completions -H "Content-Type: application/json"   -d '{
              "model": "/data/models/DeepSeek-R1",
              "messages": [
                  {
                      "role": "user",
                      "content": "hello"
                  }
              ],
              "stream": true,
              "stream_options": {
                  "include_usage": true,
                  "continuous_usage_stats": true
              }
          }'
      ```
      

   * Runtime metrics

      On the **Runtime monitoring** tab, you can view runtime\-related metrics, including CPU time, CPU usage, Memory usage, Number of GC objects, Number of threads, and Number of context switches.

4. View trace analysis.

   On the Trace analysis tab, you can search for trace information based on different conditions. Click the ID of the target trace to go to the details page of the trace. View trace information in the list.
