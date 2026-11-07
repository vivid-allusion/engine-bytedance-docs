---
title: "Executing data refresh"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/refresh-data"
---

Any change operations (including add, edit, delete) to synonym and analyzer terms only effective for the newly created indices and the new data of the existing indices. If you want to apply the updated terms to the historical data of the existing indices, you can refresh the index data using the data refresh feature.

<span id="6ac9a934"></span>
## Procedure


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management** or **Analyzer management**, and then click **Refresh data immediately** on the upper\-right corner of the page.

5. In the displayed dialog box, select the desired indices, enter admin password, and click **OK**.

   The password is configured while creating the instance. If you forget it, you can reset it. For more information, please see [Resetting an access password](https://docs.byteplus.com/en/docs/cloudsearch/resetting-password).


<span id="5a7e9157"></span>
### Viewing data refresh tasks

Once the data refresh operation is executed, the corresponding task record is generated. You can view task details, start time, progress and status in **Task Center** page.
