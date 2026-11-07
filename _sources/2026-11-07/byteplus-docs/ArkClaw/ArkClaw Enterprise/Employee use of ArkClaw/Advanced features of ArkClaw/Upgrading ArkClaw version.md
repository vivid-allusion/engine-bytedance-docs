---
title: "Upgrading ArkClaw version"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_ArkClaw_version_"
---

Regularly upgrading ArkClaw instances is a key measure to ensure the stable, secure, and efficient operation of the agent gateway. It addresses security risks in earlier versions to promote comprehensive system optimization and capability improvement. It also allows you to use new features to support business iteration. When the platform releases the latest version, we recommend that you upgrade ArkClaw instances to the latest version promptly. This topic describes how employees can upgrade their ArkClaw instance version.

<span id="PEDIwFqg"></span>
## Background

ArkClaw instance versions are managed and released by the platform. After the platform releases the latest version, employees will receive an upgrade notification and release notes. We recommend that you upgrade ArkClaw instances promptly. The detailed upgrade process is as follows:


1. After the platform releases the latest version, employees can check for updates to retrieve the latest version and its release notes.

2. After verification, employees can proceed with the upgrade. The system will automatically back up instance data before the upgrade starts. If the backup fails, the upgrade task will be terminated immediately. If the backup succeeds, the upgrade will start.

3. During the upgrade process, Core, Skill, and Plugin of the instances will be sequentially upgraded. If the upgrade fails, the instances will be automatically rolled back to the version before the upgrade to ensure the instances are available. If the upgrade succeeds, the upgrade process will end.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d7a0519cc19e3fd0bf5e545187d83a1.png) </span>

<span id="qiMCgEE8"></span>
## Prerequisites

The platform has released the latest ArkClaw version. Employees can check for updates to view the new version and its release notes.

<span id="3G1RxeNw"></span>
## Limits


* The platform only maintains Core, Skill, and Plugin that are officially provided. For other items that you install, you need to maintain them yourself.

* Only instances in the "Running" state can be upgraded. During the upgrade, the service will be interrupted for about 10 to 15 minutes. To prevent normal business operations from being affected, we recommend that you perform upgrades during off\-peak hours.

* Data automatically backed up when employees upgrade ArkClaw instances will overwrite data manually backed up by employees.

* ArkClaw uses the `x.y.z` format for version tagging, where `x` indicates the major version, and `y` and `z` indicate minor versions. Cross\-major\-version updates may contain incompatible changes, and one\-click upgrade to the latest version is not supported. Minor versions within the same major version support one\-click upgrade to the latest version.

   * Minor versions within the same major version are backward compatible and support one\-click upgrade to the latest version. Example: If the current version is 1.0.1 and the latest version is 1.2.0, both belong to the same major version. You can still upgrade directly from 1.0.1 to 1.2.0 with one click, even if there are intermediate minor versions in between.

   * Cross\-major\-version updates may involve incompatible changes. If you need to upgrade across major versions to the latest version, you need to complete the upgrade in multiple steps. Example: If the current version is 1.0.1 and the latest version is 2.2.3, the upgrade spans the major version 2.0.0. To upgrade to the latest version, you need to perform two steps: First upgrade from 1.0.1 to 2.0.0, and then upgrade from 2.0.0 to 2.2.3.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47fafad4a5be70d37e275dd9aab54bc1.png) </span>


<span id="1gOaDqe8"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page and click the details icon in the upper\-right corner.

&nbsp;

3. Click the "Check for updates" button to check whether the platform has released a new ArkClaw version.

   * If the prompt "New version available" appears, the platform has released a new version. You can view the release notes and version details, and perform the upgrade.

   * If the prompt "Already the latest version" appears, no new version has been released, and no upgrade is needed.

4. Click **Update now** to start the upgrade. The process consists of three stages: pre\-check, current version backup, and component upgrade. Click **View logs** on the upgrade page to view upgrade\-related log information in real time.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The upgrade takes about 10 to 15 minutes. Do not close the page during the upgrade.   </div>
   

5. After the upgrade succeeds, click **Completed** to return to the conversation page. You can resume normal interaction with ArkClaw and use the new version features.


<span id="MCuh5vVO"></span>
## What to do next


* If the upgrade fails, ArkClaw will automatically roll back to the version before the upgrade. Common causes for upgrade failure and solutions are as follows:

   
   |Common cause |Description |Solutions |
   |---|---|---|
   |Backup failed |The data of the ArkClaw instance failed to be backed up. This causes the upgrade job to be interrupted. |In most cases, the issue can be resolved by retrying the upgrade. |
   |Upgrade the OpenClaw manually |The employee manually upgraded the OpenClaw version, causing a conflict with the version released by the platform. This leads to an upgrade failure.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">We recommend upgrading to the version pushed by the platform. Enterprise employees should not upgrade the OpenClaw or other core components to any other versions.</div><br> |Manually roll back the OpenClaw version to match the platform\-released version and then retry, or obtain technical support via [feedback](https://docs.volcengine.com/docs/87732/2431039). |
   |Failed to upgrade the manually installed version |Employees manually installed tools such as Skills and Plugins that are not provided by the platform, which led to an upgrade failure.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">We recommend using the Skills and Plugins provided by the platform and not installing tools from other sources.</div><br> |Manually upgrade tools installed by employees, such as Skills and Plugins, and then retry, or obtain technical support via [feedback](https://docs.volcengine.com/docs/87732/2431039?lang=zh). |
   

* If you encounter usage issues after the upgrade, go to the data page and use the data automatically backed up before the upgrade (backup data on the "Manual backup" tab) to quickly restore to the pre\-upgrade version. For more details on backup and restoration, refer to [Backing up and restoring ArkClaw data](https://docs.volcengine.com/docs/87732/2431034?lang=zh).

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">We do not recommend that you continue using the earlier version on the platform. You can use this method to quickly roll back to the version before the upgrade only if the latest version has issues that affect normal business operation.   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">You still need to upgrade to the latest version after you roll back to the version before the upgrade by using backup data.   </div>
