---
title: "View the status/monitoring/logs of the service (new)"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/View_the_status_monitoring_logs_of_the_service_new"
---

The Machine Learning Platform supports viewing the status of services and instances, and provides detailed monitoring and logging, as well as WebShell, to help users understand the health of services throughout their lifecycle, from creation to deletion.

<span id="使用前提"></span>
# premise of use


1. There are \> = 1 services in [inference services].


<span id="状态"></span>
## Status


1. Log in to the Machine Learning Platform and click [Model Services] \- [Inference Services] in the left navigation bar to enter the list page. The service status and number of instances in the list page represent the overall health of the **service** .

2. On the list page, click a service name to enter the details page, and click [Deployment] to further view the status of all deployments and instances of the current service. The status of all instances jointly affects the **deployment** and the status of the **service** . For ease of understanding, the following information is specifically noted:



|Parameter |Parameter Description |
|---|---|
|instance state |* Deployment: Node scheduling, mirror pull, start instance phase.<br><br>* In operation: At this stage, the instance can provide services to the outside world normally.<br><br>* Stopping: The user triggers an action to delete the service and is in the process of deleting the instance.<br><br>* Exception: All instance deployments timed out or an error occurred during execution. |
|deployment status |* Not running: After the deployment is stopped, all deployment instances are emptied.<br><br>* Deployed: All instances are in the deployment phase, and the instance state is `in deployment`.<br><br>* Running: There are \> = 1 instances `running in`this phase.<br><br>* Stopping: The user triggers to stop the deployment and is in the process of deleting the instance.<br><br>* Exception: All instances are `abnormal`. At this point, you need to enter the details page to view the instance status and log to locate the problem. |
|service status |* Not running: After the service is stopped, all service instances are emptied.<br><br>* Deployed: All instances are in the deployment phase, and the instance state is `in deployment`.<br><br>* Running: There are \> = 1 instances `running in`this phase.<br><br>* Stopping: The user triggers an action to stop the service and is in the process of deleting the instance.<br><br>* Exception: All instances are `abnormal`. At this point, you need to enter the details page to view the instance status and log to locate the problem. |
|number of instances |* Number of instances available/expected.<br><br>* A service contains several instances, and the number of instances available reflects the health of the service to some extent. |


<span id="监控"></span>
## Monitoring


1. Click [Monitoring] to jump to the monitoring page of the service/deployment/instance to view more detailed monitoring metrics, including **business metrics** and **resource operation metrics** .

2. Viewing **business metrics** is supported only when using the API gateway, with a capture interval of 1 minute. On the page, you can view the relevant indicator monitoring data for 7 layers. Detailed monitoring metrics can be found in the [API gateway monitoring metrics description](https://docs.byteplus.com/en/docs/apig/Monitoring_metrics)

3. **Resource operation indicators** are supported as follows:

   * CPU: Utilization, usage.

   * Memory: utilization, usage.

   * Network interface card: inflow rate, outflow rate.

   * GPU: Utilization, Memory Utilization, Memory Usage. When an instance contains multiple GPUs, multiple curves are summarized on the graph.


<span id="日志"></span>
## log


1. Click on the [log] of an instance in the operation area to jump to the log page of the instance to view more detailed running logs. [real\-time log] is available by default, and [history log] needs to be opened by the user.

   1. real\-time log

      1. Support for searching keywords in the full text. Such as retrieving all log entries containing `error`strings.

         * Key words are case\-insensitive and can be retrieved. If you search for "Error", "error", "ERROR", you will find the following content.

            ```Plain
            Error
            error
            ERROR
            erroR
            ... error ...
            ```
            

         * When multiple words are separated by spaces or special characters, the spaces or special characters are ignored. If you search for "worker 5" or "worker\-5", you will find the following content.

            ```Plain
            worker-5
            worker_5
            worker 5
            worker^5
            ... worker 5 ...
            ```
            

      2. Supports viewing logs with a size limit of < 500MB or < 5000 entries. The more logs viewed, the longer the wait time may be. Use the volc ml_task logs directive to view the full log, as detailed in the [command line tool usage documentation ](https://docs.byteplus.com/en/docs/mlp/Use_documents).

      3. Support the automatic update of logs. After opening, the platform will regularly update the training logs, and support users to select the number of logs for each update.

   2. history log

      1. Supports filtering out eligible logs by search criteria, see [search syntax ](https://docs.byteplus.com/en/docs/tls/Query-overview-2).

         * Full text query: `error`

         * Key value query: `Latency: > 5000`

         * Phrase query: `"http error"`

      2. Support for statistical analysis via SQL statements, see [Analysis Overview ](https://docs.byteplus.com/en/docs/tls/Analysis-overview).

         * Count visits in requests with status code 200: `status: 200 | SELECT COUNT (*) AS PV`

      3. Support full download of historical logs and save them as timed SQL analysis.

      4. Support to view and retrieve log data in two ways: [raw log] and [chart analysis].

         Results retrieved in the aforementioned manner are presented in either raw or tabular formats, allowing for a variety of personalizations such as line wrapping, compact layout, filtering of empty fields, tiling of JSON\-like fields, and the use of page flippers.

         * For [Original Log], select fields to show or hide. Support single page log number settings (10/20/30/40/50).

         * For [Chart Analysis], support the use of a variety of charts to visualize data analysis, such as line charts, bar charts, etc. For each chart, please refer to the [Statistical Chart Overview ](https://docs.byteplus.com/en/docs/tls/chart_overview). For chart effect details, support universal configuration, field configuration and interactive events three personalized settings.
