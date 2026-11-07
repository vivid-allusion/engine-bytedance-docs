---
title: "Viewing release process"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_release_process"
---

This topic describes the information displayed and the operations available during the runtime release process.

During the release, you can go to the "Version management \> Release history" page of the current runtime, click the target version ID to enter the release details page, and observe the release progress of the target version in real time.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_386a76fbec94550deb3bc9a174f5b6b3.png) </span>

<span id="x1Z08aCs"></span>
## Basic information

Displays the change record (historical version and target version) and the release ratio.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d0323ebfbf958d6ad699026e590e7b64.png) </span>

<span id="yPDO9mRW"></span>
## New and old version ratio

Displays the real\-time traffic ratio of the target version and historical version via a progress bar. The release is complete when the target version traffic ratio reaches 100%, and the release status becomes **Released**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a grey release, the runtime remains in the <strong>Releasing</strong> state after the configured release ratio is reached. You can gradually adjust the traffic ratio based on your needs to ensure stable service operation.</div>



* <div data-tips="true" data-tips-type="tip">You can drag the progress bar at any time to adjust the traffic ratio between the new and old versions.</div>


* <div data-tips="true" data-tips-type="tip">You can click "<strong>Change release ratio</strong>" to perform a full release of the grey version. After the release succeeds, the status of the current release task changes to <strong>Released</strong>.</div>


* <div data-tips="true" data-tips-type="tip">You can click "<strong>Cancel release</strong>" to cancel the current release task and roll back online traffic to the version before this release. After a successful rollback, the status of the current release task is <strong>Rolled back</strong>.</div>



<span id="5xvef88j"></span>
## Instance list

Displays the number and status of new and old version instances during the release, making it convenient to perform O&M tasks on abnormal instances.


|Feature |Description |
|---|---|
|Log |You can view real\-time logs of the current runtime instance. |


<span id="lVyyHy6b"></span>
## Related operation


|Feature |Description |
|---|---|
|Roll back |Rollback is supported when the runtime is in the "Releasing" or "Release failed" state.<br><br><br>* Rollback cancels the current release task and reverts online traffic to the version before the release.<br><br>* Associated components are rolled back at the same time. If associated components have been deleted, the rollback may fail. |
|Cancel release |Cancel the current release task and roll back online traffic to the version before the release. |
|Change release ratio |In a grey release, you can drag the progress bar to adjust the traffic ratio between the new and old versions after reaching the preset ratio.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Adjusting the grey release ratio is not supported during a rolling release process.</div><br> |
|Retry |For release failures caused by system errors, manual retry is supported.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the runtime release fails, the details page displays error information and detailed logs to help you troubleshoot issues.</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For failures caused by system errors, manual retry is supported.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">For failures caused by user code or configuration issues, we recommend that you first roll back the current task, modify the code and configuration, and then release the runtime again.</div><br> |
