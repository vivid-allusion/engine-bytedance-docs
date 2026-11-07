---
title: "SparkSQL jobs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/SparkSQL_jobs"
---

EMR Serverless supports users in submitting SparkSQL jobs, suitable for interactive data queries, ETL tasks, report generation, and many other scenarios. This document introduces the procedure for submitting SparkSQL jobs through multiple methods, including the console, SDK, and JDBC.

<span id="简介"></span>
# Context

EMR Serverless Spark supports the following two types of SparkSQL jobs.


|Comparison items |Standard SparkSQL jobs |Pre\-launch SparkSQL jobs |
|---|---|---|
|Job type definition |When using the Default compute group in either the public queue or dedicated queue, submitting a task will temporarily launch an exclusive SparkSQL job for you. You can customize parameters such as CPU and memory used by the Driver and Executor in the SparkSQL task. |When using the Spark SQL Warehouse compute group in the dedicated queue, this compute group provides SQL\-specific resources. Submitting a SparkSQL job with this compute group will send it to a dedicated pre\-launch service, offering low overhead and low latency. There is no need to request temporary resources, and jobs can be completed in seconds. When SQL\-specific resources are limited, EMR Serverless Spark can automatically reuse elastic resources within the compute group to achieve resource elasticity for tasks.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Because the compute group is pre\-launched, the Driver/Executor CPU/Memory settings in SQL do not take effect. If you have customized cluster specification requirements, please <a href="https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D">submit a ticket</a> to contact Volcano Engine technical personnel.</div><br> |
|Spark syntax support |EMR Serverless syntax is fully compatible with open\-source Spark 3.5.1. For detailed syntax, refer to: [Spark 3.5.1 syntax](https://spark.apache.org/docs/latest/sql-ref-ansi-compliance.html). ||
|Job submission methods |You can parse and submit SparkSQL tasks through the EMR Serverless console, SDK, JDBC, and other methods. It is ready to use out of the box, with no additional cluster management required. ||


<span id="6a0a7f50"></span>
# Prerequisites


* An EMR Serverless queue has been created, and you have Developer/Admin permissions of the compute group. For operation details, see: [Create a queue](https://docs.byteplus.com/docs/E-MapReduce/Create_a_queue), [Queue permissions](https://docs.byteplus.com/docs/E-MapReduce/Queue_permissions).

* A compute group has been created. Currently, general compute groups and Spark SQL compute groups can be used. For operation details, see [Create and manage compute groups](https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups).


<span id="f942109d"></span>
# Submit SparkSQL jobs

<span id="4f5e4a5e"></span>
## Submit Job: Through the console


1. Log in to the EMR Serverless console, click Resources\>Serverless in the left navigation bar, select the Serverless queue resource for the task to be created, and enter the queue resource details page.

2. On the upper right corner of the queue details page, click SQL Editor to enter the SQL task editing page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4280cbeb18274bd588ada90b427d67fc~tplv-goo7wpa0wc-image.image) </span>

3. On the job editing page, select the metadata database table and set resources. After completing these steps, you can edit the SQL job in the job editing area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/718ac353b8064eafb222eee1cbb6dcd7~tplv-goo7wpa0wc-image.image) </span>

   1. Edit the SparkSQL job in the job editing box. After editing, you can use the **Format** button at the lower left corner of the editing box to standardize the job being edited.

   2. After completing SQL job editing, you can select compute resources using the **Queue** and **Compute Group** options in the upper right corner of the console. Once finished, click the **Run** button at the lower left corner to submit the job.

4. After the job is submitted, a **Submission Successful** indicator will pop up. When the task executes successfully, the current query results will be displayed, and the query log below will show the job ID you submitted and the current task status. You can further view detailed task information in job management.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After submitting a task to the EMR Serverless cluster, the Spark Web UI will be displayed in the query log. You can click <strong>Open link</strong> to view detailed execution status of the current task in the Web UI.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The console supports downloading query logs, query results, and query code. Files are stored in CSV format by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The console also allows you to search for key information in results by clicking the magnifying glass button and entering keywords on the <strong>Query results</strong> tab.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the <strong>History</strong> tab, you can view the results and code of historical jobs in the current queue.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If there is an issue with the SQL, parsing will fail and an error reason will be provided. For common parsing failure reasons, see <a href="https://docs.byteplus.com/docs/undefined/68da347342e561058e056aa0">常见问题</a>.   </div>
   


<span id="dbff9b4d"></span>
## Submit Job: Through SDK

Currently, EMR Serverless supports two types of SDKs: Java and Python.


* For instructions on using the Java SDK, see [Java Query SDK](https://docs.byteplus.com/docs/undefined/69a93cba8252b50542c1d9e0).

* For instructions on using the Python SDK, see [Python Query SDK](https://docs.byteplus.com/docs/undefined/69a93cff9523f10505cee5c0).


<span id="6b67858d"></span>
## Submit Job: Through JDBC

When submitting Spark SQL via JDBC, you must specify a Spark compute group. The Default compute group does not support the Submit Job operation via JDBC. For usage instructions, see the documentation: [JDBC usage](https://docs.byteplus.com/docs/E-MapReduce/95191)

<span id="解析spark-sql"></span>
# View and diagnose job instances

After submitting a job, you can also view the details of all submitted job run instances on the Job center \> Job instance page, including run status, job type, resource details, submitter, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4ff2963cba543d1a50fb25d9508db7e~tplv-goo7wpa0wc-image.image) </span>


* At the top of the page, you can quickly filter job instances by scope, submitter, and other criteria to view the details of the job instances.

* For jobs that failed to run, you can click "Log" to view detailed job run logs and locate the cause of the failure; you can also use the "AI diagnosis" feature to perform intelligent job diagnosis.
