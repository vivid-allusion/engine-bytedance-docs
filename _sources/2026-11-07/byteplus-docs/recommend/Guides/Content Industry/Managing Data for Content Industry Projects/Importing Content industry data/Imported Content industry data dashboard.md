---
title: "Imported Content industry data dashboard"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-imported_content_industry_data_dashboard"
---

Once you have imported your Trial, Historical, or Incremental data, whether in **Trial** or **Live Mode**, you can view the data statistics through the imported data dashboard.

<span id="c7b187c1"></span>
# Overview tab

Through the Overview tab, you will be able to view the import status, the date imported, and the number of imported records per data type.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bf16d6f4677429893bfe2a204633b45~tplv-goo7wpa0wc-image.image) </span>

<span id="9920fae0"></span>
# Historical data tab

The Historical data tab displays the information about your imported historical data, including the timestamp, number of successful imports, and failed imports.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Historical data tab is only available if you import your data using GCS or Amazon S3.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f1bbd31dc324f239df5900d3cc2b832~tplv-goo7wpa0wc-image.image) </span>


|**Number** |**Category** |**Description** |
|---|---|---|
|1 |Timestamp |The timestamp for the User and Content column will record the data importing time while user event data will record the timestamp stored in the data. |
|2 |Data type |Whether it is a User, Content, or User Event. |
|3 |File name |The name of the imported data file. |
|4 |Status |The importing status of the file. There are two statuses:<br><br><br>* Importing.<br><br>* Completed.<br><br><br>In the importing status, you cannot delete or re\-import the data.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The import status for each file will be recorded.</div><br> |
|5 |Successful imports |The number of successful data file imports. |
|6 |Failed imports |The number of unsuccessful data file imports. You can click on the number to view the Sample Error Logs.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/920a290267f44fbcb91db3197a7e65f4~tplv-goo7wpa0wc-image.image) </span> |
|7 |Import data |If you encounter issues with your imported data, you can resolve them by deleting, through the Overview tab, and reimporting the data. This action will ensure that any data on dates that were not deleted remains in the system, automatically undergoing deduplication.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is important to note that once you proceed to incremental data import, historical data cannot be deleted or re\-imported.</div><br> |


For more information on validating and resolving your data errors, refer to the following:


* [Content Data Validation reports](https://docs.byteplus.com/recommend/docs/content_data_validation_reports)

* [Editing Content data threshold settings](https://docs.byteplus.com/recommend/docs/editing_content_data_threshold_settings)

* [Content Data Validation error codes](https://docs.byteplus.com/recommend/docs/content_data_validation_error_codes)
