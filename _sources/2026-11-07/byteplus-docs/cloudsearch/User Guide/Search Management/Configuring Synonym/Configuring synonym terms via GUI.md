---
title: "Configuring synonym terms via GUI"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/configure-synonym-terms"
---

This topic describes how to manage synonym terms via front\-end GUI in BytePlus Cloud Search console.

<span id="1c1c8b05"></span>
## Background information

Before configuring synonym terms, please take note of the following guidelines:


* Relevant words of one synonym term should be listed in one line and separated by "," (English comma) or "= \>" without space.

* Different synonym terms should be listed in different lines. The number of words in one line should be within 127.

* Grammar format `AA,BB` means that AA and BB are synonyms, and both will be indexed.

* Grammar format `AA,BB=>CC` means that AA and BB are mapped to CC, and only CC will be indexed.

* The newly added synonym terms are not effective immediately and require manual operation to take effect.


<span id="d3d7967a"></span>
## Add synonym terms


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management**.

5. On the **Synonym management** page, click **Add Synonym** under the **Terms management** tab.

6. In the dialog box of **Add Synonym**, enter one or multiple terms as needed, and then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cd6d5f517504c23a4b9b9fb1b6e2f10~tplv-goo7wpa0wc-image.image) </span>


<span id="fa0df8bb"></span>
## Enable synonym terms

The newly added synonym terms are in `not effective` status and require manual operation to take effect.


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management**.

5. On the **Synonym management** page, review the synonym terms in `not effective` status and click **Apply all** under the **Terms management** tab.

6. In the displayed dialog box, view the prompt message, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tip   </div>
   

* <div data-tips="true" data-tips-type="tip">The <strong>Apply all</strong> operation will generate a dictionary file named <code>SYSTEM_DICTIONARY_SYNONYM.txt</code> which can be viewed in the File management \*\*\*\* tab.</div>


* <div data-tips="true" data-tips-type="tip">The newly enabled synonym terms (the name of <code>filter</code> is <code>default_dynamic_synonym</code>) will be effective in about 2 minutes for both new and existing indices containing the synonyms. For the existing indices, the new synonyms are only effective for the new data. If you want to apply the new synonyms to the historical data of the existing indices, please perform refresh data operation to recreate the indices.</div>



<span id="ed43fcc7"></span>
## Edit synonym terms

The synonym terms created via GUI can be edited. The edited synonym terms are in `not effective` status and require manual operation to take effect.


1. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management**.

2. On the **Terms management** tab of the **Synonym management** page, find the desired synonym and click **Edit** in the **Actions** column.

3. In the dialog box of **Edit Synonym**, add, delete or modify synonyms for the term as needed, and then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/092ecd560d324b8885151074cc8b0310~tplv-goo7wpa0wc-image.image) </span>

4. (Optional) The edited synonym is in `not effective` status. Click **Apply all** button and then click **OK** in the displayed dialog box to make the edit operation take effect.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">The edit operation is only effective for new indices and new data of the existing indices containing the edited synonyms. If you want to apply the new synonyms to the historical data of the existing indices, please perform refresh data operation to recreate the indices. For more information, please see <a href="https://docs.byteplus.com/docs/cloudsearch/31990">Refreshing data</a>.</div>


<span id="8e5cb740"></span>
## Delete synonym terms

The synonym terms created via GUI can be deleted. Since the deleted terms cannot be recovered, please exercise caution with delete operation. The deleted synonym terms are not effective immediately and require manual operation to take effect.


1. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management**.

2. On the **Terms management** tab of the **Synonym management** page, find the desired synonym and click **Delete in** the **Actions** column.

3. In the displayed dialog box, view the prompt message, and then click **OK**.

4. (Optional) The deleted synonym is in `Delete to take effect` status. Click **Apply all** button and then click **OK** in the displayed dialog box to make the delete operation take effect.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">The delete operation is only effective for new indices and new data of the existing indices containing the deleted synonyms. If you want to apply the new synonyms to the historical data of the existing indices, please perform refresh data operation to recreate the indices. For more information, please see <a href="https://docs.byteplus.com/docs/cloudsearch/31990">Refreshing data</a>.</div>
