---
title: "Imported data dashboard"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-imported_data_dashboard"
---

Once you have imported your Trial, Historical, or Incremental data, whether in **Trial** or **Live Mode**, you can view the data statistics through the imported data dashboard.

<span id="fdb9e662"></span>
# Overview tab

Through the Overview tab, you will be able to view the import status, the date imported, and the number of imported records per data type.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a5153b3faa14403a42fe41345a9c8a4~tplv-goo7wpa0wc-image.image" width="864px" /></div>


<span id="66dd4323"></span>
# Historical data tab

The Historical data tab displays the information about your imported historical data, including the timestamp, number of successful imports, and failed imports.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Historical data tab is only available if you import your data using GCS or Amazon S3.</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb722c126f0f4afb9c904b7dbd899b0c~tplv-goo7wpa0wc-image.image" width="864px" /></div>



|**Number** |**Category** |**Description** |
|---|---|---|
|1 |Timestamp |The timestamp for the User and Product column will record the data importing time while user event data will record the timestamp stored in the data. |
|2 |Data type |Whether it is a User, Product, or User Event. |
|3 |File name |The name of the imported data file. |
|4 |Status |The importing status of the file. There are two statuses:<br><br><br>* Importing.<br><br>* Completed.<br><br><br>In the importing status, you cannot delete or re\-import the data.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The import status for each file will be recorded.</div><br> |
|5 |Successful imports |The number of successful data file imports. |
|6 |Failed imports |The number of unsuccessful data file imports. You can click on the number to view the Sample Error Logs.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/920a290267f44fbcb91db3197a7e65f4~tplv-goo7wpa0wc-image.image) </span> |
|7 |Import data |If you encounter issues with your imported data, you can resolve them by deleting, through the Overview tab, and reimporting the data. This action will ensure that any data on dates that were not deleted remains in the system, automatically undergoing deduplication.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is important to note that once you proceed to incremental data import, historical data cannot be deleted or re\-imported.</div><br> |


For more information on validating and resolving your data errors, refer to the following:


* [Retail Data Validation reports](https://docs.byteplus.com/recommend/docs/data_validation_reports)

* [Editing Retail data threshold settings](https://docs.byteplus.com/recommend/docs/editing_retail_data_threshold_settings)

* [Retail Data Validation error codes](https://docs.byteplus.com/recommend/docs/retail_data_validation_error_codes)
