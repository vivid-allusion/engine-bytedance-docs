---
title: "Release function"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Release_function"
---

After creating the function, it needs to be released to start running function\-related operations. This article mainly describes how to release a function.

<span id="background-information"></span>
## Background Information

Function service supports both full release and canary release.

**Full release**


* The traffic ratio for the new version is 100%.

* After a successful full release, initiating the next release is permitted.


**Canary release**


* The traffic ratio for the new version ranges from 10% to 100%. Once the set ratio is reached, manual confirmation of the next steps is required, such as adjusting the ratio, proceeding with a full release, or performing a rollback.

* In a canary release scenario, the traffic proportion of the new version has not reached 100% and is in the **Releasing** state; initiating another release is not permitted.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The first release defaults to a full release.</div>


* <div data-tips="true" data-tips-type="tip">Secondary releases support selecting the release method.</div>



<span id="prerequisites"></span>
## Prerequisites

A function has been created; for specific operations, refer to [Creating a function](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection).

<span id="procedure-steps"></span>
## Procedure steps


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the **Functiont** page, find the function for which you need to create a trigger and click its name.

4. In the top right corner of the function details page, click **Release** and set the release parameters.

   
   |Parameter |Description |
   |---|---|
   |Function revision |Select the function revision to release online:<br><br><br>* **Latest**: Automatically creates a new revision based on the latest edited function code and configurations, and releases it online.<br><br>* Specific revision number: Releases the selected revision online. A new release order will be initiated to rollback the online traffic to the selected revision. |
   |Version description |You can enter text to describe the function revision that is about to be released. The character limit is 200 characters, and it can be left blank. |
   |Minimum number of instances |When releasing a function revision for the first time, this parameter needs to be set. The minimum number of instances refers to[ reserved instances](https://docs.byteplus.com/en/docs/faas/Reserved_instance). The system will maintain at least this number of instances, running continuously until you set it to zero. Reserved instances will continue to be billed during operation; for billing details, refer to [Billing](https://docs.byteplus.com/en/docs/faas/Billing).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum number of instances for microservices applications must be at least one.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For subsequent adjustments to the minimum number of instances, refer to <strong>Resource management</strong> <strong>\> Resource allocation \> Instance number range</strong> and edit.</div><br> |
   |Maximum number of instances |When releasing the first version of the function, you need to set this parameter. Set the maximum number of instances required for the function to carry the business (scale\-out limit). After the function is successfully released, the set function resources will take effect.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For subsequent adjustments to the maximum number of instances, go to <strong>Resource management</strong> <strong>\> Resource allocation \> Instance number range</strong> and edit.</div><br> |
   |Release mode |When re\-releasing a function revision, you can choose the release method based on your needs.<br><br><br>* Full release: The new version accounts for 100% of the traffic.<br><br>* Canary release: You can customize the traffic distribution between the online revision and the upcoming canary revision. If you want to observe the behavior of new and old function versions, you can choose a canary release.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When there is a canary revision of the function, requests will be randomly sent to the new and old function revisions according to the traffic proportion.</div><br> |
   |Deployment Details |Show the configuration changes and code modifications between the upcoming function revision and the online revision. |
   

5. Click **Confirm**, and you will be redirected to the current function's **Release management \> Release details** page, where the function begins to release.


<span id="what-to-do-next"></span>
## What to do next


* During the function release process, real\-time observation of the release progress is supported. For detailed information, refer to [Observation release process](https://docs.byteplus.com/en/docs/faas/Observation_release_process).

* For **Event functions**, **Web applications**, and **Task**, after a successful full release, you can create triggers, set up function trigger logic, and activate function operations. For detailed operations, refer to [Creating triggers](https://docs.byteplus.com/en/docs/faas/Trigger_management).
