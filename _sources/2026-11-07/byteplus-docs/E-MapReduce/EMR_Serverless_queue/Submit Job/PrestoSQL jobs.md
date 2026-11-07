---
title: "PrestoSQL jobs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/PrestoSQL_jobs"
---

Serverless Presto, based on Apache® Presto, provides native interactive query capabilities and supports users in performing data analysis and ETL operations using SQL.

> Apache Presto, the names of other Apache projects, and the ASF logo are either registered trademarks or trademarks of the Apache Software Foundation in the United States and/or other countries.


<span id="45ceb210"></span>
# important notes

EMR Serverless Presto is fully compatible with the syntax of open\-source Presto version 0.280. For detailed syntax, see: [Presto Documentation](https://prestodb.io/docs/0.280/index.html).

<span id="cc11360f"></span>
# prerequisites


* An EMR Serverless queue has been created, and you have Developer/Admin permissions for the queue. For operation details, see: [Create a queue](https://docs.byteplus.com/docs/E-MapReduce/Create_a_queue), [Queue permissions](https://docs.byteplus.com/docs/E-MapReduce/Queue_permissions).

* A compute group has been created. Currently, public queues and PrestoSQL compute groups are supported. For operation details, see [Create and manage compute groups](https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups).


<span id="7ee8ea2e"></span>
# Submit Job

<span id="be68f716"></span>
## Submit Job: via the console


1. Log in to the EMR Serverless console, click Resources\>Serverless in the left navigation bar, click the Serverless queue resource for the task to be created, and enter the queue resource details page.

2. In the upper right corner of the queue details page, click SQL Editor to enter the SQL task editing page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4280cbeb18274bd588ada90b427d67fc~tplv-goo7wpa0wc-image.image) </span>

3. On the job editing page, select the metadata table and set resources. After completing these steps, you can edit the SQL job in the job editing area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/718ac353b8064eafb222eee1cbb6dcd7~tplv-goo7wpa0wc-image.image) </span>

   1. Edit the PrestoSQL job in the job editing box. After editing, you can use the **Format** button in the lower left corner of the editing box to standardize the job being edited.

   2. After completing SQL job editing, you can select compute resources using **Queue** and **Compute Group** in the upper right corner of the console. After selection, click the **Run** button in the lower left corner to submit the job.

4. After the job is submitted, a **Submission Successful** indicator will pop up. When the task executes successfully, the current query result will be displayed, and in the query log below, the job ID of your submission and the current task status will be shown. You can further view detailed task information in job management.


<span id="58ace5f0"></span>
## Submit Job: via SDK

Currently, EMR Serverless supports two types of SDKs: Java and Python. For instructions on using the Java SDK, see: [Java Query SDK](https://docs.byteplus.com/docs/undefined/69a93cba8252b50542c1d9e0); for instructions on using the Python SDK, see: [Python Query SDK](https://docs.byteplus.com/docs/undefined/69a93cff9523f10505cee5c0).

<span id="9826459c"></span>
## Submit Job: via JDBC

When submitting PrestoSQL via JDBC, you must specify a Presto compute group. The Default compute group does not support job submission via JDBC. For usage, see the documentation: [Connect Presto](https://docs.byteplus.com/docs/E-MapReduce/95180).

<span id="2aef8588"></span>
# View and diagnose job instances

After submitting a job, you can also view the details of all submitted job run instances on the Job center \> Job instance page, including run status, job type, resource details, submitter, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4ff2963cba543d1a50fb25d9508db7e~tplv-goo7wpa0wc-image.image) </span>


* At the top of the page, you can quickly filter job instances by scope, submitter, and other criteria to view the details of the job instances.

* For jobs that failed to run, you can click "Log" to view detailed job run logs and locate the cause of the failure; you can also use the "AI diagnosis" feature to perform intelligent job diagnosis.
