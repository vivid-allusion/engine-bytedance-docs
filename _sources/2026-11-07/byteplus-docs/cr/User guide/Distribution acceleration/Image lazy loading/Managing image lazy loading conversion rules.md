---
title: "Managing image lazy loading conversion rules"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/manage-image-lazy-loading-conversion-rules"
---

You can enable, disable, and delete created image lazy loading conversion rules. This topic describes how to manage image lazy loading conversion rules.

<span id=".5byA5ZCv6KeE5YiZ"></span>
## Enable a rule

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Using this feature incurs additional image storage costs.</div>


* <div data-tips="true" data-tips-type="warning">Converting images for lazy loading takes time. We recommend configuring the conversion policy in advance and allowing sufficient time for the conversion to avoid affecting the service release date. For example, converting a 40 GiB image takes approximately 30 minutes.</div>



After the conversion rule is enabled, Nydus image replicas can be generated only for OCI artifacts that match the conversion rule and are pushed to CR.


1. Log in to the[ CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Instance list**. On the **Instance list ** page, click the name of the target instance.

4. On the Standard Edition instance details page, select **Distribution acceleration** \> **Image lazy loading** in the left navigation bar.

5. On the **Image lazy loading** page, click **Enable** in the **Actions** column of the target conversion rule.

6. Click **Confirm** to enable the rule.


<span id=".56aB55So6KeE5YiZ"></span>
## Disable a rule

You can disable image lazy loading conversion rules that are temporarily not needed, thereby suspending automatic image conversion.


1. Log in to the[ CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Instance list**. On the **Instance list ** page, click the name of the target instance.

4. On the Standard Edition instance details page, select **Distribution acceleration** \> **Image lazy loading** in the left navigation bar.

5. On the **Image lazy loading** page, click **Disable** in the **Actions** column of the target conversion rule.

6. Click **Confirm** to disable the rule.


<span id=".5L-u5pS56KeE5YiZ"></span>
## Modify a rule

You can modify the name, description, and acceleration rule of an image lazy loading conversion rule, and adjust the image lazy loading policy.


1. Log in to the[ CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Instance list**. On the **Instance list ** page, click the name of the target instance.

4. On the Standard Edition instance details page, select **Distribution acceleration** \> **Image lazy loading** in the left navigation bar.

5. On the **Image lazy loading** page, click **Modify** in the **Actions** column of the target conversion rule.

6. Configure the parameters for the image lazy loading conversion rule. For parameter descriptions, see [Create image lazy loading conversion rule](https://docs.byteplus.com/en/docs/cr/create-image-lazy-loading-conversion-rules?lang=en).

7. Click **Confirm** to complete the modification.


<span id=".5Yig6Zmk6KeE5YiZ"></span>
## Delete a rule

You can delete image lazy loading conversion rules.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For a rule with a conversion task in progress, the task is allowed to continue running in the background until completion and is not affected by the rule deletion.</div>



1. Log in to the[ CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Instance list**. On the **Instance list ** page, click the name of the target instance.

4. On the Standard Edition instance details page, select **Distribution acceleration** \> **Image lazy loading** in the left navigation bar.

5. On the **Image lazy loading** page, click **Delete** in the **Actions** column of the target conversion rule.

6. Click **Confirm** to complete the deletion.


<span id=".5p-l55yL6KeE5YiZ5Lu75Yqh"></span>
## View rule\-triggered tasks

When an OCI artifact that matches a conversion rule is pushed to CR, a conversion task is triggered. The method for viewing task details is as follows.


1. Log in to the[ CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Instance list**. On the **Instance list ** page, click the name of the target instance.

4. On the Standard Edition instance details page, select **Distribution acceleration** \> **Image lazy loading** in the left navigation bar.

5. On the **Image lazy loading** page, click the name of the target conversion rule.

6. In the **Execution history** section, view the task details.

   
   |Parameter |Description |
   |---|---|
   |Task ID |ID of the conversion task. Click a task ID to view the image names before and after conversion on the task details page. |
   |Status |The execution status of the conversion task.<br><br><br>* **Waiting**: The task is in the queue because the task execution quota has been reached. Only one task can run per rule at a time, and each instance supports up to 5 concurrent tasks. Subsequent tasks will be queued.<br><br>* **In progress**: The task has started but has not yet completed.<br><br>* **Success**: The task has completed, and at least one image was successfully converted.<br><br>* **Fail**: The task execution failed. Possible causes: the namespace does not exist, the OCI artifact repository is empty, or the instance is in an abnormal state. |
   |Execution progress |Displays the number of tasks to be processed and the number of tasks completed. |
   |Task creation time |The time when the conversion task execution is created. |
   |Execution start time |The time when the conversion task execution starts. |
   |Execution end time |The time when the conversion task execution ends. |
