---
title: "Business Dimension (Item) Data Access (Local File Upload)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Business_Dimension_Item_Data_Access_Local_File_Upload"
---

If you need to expand the data scope of event analysis through dimensional data, you need to define the business dimension information required by data analytics, and then connect the relevant business dimension data and behavioral data to the DataFinder. After the relevant data is successfully reported, you can query and analyze the dimensional data in the DataFinder. This article shows you how to upload business dimension data by uploading a local CSV file.

<span id="42a30326"></span>
# Limitations and Precautions


* Currently, only SaaS\-cloud native environments support this feature.

* Only users with **Data Access \- Manageable** privileges can use the local upload feature.

* Business dimension data supports multiple updates, and supports the use of local file upload and API reporting to update the reported data in two ways. The value is subject to the latest reported result.


<span id="de912356"></span>
# Prerequisite

You need to plan and create completed items and their associated properties according to business requirements, otherwise the local file will not take effect after uploading.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The business dimension attributes you create must be consistent with the data format of the business dimension data uploaded later, otherwise the corresponding data may not be able to be queried and used normally after the local file is uploaded.</div>


<span id="192c0abc"></span>
# Local file upload item properties


1. After logging in to the DataFinder console, click **Data Management** \> **Data Transmission Service** \> **Data Access** at the top, in the External Data Source tab, find the **local file** method, and click the **Access** button.

2. Configure local upload parameters in the pop\-up sidebar.

   
   |Parameter |Configuration instructions |
   |---|---|
   |data type |Currently only "dimension tables" are supported. |
   |business dimension |Select the created business dimension in the drop\-down box. |
   |Select file |Select the file that needs to be uploaded. You can click Download Template to download a local file template, follow up the sample data in the template and fill in the business dimension data to be uploaded.<br><br>The uploaded file must contain data related to the following items:<br><br><br>* **Associated itemid:**  that is, the dimension id of the business dimension.<br><br>   For example, a product\-related business dimension is created, and the business dimension name is: goods; then the **associated id** is the product id, such as product id1, product id2,...<br><br>* **Associated attribute name:**  the attribute name of the associated business dimension.<br><br>   For example, in the product\-related business dimension, attributes are created: product level category, product sub\-category, product name.<br><br>* **Associated attribute value:**  that is, the value of the associated attribute. Note that the data type of the attribute value here needs to be the same as the data type that was set when the business dimension attribute was created.<br><br><br>You can refer to the following example diagram to check whether your item data to be uploaded is correct.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f2689ef48714e10ab9f8dfdc0c876f4~tplv-goo7wpa0wc-image.image) </span> |
   

3. Check whether the data to be uploaded meets expectations.

   After completing the local file selection, you can view the previewed data to be uploaded on the page, and the interface will display the number of data items that can be uploaded normally. You can judge whether the data to be uploaded meets expectations based on the preview and parsed data.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can focus on whether the data format in the data preview is consistent with the created business dimension attribute data format. If not, the data cannot be queried and used normally after uploading.   </div>
   

4. After confirming that the data is correct, click the **upload** button at the bottom right of the page to start uploading the business dimension data.


<span id="75019562"></span>
# Next steps

<span id="9b20a0d2"></span>
## Next steps: (optional) associate item properties with events


* If you have previously associated the item with the event and only used the local file upload method to update and modify the existing item attribute data, you only need to complete the local file upload operation, and there is no need to associate the item attribute with the event again.

* If you have not previously associated an item with an event, and you are reporting the item data for the first time using a local file upload method, you will also need to associate the item attribute with the event.

   The created item object needs to be associated with an event before it can be used.

   * (Recommended) method 1 Interface association: SaaS\-cloud native environment supports direct configuration of associated event attributes on the **Data Management** \> **Business Dimension** page. This method can flexibly associate items with events. It is recommended to use this method. Please

   * Method 2 Code reporting: When configuring data access, you need to configure the business dimension and the association rules of event data at the same time, that is, configure the item id value of one or more specific items into the properties of the event, through code event tracking, configure the business dimension as the properties of a certain event in the `params`of the event tracking SDK. For details, please refer to the event tracking and event\-related documents of each end, such as [iOS SDK Event Tracking and Properties](https://docs.byteplus.com/docs/DataFinder/iOS_SDK_Event_Tracking_and_Properties), [Android SDK Event Tracking and Properties](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Event_Tracking_and_Properties), [Web/JavaScript SDK Event Tracking and Properties](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Event_Tracking_and_Properties), etc.


<span id="f0e5ad92"></span>
## Next steps: business dimension data analytics

When the data reporting has been completed and the attribute is not disabled. You can use these properties in attribute filtering, grouping, and so on. For the business dimension, we also provide `business dimension analysis`function, which can analyze the business dimension as the main body. For operational guidance on business dimension data analytics,
