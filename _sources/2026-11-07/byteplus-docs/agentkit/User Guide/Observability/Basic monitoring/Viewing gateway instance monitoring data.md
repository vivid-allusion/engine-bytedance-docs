---
title: "Viewing gateway instance monitoring data"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_gateway_instance_monitoring_data"
---

You can view gateway instance monitoring data to understand the health of your gateway instance and quickly identify abnormal requests and performance bottlenecks. The monitoring data supports troubleshooting and business optimization.

<span id="pFLzq8vW"></span>
## Prerequisites

You have enabled the log service for the gateway instance. For details, see [Enabling logs](https://docs.byteplus.com/en/docs/agentkit/Enabling_logs?lang=en).

<span id="ZOiMsAzU"></span>
## Notes

You can view monitoring data only when the target gateway instance is in the **Running** state. Query\-related limits are as follows:


* **Time range for a single query**: from the ** last 15 minutes** to **1 ** year.

* **Data storage period: ** By default, you can query monitoring data within the past ** 90 ** days. You can **adjust the storage period** as needed. For details, see[ Modify the log storage period](https://docs.byteplus.com/en/docs/tls/Managing_topics#.5L-u5pS55pel5b-X5a2Y5YKo5pe26Ze0). Data beyond the storage period cannot be queried.


<span id="VP0w2Kh5"></span>
## Procedure


1. Log in to the[ AgentKit console](https://console.byteplus.com/agentkit). 

2. In the top menu bar, select the project and region of the target model service.

3. In the left\-side navigation pane, select "**Gateway \> Gateway instance**".

4. On the gateway instance list page, click the name of the target instance, and click the "Monitoring" tab to view the monitoring metric data of the gateway instance.

   * **Time filtering range**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">A custom time range<strong> takes effect only for the current page session</strong>. If you leave the page and open it again, the time range is automatically reset to the default value: Last 15 minutes.      </div>
      

      By default, the monitoring data of the last 15 minutes is displayed. To view data in another time range, you can specify a custom time range as follows:

      1. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b34a4537a3f6496aaa20c6ed6863867.png) </span> to open the time filter pane.

      2. Select a time filter mode as needed. Three modes are supported: Relative time, Absolute time, and Historical record.

         * **Relative time: ** Quickly select a preset time range, such as "Last 1 hour". This mode is suitable for real\-time troubleshooting, routine inspection, and quick observation of recent operational changes.

            <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="default" data-wrapper-indent="4">If you select "Relative time" and switch on "On the hour", the time range is automatically aligned to the hour. This helps you perform periodic comparison analysis.            </div>
            

         * **Absolute time: ** Specify a start time and end time (accurate to the second). This mode is suitable for precise backtracking and review when you know exactly when a fault occurred.

         * **Historical record: ** View and reuse time ranges that you have queried before. This mode is suitable for scenarios in which you frequently switch to the same time range, which reduces repeated configuration.

      3. In the selected mode, select the required time range, for example, "Relative time  **\>**  Last 7 days". Then, the monitoring data for the selected time range is reloaded on the page.

   * **Auto refresh**

      Auto refresh is disabled by default. To monitor metric changes in real time, click "**Auto refresh off**", click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f1ab09fcaaff419fca141d643dbfbf05.png) </span> , and then select a refresh frequency to enable auto refresh.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Auto refresh <strong>takes effect only for the current page session</strong>. If you leave the page and open it again, auto refresh is <strong>disabled again</strong>.      </div>
      

   * **Currently supported metrics**

      
      |Metric name |Unit |Description |
      |---|---|---|
      |QPS |Count/s |**The number of service requests** that a gateway instance processes per second within the current collection period (for example, 15 minutes). This metric reflects the instantaneous request load of the gateway. |
      |Number of requests |Count |**The total number of service requests** (both successful and failed requests) that a gateway instance receives within the current collection period (for example, 15 minutes), including both successful and failed calls. |
      |Response time |ms |The ** average time ** that a gateway instance takes to process service requests within the current collection period (for example, 15 minutes). The duration is measured from when a request is received to when the response is returned. |
      |Total inbound/outbound bandwidth |bit/s |The total traffic that a gateway instance **receives ** from clients (callers) per second (**inbound**) and the total traffic that the gateway instance ** returns to ** clients per second (**outbound**) within the current collection period (for example, 15 minutes). Both inbound and outbound traffic include public network traffic and private network traffic. |
      |Inbound/outbound public network bandwidth |bit/s |The traffic per second that a gateway instance receives from clients (callers) **over the public network ** (**inbound**) and the traffic per second that the gateway instance returns to clients **over the public network** (**outbound**) within the current collection period (for example, 15 minutes). |
