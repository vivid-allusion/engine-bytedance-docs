---
title: "Editing or deleting a branch gateway"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-editing-or-deleting-a-branch-gateway"
---

In the Admin Console, you can edit the basic information of a branch gateway or delete the branch gateways that are no longer needed according to your enterprise's office networking needs.

<span id="a2e40181"></span>
# Instructions for use

Before deleting a branch gateway, please be sure to understand the following instructions for use:


* After the branch gateway is deleted, the relevant branch office can not establish network connections with other branch offices over SealSuite's public cloud.

* If you have enabled the remote office function under the SD\-WAN module, you need to pay attention to the following situations:

   * If you have added multiple branch gateways in the Admin Console, deleting a single branch gateway will not affect the operation of the Cloud Access Gateway and Cloud Application Gateway, which will continue to enable remote access for branch offices that are connected to the public cloud through other running branch gateways. However, if an internal application is deployed to the branch gateway server of a branch office that is connected to the public cloud via the deleted branch gateway, the application is not available for remote access after the relevant branch gateway is deleted in the Admin Console.

   * If there is only one branch gateway in the Admin Console, deleting it will cause the Cloud Access Gateway and Cloud Application Gateway to be deleted altogether. With the Cloud Access Gateway and Cloud Application Gateway being deleted, users cannot remotely access enterprise resources across branch offices.

* Please proceed with caution when deleting a branch gateway, because the branch gateway cannot be restored after being deleted.


<span id="17640dac"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **SD\-WAN** \> **Branch Gateway**.

3. On the **Branch Gateway** page, manage the branch gateways by using the following steps:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7b3de71741849b898d923120002ba87~tplv-goo7wpa0wc-image.image) </span>

   * View basic information of a specific branch gateway, including its operational status, the type of branch gateways, the branch network segment, component\-related information, and more.

   * As shown in area ① of the above screenshot, click **Delete Branch** to delete the branch gateway that is no longer needed.

   * As shown in area ② of the above screenshot, click **Edit** to adjust the basic information of the branch gateway, including **Name**, **Branch Gateway Type**, **Branch Network Segment**, **Bandwidth Speed Limit**, and other related configurations.
