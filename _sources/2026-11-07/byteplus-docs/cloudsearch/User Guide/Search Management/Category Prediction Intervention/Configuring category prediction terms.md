---
title: "Configuring category prediction terms"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/configure-category-prediction-terms"
---

Category prediction terms are configured in Cloud Search service to manually intervene the query results and improve the search accuracy.

<span id="0b5a616d"></span>
## Limits

This feature is only available for Cloud Search instances of OpneSearch versions.

<span id="3631d42c"></span>
## Prerequisites


* The instance status is running.

* The `opensearch-intervention` plugin has been installed in advance. For more information, please see [Installing category prediction plugin](https://docs.byteplus.com/docs/undefined/66daa4d74b66d802ff37bfe8).


<span id="2fb90c16"></span>
## Add category prediction terms


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Search management \> Category intervention and prediction**, and click **Add category prediction term**.

5. In the displayed dialog box, enter the **search term**, configure **Field category relevance** and **Correlation**, and then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00817d8f60644ac284b1d8e8d59901e2~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The input box of <strong>Relevance</strong> is used to fill in <strong>term weight</strong>. When the documents match the configured term, the matching score is adjusted according to the term weight value as per the following rules:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If term weight value is greater than 1, the final matching score increases;   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If term weight value equals to 1, the final matching score is not affected by the configured term;   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If term weight value is between 0 and 1, the final matching score decreases.   </div>
   


<span id="b2fe5f30"></span>
## Enable category prediction terms


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Search management \> Category intervention and prediction**.

5. On the term list page, review the terms in `not effective` status, and then click **Apply all** button.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If <code>opensearch-intervention</code> hasn't been installed in advance, a prompt is displayed to inform you to install the plugin. For more information, please see <a href="https://docs.byteplus.com/docs/undefined/66daa4d74b66d802ff37bfe8">Installing category prediction plugin</a>.   </div>
   

6. In the displayed dialog box, view the prompt message, and then click **OK**.


<span id="f6552caf"></span>
## Edit category prediction terms

The category prediction terms can be edited. The edited terms are in `not effective` status and require manual operation to take effect.


1. On the **Instances** page, click the name of the desired instance.

2. On the left navigation bar of **Instance details** page, select **Search management \> Category intervention and prediction**.

3. On the term list page, find the desired term and click **Edit** in the **Actions** column.

4. In the displayed dialog box, modify the term and term weight as needed, and then click **OK**.

5. (Optional) The edited term is in `not effective` status. Click **Apply all** button and then click **OK** in the displayed dialog box to make the edit operation take effect. For more information, please see [Enable category prediction terms](https://docs.byteplus.com/docs/undefined/6703eba958b6d502fbfef311#b2fe5f30).


<span id="5b0039f8"></span>
## Delete category prediction terms

The category prediction terms can be deleted. Since the deleted terms cannot be recovered, please exercise caution with delete operation. The deleted terms are not effective immediately and require manual operation to take effect.


1. On the **Instances** page, click the name of the desired instance.

2. On the left navigation bar of **Instance details** page, select **Search management \> Category intervention and prediction**.

3. On the term list page, find the desired term and click **Delete** in the **Actions** column.

4. In the displayed dialog box, click **OK**.

5. (Optional) The deleted term is in `Delete to take effect` status. Click **Apply all** button and then click **OK** in the displayed dialog box to make the delete operation take effect. For more information, please see [Enable category prediction terms](https://docs.byteplus.com/docs/undefined/6703eba958b6d502fbfef311#b2fe5f30).
