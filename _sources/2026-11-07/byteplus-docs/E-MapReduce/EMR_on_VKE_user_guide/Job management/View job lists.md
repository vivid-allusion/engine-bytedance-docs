---
title: "View job lists"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/View_job_lists"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Job management is currently in the allowlist invitation testing phase and provides the capability to view job information for the EMR on VKE product type. We welcome you to try it out and provide valuable feedback. Support for more features and product types, as well as the official release of this module, is coming soon.</div>


In the **Job Management** module, you can view job information for all EMR clusters under the current primary account.

<span id="e408cc16"></span>
## procedure


1. In the Volcano Engine E\-MapReduce console, click the **Job management** \> **Assignment list** item in the left sidebar.

2. The page displays the job lists from each EMR cluster under the current primary account for the past 15 days. The columns in the table include:

   * **Job name / ID**: Displayed in two rows. The first row shows the **job name**, and the second row shows the **job ID**. You can click the **job name link** to enter the **job details** page and view detailed information for a single job. On the **job details** page, in addition to the information shown on the job list page, the following information is also included:

      * The job's **execution engine**.

      * The EMR **cluster ID** where the job is running.

      * A redirect link to the **cluster details page** of the EMR cluster where the job is running.

      * The specific name of the **Web UI**, such as Spark History Server, Ray Dashboard, Ray History Server (if installed), and more.

   * **Job type**: Such as Spark, Ray, and more.

   * **Status**: Includes RUNNING, SUCCEEDED, FAILED, and more.

   * **Resource type**: The product form of the EMR cluster where the job is running. For example, EMR on VKE and more.

   * **Resource name**: The name of the EMR cluster where the job is running.

   * **Allocated CPU (vCPU)** : The total number of CPU cores allocated to the job (if explicitly specified when submitting the job).

   * **Allocated memory (GiB)** : The total memory allocated to the job (if explicitly specified when submitting the job), Unit: GiB, which is 2³⁰ bytes.

   * **Submission time**: The time the job was submitted.

   * **End time**: The time the job finished running.

   * **Duration**: The total runtime of the job or the elapsed time up to the current moment.

   * **Operation**:

      * **Web UI**: Supports redirecting to the corresponding Web UI, such as Dashboard, History Server pages, and more. If the Web UI is inaccessible (for example, if the VKE cluster is not configured with Ingress or the EMR cluster has been released), the Web UI link will be grayed out.

3. You can search the job list by **job name / ID**, **status**, **submission time range**, and **resource name / ID**.

4. You can filter the job list by **job type** and **resource type**.

5. You can sort the job list by **submission time** and **end time**. Supports ascending and descending order.

6. The job list is displayed using **pagination**. You can select the number of job entries to display per page in the lower right corner of the job list page, and jump to a specified page number.

7. Click the Refresh button in the upper right corner of the page Assignment list to reload the job list and refresh the displayed content with the latest data.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only viewing Spark and Ray jobs under the EMR on VKE product type is supported.</div>


   * <div data-tips="true" data-tips-type="tip">For Spark jobs, you can view jobs submitted via Spark Operator, as well as native spark\-submit, spark\-shell, spark\-sql, and other methods in either cluster mode or client mode.</div>


   * <div data-tips="true" data-tips-type="tip">For Ray jobs, you can view jobs submitted as RayJob custom resource types via KubeRay Operator, as well as Ray jobs submitted within RayCluster.</div>


* <div data-tips="true" data-tips-type="tip">Currently, you can view information for jobs submitted within the past 15 days.</div>


* <div data-tips="true" data-tips-type="tip">You can view information for all running and historical jobs in all running and historical EMR clusters under the current primary account.</div>


* <div data-tips="true" data-tips-type="tip">The current job information collection cycle is 1 minute. There may be a delay from Submit Job to when it can be observed in the job list.</div>
