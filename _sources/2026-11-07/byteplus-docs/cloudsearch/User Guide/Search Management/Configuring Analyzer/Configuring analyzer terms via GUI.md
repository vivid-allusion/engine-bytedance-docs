---
title: "Configuring analyzer terms via GUI"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Configure-analyzer-terms"
---

This topic describes how to manage analyzer terms via front\-end GUI in BytePlus Cloud Search console.

<span id="cc96b7fa"></span>
## Background information

Before configuring analyzer terms, please take note of the following guidelines:


* There are two types of analyzer terms, i.e. main term and stop word:

   * If analysis\-ik is used when creating an index, and the data written that contains the main term, then the index will be created and can be searched by keyword.

   * If IK analysis\-ik is used when creating the index, and the data written that contains the stop word, the stop word will be filtered out from the data.

* Each analyzer term should be listed in a single line. Multiple analyzer terms can be added at one time by listing them in different lines.

* The newly added analyzer terms are not effective immediately and require manual operation to take effect.


<span id="2e12e6c1"></span>
## Add analyzer terms


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Search management \> Analyzer management**.

5. On the **Analyzer management** page, you can add Main term and Stop word.

   
   <Tabs>
   <Tab zoneid="ptLUDGHc5d" title="Add Main term">
   <TabTitle>Add Main term</TabTitle>
   
      1. On the **Terms management** panel of **Main term** page, click **Add Main term**.
   
      2. In the displayed dialog box, enter analyzer terms as needed, and then click **OK**.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/004917f3d1514b45a00574838b1a0cb8~tplv-goo7wpa0wc-image.image) </span>
   
   
   </Tab>
   <Tab zoneid="XB6994UEHD" title="Add Stop word">
   <TabTitle>Add Stop word</TabTitle>
   
      1. On the **Stop word** page, click **Add Stop word** under the **Terms management** tab.
   
      2. In the displayed dialog box, enter stop word as needed, and then click **OK**.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b53574821cfc48a0b18177e9f056ea44~tplv-goo7wpa0wc-image.image) </span>
   
   
   </Tab>
   </Tabs>
   


<span id="03983238"></span>
## Enable analyzer terms

The newly added analyzer terms are in `not effective` status and require manual operation to take effect.

The enable operation is only effective for new indices and new data of existing indices containing the terms. If you want to apply the new analyzer terms to the historical data of existing indices, please perform refresh data operation to recreate the indices. For more information, please see [Refreshing data](https://docs.byteplus.com/docs/cloudsearch/31990).


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Search management \> Analyzer management**.

5. On the **Analyzer management** page, you can enable Main term and Stop word.

   
   <Tabs>
   <Tab zoneid="NoQXeRVFHh" title="Enable Main term">
   <TabTitle>Enable Main term</TabTitle>
   
      1. On the **Terms management** panel of **Main term** page, review the terms in `not effective` status, and then click **Apply all** button.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b03ac352a4f4e7e9d097cfd88e2968d~tplv-goo7wpa0wc-image.image) </span>
   
      2. In the displayed dialog box, view the prompt message, and then click **OK**.
   
   
   </Tab>
   <Tab zoneid="XFR9iUvIel" title="Enable Stop word">
   <TabTitle>Enable Stop word</TabTitle>
   
      1. On the **Terms management** panel of **Stop word** page, review the terms in `not effective` status, and then click **Apply all** button.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c94c6b5388534f33b91ca37a7cc7accc~tplv-goo7wpa0wc-image.image) </span>
   
      2. In the displayed dialog box, enter stop word as needed, and then click **OK**.
   
   
   </Tab>
   </Tabs>
   


<span id="765f5dd6"></span>
## Edit analyzer terms

The analyzer terms created via GUI can be edited. The edited terms are in `not effective` status and require manual operation to take effect.


1. On the **Instances** page, click the name of the desired instance.

2. On the left navigation bar of **Instance details** page, select **Search management \> Analyzer management**.

3. On the **Terms management** panel of **Main term** or **Stop word** page, find the desired analyzer term and click **Edit** in the **Actions** column.

4. In the displayed dialog box, modify the term as needed, and then click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3a578656dd84d2f9b7f91e98ceb7df2~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85a13fe5114f4ecdab452d0382bb730b~tplv-goo7wpa0wc-image.image) </span>


5. (Optional) The edited term is in `not effective` status. Click **Apply all** button and then click **OK** in the displayed dialog box to make the edit operation take effect. For more information, please see [Enable analyzer terms](https://docs.byteplus.com/docs/cloudsearch/31992#03983238).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The edit operation is only effective for new indices and new data of existing indices containing the edited terms. If you want to apply the edited terms to the historical data of existing indices, please perform refresh data operation to recreate the indices. For more information, please see <a href="https://docs.byteplus.com/docs/cloudsearch/31990">Refreshing data</a>.</div>


<span id="e40d8b2e"></span>
## Delete analyzer terms

The analyzer terms created via GUI can be deleted. Since the deleted terms cannot be recovered, please exercise caution with delete operation. The deleted analyzer terms are not effective immediately and require manual operation to take effect.


1. On the **Instances** page, click the name of the desired instance.

2. On the left navigation bar of **Instance details** page, select **Search management \> Analyzer management**.

3. On the **Terms management** panel of **Main term** or **Stop word** page, find the desired analyzer term and click **Delete** in the **Actions** column.

4. In the displayed dialog box, click **OK**.

5. (Optional) The deleted term is in `Delete to take effect` status. Click **Apply all** button and then click **OK** in the displayed dialog box to make the delete operation take effect. For more information, please see [Enable analyzer terms](https://docs.byteplus.com/docs/cloudsearch/31992#03983238).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The delete operation is only effective for new indices and new data of existing indices containing the deleted terms. If you want to apply the deleted terms to the historical data of existing indices, please perform refresh data operation to recreate the indices. For more information, please see <a href="https://docs.byteplus.com/docs/cloudsearch/31990">Refreshing data</a>.</div>
