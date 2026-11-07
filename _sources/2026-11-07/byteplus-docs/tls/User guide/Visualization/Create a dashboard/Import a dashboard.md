---
title: "Import a dashboard"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Import_dashboard"
---

TLS supports importing dashboards across regions and projects by adding JSON scripts or configuration forms. The new dashboard will retain all the configuration information of the original dashboard. This topic describes the usage limitations and basic operations of an import dashboard.

<span id="3abe6ba3"></span>
## Before you begin


* The source dashboard has been created. For specific operations, see [Create a dashboard](https://docs.byteplus.com/docs/tls/Creating_a_dashboard).

* When importing JSON scripts, you need to obtain the JSON scripts of the dashboard first. For specific operation, please refer to [Dashboard common operations](https://docs.byteplus.com/docs/tls/Managing_dashboards).


<span id="cd8b5430"></span>
## Precautions


* When importing JSON scripts, the JSON file must be less than 5MB.

* Only the import of Byteplus TLS dashboards is supported.


<span id="b687c36d"></span>
## Procedure

<span id="bce75599"></span>
### Import a **dashboard by JSON**


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where TLS is located.

3. In the left\-side navigation pane, choose **Common Functions** \> **Dashboard**.

4. On the **Dashboard** page, choose  **+.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e976a12a715749a58ff652791c16d892~tplv-goo7wpa0wc-image.image) </span>

5. Click **Dashboards imported from JSON files** and then click **Next: configure dashboard**.

6. Complete the following configuration.

   1. Set the basic configuration.

      
      |Parameter |Description |
      |---|---|
      |Dashboard Name |Set the dashboard name. |
      |Target project |The project to which the new dashboard belongs. |
      |Description |Enter a description for the dashboard. |
      

   2. Set the data source configuration.

      TLS supports importing JSON scripts in two ways.

      * Click **Fill in data source** and enter the JSON script.

      * Click **Upload data source** to upload the JSON file.

   3. Replace the log topic.

      The log topic replacement area displays all the source log topics associated with the dashboard, as well as the statistical charts, filters, and variables associated with each log topic. By clicking on specific values, you can view the corresponding names of the statistical charts, filters, and variables.

      If you need to replace the log topic for the statistical charts within a new dashboard, you can select the log topic under the current log project to replace it in the **Replace Topic** column.

7. Click **Create dashboard**.


<span id="b263be8f"></span>
### Import a **dashboard by form**


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where TLS is located.

3. In the left\-side navigation pane, choose **Common Functions** \> **Dashboard**.

4. On the **Dashboard** page, choose  **+.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e976a12a715749a58ff652791c16d892~tplv-goo7wpa0wc-image.image) </span>

5. Click **Import other project dashboards** and then click **Next: configure dashboard**.

6. Complete the following configuration.

   1. Set the basic configuration.

      
      |Parameter |Description |
      |---|---|
      |Source region |The region where the dashboard to be imported is located. |
      |Source project |The project to which the dashboard to import belongs. |
      |Source dashboard |The dashboard to be imported. |
      |Target project |The project to which the new dashboard belongs. |
      |New dashboard name |The name of the new dashboard. |
      

   2. Replace the topic.

      The log topic replacement area displays all the source log topics associated with the dashboard, as well as the statistical charts, filters, and variables associated with each log topic. By clicking on specific values, you can view the corresponding names of the statistical charts, filters, and variables.

      If you need to replace the log topic for the statistical charts within a new dashboard, you can select the log topic under the current log project to replace it in the **Replace Topic** column.

7. Click **Create dashboard**.
