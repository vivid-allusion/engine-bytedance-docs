---
title: "Installing category prediction plugin"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/install-category-prediction-plugin"
---

The newly added category prediction terms take effect only when the `opensearch-intervention` plugin is installed in advance. This topic describes how to install the plugin.

<span id="0ea28bf5"></span>
## Precautions

Installing `opensearch-intervention` plugin results in instance restart. It is recommended to perform this operation during off\-peak hours.

<span id="2ef09718"></span>
## Procedure


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Instance management \> Plugin management**.

5. On the **System built\-in plugin** panel, find the `opensearch-intervention` plugin and click **Install** in the **Actions** column.

6. In the displayed dialog box, view the prompt message, and then click **OK**.

7. View the plugin installing progress.

   When the plugin status changes from **Installing** to **Installed**, it means that the desired plugin is successfully installed and the related functions can be used.


<span id="4bddc8dd"></span>
## Other operations

The manually installed plugins can be uninstalled when it is no longer needed. Since uninstalling plugins result in instance restart, it is recommended to perform this operation during off\-peak hours.

For more information, please see [Uninstalling built-in plugins](https://docs.byteplus.com/docs/cloudsearch/built-in-plugins#e482bd25).
