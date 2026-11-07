---
title: "Upgrading add-ons"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on"
---

VKE allows you to upgrade add\-ons. If any of your installed add\-ons have the **Upgradable** label, we recommend upgrading them to ensure the availability of related features.

<span id=".5Y2H57qn6aG755-l"></span>
## Upgrade instructions


* The change descriptions, impacts, and maintenance status vary based on different versions of add\-ons. Before you upgrade add\-ons, see [Add-on release notes](https://docs.byteplus.com/en/docs/vke/Add-on-release-notes) to learn about the version details of the add\-ons to be upgraded.

* The upgrade feature in the console allows you to upgrade add\-ons to the latest version with a few clicks. You cannot specify a specific version.

* Before you upgrade the add\-on, we recommend checking and resolving all issues that may affect the cluster upgrade.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · apply for trial</strong></a>]: This upgrade check feature is currently in beta. Submit an application to use it. For more information about the feature, see <a href="https://docs.byteplus.com/en/docs/vke/Add-on_upgrade_check">Add\-on upgrade check</a>.   </div>
   

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An add\-on has been installed. For instructions, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation pane, click **Cluster**. On the page that appears, click the name of the cluster that you need to configure.

3. On the cluster management page, click **Addons** in the left navigation bar.

4. When an add\-on can be upgraded to the latest version, the **Upgradable** label will appear in the upper\-right corner of the add\-on section.

5. In the upper\-right corner of the target add\-on section, click `...` \> **Upgrade**.

6. In the message that appears, view the details related to the add\-on upgrade, such as the version information, add\-on release notes, and upgrade impacts. After you confirm that all information is correct, click **Confirm**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For add\-ons that require additional configuration, specify the parameters and upgrade the add\-ons based on the parameter descriptions in <a href="https://docs.byteplus.com/en/docs/vke/Installing-an-add-on">Installing add\-ons</a>.   </div>
