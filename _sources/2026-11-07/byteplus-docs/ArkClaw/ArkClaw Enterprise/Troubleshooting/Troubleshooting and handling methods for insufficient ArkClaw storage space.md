---
title: "Troubleshooting and handling methods for insufficient ArkClaw storage space"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Troubleshooting_and_handling_methods_for_insufficient_ArkClaw_storage_space"
---

When an ArkClaw instance runs out of storage space, an insufficient storage notification will be triggered. You can receive reminders via [system notifications](https://docs.byteplus.com/en/docs/87732/2356378?lang=zh) or configured [message channels](https://docs.byteplus.com/en/docs/87732/2266749?lang=zh). This issue may cause file write failures, dependency installation interruptions, code retrieval errors, task execution delays, and other failures.

This topic guides you to quickly resolve the insufficient storage space issue and ensure stable business operations by clearing redundant files, releasing system cache, or scaling up storage capacity.

<span id="fu9zjJt3"></span>
## Handling methods for insufficient storage space

The following three methods are provided to resolve the insufficient storage space issue. Select a method based on your needs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you are <strong>temporarily unable to determine</strong> the method, we recommend that you troubleshoot and resolve the issue in the following order: <strong>Clear large files \> Clear cache data</strong>.</div>



|**Handling method** |Application scenarios |**Chargeable** |Description |
|---|---|---|---|
|Clear large files |Applicable to scenarios where project files, installation packages, audio and video files, compressed packages, and various generated files accumulate over the long term and redundant content needs to be cleared to release storage capacity. |No |Manually delete large files that are no longer required to fully release storage space. |
|Clear cache data |Suitable for scenarios where you need to quickly release partial storage space or troubleshoot anomalies arising from accumulated temporary cache.<br><br> |No |Only temporary system cache will be cleared. Business data and installed plugins will not be modified, which helps ease storage pressure temporarily. |


<span id="pcVe4WdS"></span>
## Method 1: Clear large files (recommended)

ArkClaw generates many temporary files for tasks, consuming significant storage space. You can manually delete unused files to free up storage space.

<span id="Bnm3OAes"></span>
### Operation instructions

Before clearing large files, [view the workspace file list](https://docs.byteplus.com/en/docs/ArkClaw/File_space?lang=en#146n9nQS) first and [download the files to be retained to your local device for backup](https://docs.byteplus.com/en/docs/ArkClaw/File_space?lang=en#4mZkvKCU).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You may prioritize checking and clearing the following items in the workspace file list:</div>



* <div data-tips="true" data-tips-type="default">Idle and unused project directories.</div>


* <div data-tips="true" data-tips-type="default">Images, videos, documents, and exported files already saved locally.</div>


* <div data-tips="true" data-tips-type="default">Compressed packages, installation packages, and legacy version files.</div>


* <div data-tips="true" data-tips-type="default">Duplicated uploaded data files.</div>


* <div data-tips="true" data-tips-type="default">Temporary and intermediate files no longer needed after task completion.</div>



<span id="IUII3iQC"></span>
### Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page, and select "File management" in the directory tree on the left.

3. Delete target files in the file space. For details, refer to [Deleting files](https://docs.byteplus.com/en/docs/ArkClaw/Claw_cloud_disk?lang=en).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Make sure the files are no longer needed before deletion. If you are unsure about the purpose of the files, back them up first before deletion.   </div>
   

<span id="jVZkw22j"></span>
## **Method 2: Clear cache data**

Clear temporary cache data generated during ArkClaw operation, such as npm cache, npx runtime cache, and system package manager cache, to quickly release part of storage space.

<span id="mLGS65ze"></span>
### Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. Clear temporary cache data with one click. For details, see [Clearing ArkClaw storage cache data](https://docs.byteplus.com/en/docs/ArkClaw/Clearing_ArkClaw_storage_cache_data__?lang=en).
