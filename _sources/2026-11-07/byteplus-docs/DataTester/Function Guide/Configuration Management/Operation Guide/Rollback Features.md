---
title: "Rollback Features"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Rollback-Features"
---

<span id="一-名词解释"></span>
# 1. Term explanation


* **Rollback:**  refers to the act of restoring a variant value in effect on the line to the correct state of the previous full version in effect. For example, the version that takes effect online is in the release and has been fully released. You can click "Roll Back" to roll back the previous full version that takes effect.

* **Cancel publishing:**  Refers to the time set to release at a certain time in the future, but not yet at that time, choose to cancel publishing.

* **Set to the latest version:**  refers to the full history of the version, set to the latest version, you need to reset the release plan, that is, re\-go through the release process.


<span id="二-应用场景"></span>
# 2. Application scenario


* **Rollback:**  For example, a version that is being released has a lot of negative feedback from users, so you can roll back to the previous full amount of relatively safe versions that are in effect.

* **Cancel the release:**  For example, the scheduled release has been set, but suddenly found that the variant value of the release setting, the release range and other information are still incorrect, then you can choose to cancel the release of the version. After the modification is correct, republish it.

* **Set to the latest version:**  For example, there are many historical versions, and if you want to release a full version again, you can choose to set a full version to the latest version.


<span id="三-如何“回滚和取消发布-”"></span>
# 3. How to "Roll Back and Cancel Publishing"

<span id="_1-操作入口"></span>
## 1. Operation entrance

On the version list page, click "Release Progress" to display the release progress in a pop\-up window. You can roll back and cancel the release on the release progress page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e9533771b554f19a50f65184d5da28c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-回滚"></span>
## 2. Roll back

On the View Release Schedule page, you can roll back.

The current version is being released, it has been fully released, and it can be rolled back. If the rollback is successful, it will take effect immediately by default, and the previous full version will take effect immediately. If there is no full version in effect online, turn off the feature to take effect the local default.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8545432ee6c4314819ef9a404ac7068~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="_3-取消发布"></span>
## 3. Cancel publication

If you view the release plan page, you can cancel the release.

The release plan is "Timed Automatic Release" and the current version is to be released, so you can cancel the release. If the cancellation is successful, it will take effect immediately by default, and the previous full version will take effect immediately. If there is no full version in effect online, turn off the feature to take effect the local default.

<span id="四-如何“设为最新版本”"></span>
# 4. How to "set to the latest version"

<span id="_1-操作入口"></span>
## 1. Operation entrance

On the version list page, click "Set as latest version" to enter the editing page, save it, and generate a new version number. After the latest version is generated, you need to reset the release plan, that is, go through the release process again.

<span id="_2-设为最新版本"></span>
## 2. Set to the latest version

Set to the latest version, the process after entering the editing feature page is similar to creating a feature, you can refer to [Create Features](https://docs.byteplus.com/docs/DataTester/Create-Features).
