---
title: "Publishing Features"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Publishing-Features"
---

<span id="一、功能简介"></span>
# Introduction to functions

In order to ensure the safety of the release and reduce the risk of going online, FeatureFlag provides a grey release function, which can control the flow from small to large and gradually increase the volume. During the launch process, user feedback and data indicators are observed to ensure the smooth launch of the function. If there is an abnormal quick rollback, reduce the impact surface.

<span id="二、如何使用"></span>
# How to use

<span id="_1-如何发布"></span>
## 1. How to publish


* Entry: Featured version details page, publish button in the upper right corner

* Release process: Confirm release information \- \> closed beta \- \> approval \- \> incremental release

   * Confirm the release information: that is, confirm whether the new value after the change is in line with expectations, you can click to view the DIff before and after the change.

   * Closed beta: Send the new value to users who meet the closed beta conditions (such as channel = test)

      * Please observe the user feedback of the closed beta during the closed beta stage. If there is any problem, cancel the release; if it is confirmed that there is no problem with the closed beta, complete the closed beta and enter the next step.

   * Approval: That is, invite others to review, and after others pass the review, they can enter the next step

   * Incremental release: that is, choose the flow to gradually increase the volume, it is recommended to choose 1% canary, and then gradually increase the volume after observing no abnormal problems

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aed6f6fdc2b24f64a05aa87b2f324ab6~tplv-goo7wpa0wc-image.image) </span>

* Note: If you need to change the closed beta conditions and release process (for example, no closed beta link is required), you can configure it by the app administrator to the release plan settings


<span id="_2-出现问题快速回滚"></span>
## 2. Quick rollback if there is a problem


* If an abnormality is found during the release of a certain version, you can click to roll back this release.

* After rolling back, it will return to (that is, take effect) the previous full version; if there is no full version in history, it will close the Feature and continue to take effect. Local default value.
