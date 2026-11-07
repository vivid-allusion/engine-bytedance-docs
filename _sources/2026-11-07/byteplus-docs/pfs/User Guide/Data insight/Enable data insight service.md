---
title: "Enable data insight service"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Enable_Data_Insight_Service"
---

Data Insight Service management allows you to activate and manage file systems that require data insight analysis. This article describes the steps for enabling the Data Insight Service.

<span id="33400877"></span>
## Prerequisites


* You have created a file system. For details, see [Creating a file system](https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system).

* The target file system is not in the expansion state. For more information, see [Expanding a file system](https://docs.byteplus.com/en/docs/pfs/Expanding-a-file-system).


<span id="d1ea7406"></span>
## Steps


1. Log in to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation bar, select **Data Insight** \> **Service Management**.

4. On the **Service Management** page, select the file system you want to analyze, then click **Dashboard** or the **Custom** **task** column’s **Enable**.

   * **Dashboard**: Provides the system’s default dashboards, including **Directory Tree**, **TOP dashboard**, **Capacity dashboard**, and **Hotspot dashboard**. For more information, see [Analysis dashboard](https://docs.byteplus.com/en/docs/pfs/Analysis_dashboard).

      * **Custom** **task**: Data insights policies are used to define detailed metric rules. Data insights tasks are based on policies, specifying execution objectives and methods. You need to enable the **Custom Task** feature before creating data insights tasks. For more information, see [Manage data Insight policies](https://docs.byteplus.com/en/docs/pfs/Manage_data_insight_policies) and [Manage data insight tasks](https://docs.byteplus.com/en/docs/pfs/Manage_Data_Insight_tasks).

5. In the dialog box, click **Enable**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Data Insights analysis features for the corresponding file system are only available after you enable the Data Insights service.   </div>
