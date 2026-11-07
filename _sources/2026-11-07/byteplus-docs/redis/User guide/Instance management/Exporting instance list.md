---
title: "Exporting instance list"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/export-instance-list"
---

Cache for Redis allows you to export the instance list. You can filter out target instances based on service requirements and export relevant information about the instances (such as region and specifications) to facilitate instance resource management offline.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg) icon in the upper\-right corner of the page.

   > **tip**

   > You can first filter out target instances based on criteria such as **Instance status**, **Availability zone**, **Version**, **Billing method**, **Tag**, or whether the **Sharding cluster** is enabled in the instance list before exporting.

4. In the pop\-up dialog box, set the following configurations.

   |Parameter |Description |
   |---|---|
   |Export range |Select the export range of the instance list. The following values are supported:<br><br><br>* **Export all data**: Export the specified field data of all instances **under the specified region and project of the current account**.<br><br>* **Export selected data**: Export the specified field data of the selected instances.<br><br>* **Export current search results**: Export the specified field data of the instances that meet the search criteria.<br><br><br>> **tip**<br><br><br>> To select the export range as **Export selected data**, you must select at least one instance in the Instances list.<br> |
   |Exporting list fields |Check the instance information to be exported according to business needs, such as instance running status, availability zone, private address/port, public address/port, tags and so on. |

5. Click **OK**.

   > **tip**

   > After clicking **OK**, the instance list information will be exported as a CSV file and automatically downloaded to your local device via the browser. You can view the file using a text editor.
