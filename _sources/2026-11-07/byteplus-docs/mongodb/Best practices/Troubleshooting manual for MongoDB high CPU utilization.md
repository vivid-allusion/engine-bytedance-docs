---
title: "Troubleshooting manual for MongoDB high CPU utilization"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/troubleshooting-for-high-cpu-utilization"
---

If the query statements are not optimal enough (for example, indexes are not properly set), the number of concurrent requests is large, or the computing workload is heavy during the use of the MongoDB database, the CPU usage of the MongoDB database may become high. This will lead to problems such as slow data read/write and more timeouts, severely affecting normal service operations. This topic describes how to troubleshoot and locate the high CPU usage issue of the MongoDB instance in terms of query statements, slow log, and execution plans.

<span id=".5p-l55yL5q2j5Zyo6L-Q6KGM55qE6K-t5Y-l"></span>
## Viewing running statements

Perform the following steps to view the statements running in the database:


1. Connect to the instance via the Mongo Shell tool. For more information, refer to [Connect to instance via Mongo shell tool](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

2. Run the `db.currentOp()` command on the target instance to view the statements running in the database.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information about the <code>db.currentOp()</code> command, refer to <a href="https://www.mongodb.com/docs/v4.0/reference/method/db.currentOp/">db.currentOp()</a>.   </div>
   

   Example of a partial return result is as follows.

   ```JSON
   {
                           ...
                           "client" : "192.168.***.***:****",
                           "appName" : "MongoDB Shell",
                           "active" : true,
                           "currentOpTime" : "2023-01-28T16:45:51.243+0800",
                           "opid" : 7339****,
                           ...
                           "secs_running" : NumberLong(0),
                           "microsecs_running" : NumberLong(137),
                           "op" : "command",
                           "ns" : "admin.$cmd.aggregate",
                           "command" : {
                                   "currentOp" : 1,
                                   ...
                                   "$db" : "admin"
                           },
                           "numYields" : 0,
                           "locks" : {
                           },
                           "waitingForLock" : false,
                           "lockStats" : {
                           },
                           ...
                           
   }
   ```
   

   You need to focus on the following fields in the response.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view and analyze whether time\-consuming requests exist in the response. For example, the CPU usage is normal during routine service operations, but increases after you perform some operations that require full table scan, which makes service response slow. You need to focus on these requests. For more information about the fields in the response, refer to <a href="https://www.mongodb.com/docs/v4.0/reference/command/currentOp/#output-fields">currentOp</a>.   </div>
   

   
   |Field |Description |
   |---|---|
   |`client` |Information of the client that initiates the request (including the IP address and port number). |
   |`opid` |Identifier of the current operation. You can run the `db.killOp(opid)` command to terminate the current operation. For more information about the `db.killOp()` command, refer to [db.killOp()](https://www.mongodb.com/docs/v4.0/reference/method/db.killOp/). |
   |`secs_running` |Duration of the current operation (period from the operation start to the current time), in seconds. If the operation lasts for too long, it is recommended to check whether the request is reasonable. |
   |`microsecs_running` |Duration of the current operation (period from the operation start to the current time), in microseconds. If the operation lasts for too long, it is recommended to check whether the request is reasonable. |
   |`ns` |Collection of targets in the current operation. |
   |`op` |Type of the current operation, such as `query`, `update`, `insert`, or `command`. |
   |`locks` |Lock\-related information. For more information, refer to [Concurrency Description](https://www.mongodb.com/docs/v4.0/faq/concurrency/). |
   


<span id=".5p-l6K-i5oWi5pel5b-X"></span>
## Querying slow logs

If the CPU usage of your instance increases out of expectation but no time\-consuming requests are found in the output of the `db.currentOp()` command, you can analyze slow requests to troubleshoot and locate the fault.

By default, the MongoDB database records requests with an execution time of over 100 ms into slow logs. You can refer to the following steps to analyze slow logs and identify the cause of abnormal CPU usage increases.


1. Query slow logs on the MongoDB console. For more information, refer to [Querying slow logs](https://docs.byteplus.com/en/docs/mongodb/query-slow-log).

2. Analyze slow logs to find the cause of the abnormal CPU usage increase of the MongoDB instance.

   The following table lists some keywords in slow logs, causes for slow logs, and some handling suggestions.

   
   |Cause for slow log |Keyword |Suggestion |
   |---|---|---|
   |Full table scan executed |* `COLLSCAN`<br><br>* `docsExamined` |* If a request in the slow log contains the `COLLSCAN` keyword, this request executed a full table scan, occupying a large number of CPU resources. If such requests are frequent, you can create indexes for queried fields to optimize the issue.<br><br>* You can determine the number of documents scanned in the current query request based on the value of the `docsExamined` field. A larger value indicates more CPU resources occupied by the current request. |
   |Improper index |* `IXSCAN`<br><br>* `keysExamined` |* If a slow log contains the `IXSCAN` keyword, the request uses indexes.<br><br>* You can determine the number of indexes scanned in the current request based on the value of the `keysExamined` field. A larger value indicates higher CPU usage.<br><br>   Proper index setup has a major impact on the cost and execution speed of request queries. More indexes do not mean better, as the write and update performance will be affected. If your applications have more write operations, indexes may have an impact on the performance. We recommend you create proper indexes based on your business characteristics.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If proper indexes have been set but the optimal index is not used during the execution of a query plan. At this point, you can run the <code>PlanCache.clear()</code> command to clear the query cache of the instance and allow the instance to select another index from PlanCache. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/instance-not-choose-optimal-index">Why doesn't instance always select optimal index</a>.   </div><br>    |
   |Large data sorting |* `SORT`<br><br>* `hasSortStage` |* If a slow log contains the `SORT` keyword, optimize sorting through indexes.<br><br>* When the `hasSortStage` field in a query request is set to `true`, sorting is required in the current request.<br><br>   If sorting cannot be implemented through indexes, the MongoDB database sorts the items in the query result, which consumes a large amount of CPU resources. In this case, you can create indexes for frequently sorted fields to optimize querying and reduce CPU resource consumption. |
   


<span id=".5YiG5p6Q5omn6KGM6K6h5YiS"></span>
## Analyzing execution plans

MongoDB provides the `explain()` command for checking statistical data of the specified query plan, including the indexes used, whether the query statement is covered by the indexes, the number of scanned indexes, the number of read documents, the number of returned documents, and the time taken to execute the query.

You can create proper indexes based on the preceding information in a query plan to optimize querying and reduce CPU resource consumption. For more information about the output of the `explain()` command, refer to [Explain results](https://www.mongodb.com/docs/v5.0/reference/explain-results/#queryplanner).

<span id=".5L2_55So5LiO5Lia5Yqh6LSf6L2955u45Yy56YWN55qE5a6e5L6L"></span>
## Using an instance matching your business load

If the CPU usage is still high after you set proper indexes for a database request based on the statements running in the database, slow request, and analysis result of an execution plan, you must evaluate whether the current configuration of the MongoDB instance meets your business needs.

You can [Viewing monitoring data](https://docs.byteplus.com/en/docs/mongodb/view-monitoring-data) to analyze the use of instance resources and carry out performance testing on the MongoDB database to check whether the current instance specification can provide the device performance and service capability needed by your business. Data analytics For more information about how to upgrade specification of MongoDB instance, refer to [Modifying instance configuration](https://docs.byteplus.com/en/docs/mongodb/solutions-for-spec-modification).
