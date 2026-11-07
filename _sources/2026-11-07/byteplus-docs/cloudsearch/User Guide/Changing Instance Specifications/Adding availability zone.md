---
title: "Adding availability zone"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/add-availability-zone"
---

Increasing the number of availability zones (AZs) can improve high availability performance. You can add AZ for an existing Cloud Search instance based on your business requirements.

This topic describes how to add availability zone for a single\-AZ instance.

<span id="a7a83074"></span>
## Precautions


* Please backup data in advance to avoid data loss due to failures during instance updating process. For more information, please see [Setting up automatic snapshots](https://docs.byteplus.com/docs/cloudsearch/automatic-snapshots) or [Setting up manual snapshots](https://docs.byteplus.com/docs/cloudsearch/manual-snapshots).

* Adding AZ to an instance normally increases the number of nodes, which incurs additional charges. For more information about the relevant fees, please see [Billable Items](https://docs.byteplus.com/docs/cloudsearch/billing-items).

* The upgrade task of adding AZ instance consists of two processes, namely instance upgrade and data migration. You can view the detailed upgrade process in Task Center. For more information, please see [Viewing task progress](https://docs.byteplus.com/docs/cloudsearch/task-progress).


<span id="f21716b7"></span>
## Prerequisites


* Instance status is Running.

* The dedicated master node is enabled, otherwise the operation to add AZ cannot be performed. For more information about how to enable dedicated master nodes, please see [Adding dedicated master nodes](https://docs.byteplus.com/docs/cloudsearch/adding-master-nodes).


<span id="f869815e"></span>
## Procedure


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the right side of **Instances** page, click the `...` icon in the **Actions** panel, and click **Add availability zone**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44aa9816cac34885bc5a289976093863~tplv-goo7wpa0wc-image.image) </span>

4. In the displayed dialog box, configure the corresponding parameters as listed below, check the box for Terms of Services and then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2837c4cb186447987234e25870181b8~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Deployment method |Currently two\-AZ is supported. |
   |Availability zone |Select another AZ as needed for Backup availability zone with the existing AZ unchanged. |
   |Node number change |When changing from single\-AZ to two\-AZ, the total number of nodes is rounded up to a multiple of 2. If the original number of nodes is already a multiple of 2, the number of nodes does not change. |
   |Agreement |Confirm the SLA and check whether data backup is complete. If not, please click **Backup now** at the top of the dialog box.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If adding AZ without data backup, data loss during the upgrade process will not be included in the service interruption time.</div><br> |
   

5. After successfully submitting the order of adding AZ, switch to **Instances** page to check whether the operation is completed. When the instance status changes from updating to running, the added AZ information will be displayed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b74c474adbba44a99bce3abe11a47058~tplv-goo7wpa0wc-image.image) </span>
