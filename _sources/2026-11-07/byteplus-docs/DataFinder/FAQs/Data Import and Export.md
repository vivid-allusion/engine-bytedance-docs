---
title: "Data Import and Export"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Data_Import_and_Export"
---

<span id="db3c196a"></span>
# Data import

<span id="cddcde4e"></span>
## Does the Finder support external data sources?

The external data sources currently supported by DataFinder can be viewed on the console's **Data Management** \> **Data Access** \> **External Data Sources** page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b217eabeb1244c78d2aafd1d99ae333~tplv-goo7wpa0wc-image.image) </span>

Currently supported:


* Access to three\-party platforms Singular, Adjust, Appflyer: When using the advertising monitoring function, it currently supports access to three\-party advertising channel data for advertising monitoring effect analysis.

* Also supports importing CSV data: currently supports importing business dimension data by uploading CSV, see details [Business Dimension (Item) Data Access (Local File Upload)](https://docs.byteplus.com/docs/DataFinder/Business_Dimension_Item_Data_Access_Local_File_Upload).

* Access to WeChat official account data: Currently supports direct access to WeChat official account data for user behavior analysis.


With the iterative development of product functions, the support of actual external data sources is subject to the product interface.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are using a private environment, it also supports the analysis of data from some types of data warehouses and databases; using a SaaS\-like environment, it does not currently support direct docking of data warehouses and databases.</div>


<span id="26b1e8b4"></span>
## Does Finder support importing historical data?

For historical data, it is defined as data from 7 days ago. If the client side time of the data exceeds seven days, it cannot be imported under normal circumstances. If you need to import historical data, you need to add the identity __is_history of the historical data in the custom field of the header, and the attribute value is set to string "true".

<span id="976d884d"></span>
## SaaS\-cloud native cloud hosting version, will importing historical data consume the effect package?

Whether it is MTU or event volume effect package, as long as the imported data is not in this month, it will not be counted in the bill statistics at the end of the month. But the bytehouse consumes storage resources normally.

&nbsp;

&nbsp;

&nbsp;

<span id="0c293464"></span>
# Data export

<span id="5717241b"></span>
## Is data export available?


* Most charts support downloading as Excel files locally. The original data source supports exporting user and device information: including user id, public attributes, etc.; behavioral events: including events, event attributes, etc. You need to contact us to open it before use.


<span id="40943641"></span>
## Does the file downloaded from the finder page use the XSSF Workbook framework?

The files downloaded from the finder page use the Python framework and do not involve the XSSF Workbook framework.

<span id="2dc961e8"></span>
## An error was encountered while downloading the event analysis, prompting "User ID not 1\-dimensional".

This error is due to the duplicate user ID caused by the two column names when downloading duplicate error, you need to let the customer distinguish the show_name of the two user IDs, and change the display name of one of the user IDs. You can use the CSV format because there are problems with the XLSX format.

<span id="8f7dcaaf"></span>
## When downloading data in the scene analysis page, unwanted data was not filtered out normally. What is the reason for downloading or full data?


* Problem description: In scenario analysis, after using Mini Program analysis for page URL filtering, the downloaded data is still full data, which does not meet expectations.

* Solution: The filtering function described in the current document is only effective in the console page query display. When downloading data to the local operation, there is no filter condition, so the full amount of data is downloaded. You can try Event Analytics in Advanced Analytics to configure Mini Program page visits to bypass and view and download filter results by URL properties.


<span id="5eb1aedd"></span>
## Can I program data directly into HIVE?


* not supported

    &nbsp;


<span id="how-many-pieces-of-data-can-user-groups-currently-export"></span>
## How many pieces of data can user groups currently export?

The current limit is 200,000 pieces of data can be exported.

<span id="2f9f9b9e"></span>
## Can the imei of the user device reported by the SDK be exported?

Imei is not warehoused and cannot be exported.

<span id="68d88de6"></span>
## The original data source exports the data the day before, and when will the data file be generated?

It is generated every morning around 9 am.

<span id="7e6e84ff"></span>
## OpenAPI call frequency limit and CSV file cutting

(1) OpenAPI is used 600 times a minute

(2) File cutting: app_launch is the application startup event, a csv, origin_event is the event other than app_launch, 1 CSV, but more than 90M will be cut

<span id="b23aa48d"></span>
## Does the user data output through Webhooks not match the data displayed by the user scrutiny interface?


* Webhooks data output provides raw event data, while the data displayed by the user scrutiny interface is structured data processed by the DataFinder server level, and there will be inconsistencies; in addition, some attribute data is automatically generated by the DataFinder server level according to event attributes and will not appear in the original event, that is, the Webhook data output will not contain such data.

* If you want to obtain data consistent with user scrutiny, you need to use the transaction table export function.
