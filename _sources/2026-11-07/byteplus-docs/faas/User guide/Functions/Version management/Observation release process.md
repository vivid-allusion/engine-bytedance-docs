---
title: "Observation release process"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Observation_release_process"
---

During the function release process, you can observe the release progress of the target version in real\-time on the **Release Management \> Release Details** page of the current function. This article introduces the information displayed and the actions that can be performed during the function release process.

<span id="basic-information"></span>
## Basic information

Display the change records for this release (historical and target versions), the release percentage, start and end times, and other details such as the description of this release.

<span id="old-and-new-version-ratio"></span>
## Old and new version ratio

Display the traffic distribution between the current target version and historical versions in real\-time through a progress bar. When the traffic ratio of the target version reaches 100%, the release is complete, and the status of the release record is **Release Complete**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the context of a canary release, once the set release ratio is achieved, the function remains in <strong>release in progress</strong> status. You can gradually adjust the traffic ratio based on your needs to ensure stable service operation during the canary roll\-out.</div>



* <div data-tips="true" data-tips-type="tip">Supports dragging the progress bar at any time to adjust the traffic distribution between the new and old versions.</div>


* <div data-tips="true" data-tips-type="tip">Supports <strong>full release</strong> click to perform a full release of the canary revision. After the release, the current status of the release work order is <strong>Release Completed</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Supports <strong>rollback</strong> click, cancels the current release work order, and rolls back the live traffic to the version before this release. After the rollback is successful, the current status of the release work order is <strong>Rollback Completed</strong>.</div>



<span id="instance-list"></span>
## Instance list

Displays the number and status of new and old version instances during the release process, facilitating operational maintenance of abnormal instances.


|Feature |Description |
|---|---|
|Logging |View real\-time logs of the current function instance. |
|Webshell |Through Webshell, you can log in to the function instance and perform corresponding command line operations. For example, view the environment information of the instance and debug the function. |
|Migrate |If your function instance is abnormal, you can restart an instance through the instance migration feature. |


<span id="deployment-details"></span>
## Deployment details

Under non\-first\-time release scenarios, display the config and code change points compared to the target version against historical versions.

<span id="related-operations"></span>
## Related operations


|Feature |Description |
|---|---|
|Roll back |If the function is being released or the release has failed, rollback is supported. Rollback will cancel the current release work order and rollback the online traffic to the version before this release. After the rollback is successful, the current work order status is **rolled back**. |
|Adjust the release ratio |In the canary release scenario, once the preset proportion is reached, you can drag the progress bar to adjust the traffic share between the new and old versions. |
|Full release |In the canary release scenario, once the preset ratio is reached, a full release is possible. After a successful release, the status of the current release ticket is **release completed**. |
|Retry |For release failures caused by system errors, manual retry is supported.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the function release fails, the details page will display error messages and detailed logs to assist in troubleshooting.</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If it is a system error, manual retry is supported.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the issue is related to user code or configuration, it is recommended to rollback the current work order first, and after completing code and configuration modifications, re\-release the function.</div><br> |
