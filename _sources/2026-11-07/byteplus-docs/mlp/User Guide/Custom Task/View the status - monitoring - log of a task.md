---
title: "View the status/monitoring/log of a task"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/View_the_status-monitoring-log_of_a_task"
---

Machine Learning Platform supports viewing the status of tasks and instances, running logs, monitoring data, and other information. Through this information, users can obtain the progress and health status of the current training task. In addition, users can also enter the training container through WebShell for troubleshooting.

<span id="使用前提"></span>
# premise of use


1. [Custom Training] There is \> = 1 training task.


<span id="操作步骤"></span>
# Procedure


1. Log in to the Machine Learning Platform and click [Model Training] \- [Custom Training] in the left navigation bar to enter the list page. The status and running time on the list page briefly describe the overall situation of the task.

2. Click on the task name to enter the details page to view the status of all **instances** . The status of all training instances jointly affects the status of the **task** . Click Timeline to view some important time nodes for the task. In order to make it easier for users to understand, the following information is specifically explained:

   
   |Parameter |Parameter Description |
   |---|---|
   |instance state |Queuing: In this state, the instance is waiting for quota and node scheduling.<br><br>Deployment: image pulling, storage mount, container creation, etc.<br><br>Running: Execute the training code.<br><br>Stopping: The user triggers a cancel operation or the task has exceeded its maximum running time and is deleting the instance.<br><br>Exception: Instance encountered a system error while queuing, deploying, and stopping.<br><br><br>* Completed: Execution completed.<br><br>   Failure: Failed to run or abnormal timeout.<br><br>* Deleted: The instance has been deleted.<br><br>* Finished (on hold): The `instance retention duration`is configured and the instance `completes`.<br><br>* Failed (on hold): The `instance retention duration`is configured and the instance `fails`to run. |
   |task status |Creating: After submitting a request created by a task, wait for the request to return.<br><br><br>* Queuing: All instances are `queued`.<br><br>* Deployed: All instances have completed queuing, and the state of the instances is `in deployment`or includes part `of the running`state.<br><br>* Running: All instances are deployed and the instance status is `running`.<br><br>   Stopping: The user triggers a cancel operation or the task has exceeded its maximum running time and is deleting the instance.<br><br>* Exception: There are \> = 1 instances with `abnormal`status at this stage.<br><br>* Completed: All instances are completed.<br><br>* Failure: There are \> = 1 instances with the status of `failure`.<br><br>* Stopped: The task is cancelled manually, timed out, and preempted, so that all uncompleted instances finally reach the state of `being deleted`.<br><br>* Failure (on hold): There are \> = 1 instances with the status `Failure (on hold)`.<br><br>* Done (on hold): All instances have the status `Done (on hold)`. |
   |Timeline |Show the important time nodes of task execution, such as creation completion, start queuing, start running, etc. |
   


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c80d6c551894cb68a9c5ec39acd4a94~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31904ffd8aae4e51bdb1acfa736c85c8~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1c10e2639804448a3b5473640a40262~tplv-goo7wpa0wc-image.image) </span>


3. Click [Monitoring] of an instance in the operation area to jump to the monitoring page of the instance to view more detailed monitoring metrics. The specific supported monitoring metrics are as follows.

   * CPU: Utilization, usage.

   * Memory: utilization, usage.

   * Network: the rate of inflow, the rate of outflow.

   * GPU: Utilization, Memory Utilization, Memory Usage. When an instance contains multiple GPUs, multiple curves are summarized on the graph.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77faacf66ec748979a1e3141db968d18~tplv-goo7wpa0wc-image.image) </span>


4. Click on the [log] of an instance in the operation area to jump to the log page of the instance to view more detailed running logs. [real\-time log] is available by default, and [history log] needs to be opened by the user.

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

5. When the instance state is `running`, click [WebShell] in the operation area to enter the instance container to manually execute commands or troubleshoot problems.
