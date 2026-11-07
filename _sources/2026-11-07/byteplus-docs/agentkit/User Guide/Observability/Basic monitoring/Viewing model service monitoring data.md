---
title: "Viewing model service monitoring data"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_model_service_monitoring_data"
---

You can view model service monitoring data to understand the request performance, errors, and resource consumption of the service. This helps you troubleshoot issues and optimize your business.

<span id="kni6x0hz"></span>
## Prerequisites

You have enabled the log service for the gateway instance. For more information, see [Enabling logs](https://docs.byteplus.com/en/docs/agentkit/Enabling_logs?lang=en).

<span id="vaendMX6"></span>
## Notes

You can view the monitoring data of a gateway instance only when the instance is in the **Available** state. Query\-related limits are as follows:


* **Time range for a single query**: from ** the last 15 minutes** to **1 ** year.

* **Data storage period:**  By default, you can query monitoring data within the past **90 ** days. You can **adjust the storage period ** as needed. For details, see [Modify the log storage period.](https://docs.byteplus.com/en/docs/tls/Managing_topics#.5L-u5pS55pel5b-X5a2Y5YKo5pe26Ze0) Data beyond the storage period cannot be queried.


<span id="4wETluYR"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the top menu bar, select the project and region of the target model service.

3. In the left\-side navigation pane, select "**Gateway \> Model service**".

4. On the Model service page, click the "Monitoring" tab to view the monitoring metric data of the model service.

   * **Filter data by Proxy API Key or Provider**

      You can filter monitoring data by ** Proxy API Key (gateway proxy key) ** and ** Provider (model provider)** . Select a filter target from the corresponding drop\-down list. The two filter conditions can be used in combination. After you modify the filter conditions, all monitoring metrics on the page are reloaded and displayed based on the new conditions.

   * **Filter data by time range**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">A custom time range<strong> takes effect only for the current page session</strong>. If you leave the page and open it again, the time range is automatically reset to the default value: Last 15 minutes.      </div>
      

      By default, the monitoring data of the last 15 minutes is displayed. To view data in another time range, you can specify a custom time range as follows:

      1. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b34a4537a3f6496aaa20c6ed6863867.png) </span> to open the time filter pane.

      2. Select a time filter mode as needed. Three modes are supported: Relative time, Absolute time, and Historical record.

         * **Relative time: ** Quickly select a preset time range, such as "Last 1 hour". This mode is suitable for real\-time troubleshooting, routine inspection, and quick observation of recent operational changes.

            <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="default" data-wrapper-indent="4">If you select "Relative time" and switch on "On the hour", the time range is automatically aligned to the hour. This helps you perform periodic comparison analysis.            </div>
            

         * **Absolute time:**  Specify a start time and end time (accurate to the second). This mode is suitable for precise backtracking and review when you know exactly when a fault occurred.

         * **Historical record:**  View and reuse time ranges that you have queried before. This mode is suitable for scenarios in which you frequently switch to the same time range, which reduces repeated configuration.

      3. In the selected mode, select the required time range, for example, "Relative time  **\> ** Last 7 days". Then, the monitoring data for the selected time range is reloaded on the page.

   * **Auto refresh**

      Auto refresh is disabled by default. To monitor metric changes in real time, click "**Auto refresh off**", click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f1ab09fcaaff419fca141d643dbfbf05.png) </span> , and then select a refresh frequency to enable auto refresh.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Auto refresh<strong> takes effect only for the current page session</strong>. If you leave the page and open it again, auto refresh<strong> is disabled again</strong>.      </div>
      

   * **Currently supported metrics**

      
      |Metric name |Unit |Description |
      |---|---|---|
      |Input tokens |Token |The total number of tokens consumed by the ** input content (Prompt)**  received by the model service in the current collection period (for example, 15 minutes). |
      |Cached tokens |Token |The total number of tokens that hit the ** prompt cache ** in the model service in the current collection period (for example, 15 minutes). You can use this metric to evaluate cache hit efficiency and identify billing optimization opportunities. |
      |Output tokens |Token |The total number of tokens consumed by the **output content (Completion)**  generated by the model service in the current collection period (for example, 15 minutes). |
      |Cache hit ratio |% |**The ratio of cached tokens to input tokens for the model service ** in the current collection period (for example, 15 minutes). You can use this metric to measure the reuse efficiency of prompt caching. |
      |Tokens by provider |Token |The token consumption aggregated by ** model provider** (such as ModelArk) in the current collection period (for example, 15 minutes). You can use this metric to analyze the proportion of calls and the cost distribution of different providers. |
      |Tokens by model |Token |The token consumption aggregated by ** model** in the current collection period (for example, 15 minutes). You can use this metric to analyze the proportion of calls and the cost distribution of different models. |
      |Tokens by Proxy API Key |Token |The token consumption aggregated by **Proxy API Key** (gateway proxy key) in the current collection period (for example, 15 minutes). You can use this metric to analyze the usage and cost allocation of different callers or business lines. |
      |Input tokens/min |Token/min |**The average number of input tokens per minute** (TPM, Tokens Per Minute\-Input) for the model service in the current collection period (for example, 15 minutes). You can use this metric to measure the request load on the input side and use it as a throttling reference. |
      |Output tokens/min |Token/min |**The average number of output tokens per minute ** (TPM, Tokens Per Minute\-Output) for the model service in the current collection period (for example, 15 minutes). You can use this metric to measure the generation load on the output side and use it as a throttling reference. |
      |TTFT |ms |TTFT (Time To First Token) is the duration from when the model service receives a request to **when the first token is returned**. You can use this metric to measure the ** first token latency** of models. **A smaller value indicates a faster first\-token response.**  |
      |TPOT |ms/token |TPOT (Time Per Output Token) is the ** average time that the model takes to generate each output token** in the generation phase. You can use this metric to measure the **streaming generation speed ** of models. ** A smaller value indicates faster generation**. |
