---
title: "Importing Retail data in Live Mode using GCS"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-importing_retail_data_in_live-mode_using_gcs"
---

You can import your historical or incremental data using Google Cloud Services (GCS) in the BytePlus Recommend Console.

<span id="3449df71"></span>
# Prerequisites

You need to have the following criteria prepared before starting the import process:


* **GCS account**.

* Create a **GCS Bucket** for BytePlus Recommend.

* Assign the **Storage Object Viewer Role** to the created GCS account to ensure that the BytePlus Recommend team can access the data.

* Generate the **JSON keyfile** for the GCS you have created and share it with the BytePlus Recommend team.

* Requires minimum 60\-100 days of data prepared.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The dates reflected in the Import data screen reflect the valid period for the required data. If you need to import data for a different time frame, whether more or less than the required period, reach out to the BytePlus Recommend team for assistance   </div>
   

* Format your file according to our requirements.


<span id="94914527"></span>
# Data import file format requirements

You have to prepare your files according to our requirements to ensure minimal errors faced during the import process. These requirements differ depending on the type of data you are importing.

The requirements are in the table below:


|**Data Category** |**Data Type** |**File Organization** |**Naming Convention** |
|---|---|---|---|
|Historical |User |Store all the User data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `gs://{created_bucket}/{prefix}/historical/User/{filename.json}.` |
||Product |Store all the Product data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `gs://{created_bucket}/{prefix}/historical/Product/{filename.json}.` |
||UserEvent |Files should be organized **daily** based on the time of user behavior. This means you should organize the data into one file for every 24 hours in the user's timezone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10. Also, ensure that files should not contain data spanning over multiple days.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br>**One JSON file:** <br><br>`gs://{created_bucket}/{prefix}/historical/UserEvent/{date.json}.`<br><br>**Multiple JSON files:** <br><br>`gs://{created_bucket}/{prefix}/historical/UserEvent/{date}/{filename.json}.` |
|Incremental |User |Store all the User data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br><br>* **Data split by day**: `gs://{prefix}/{created_bucket}/incremental/User/{date}/{filename.json}.`<br><br>   **Example**: `gs://{prefix}/{created_bucket}/incremental/User/20230801/{filename.json}.`<br><br>* **Data split by hour (24 hours)** : `gs://{prefix}/{created_bucket}/incremental/User/{date}_{hour}/{filename.json}.`<br><br>   **Example**: `gs://{prefix}/{created_bucket}/incremental/User/20230801_01/{filename.json}` |
||Product |Store all the Product data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br><br>* **Data split by day**: `gs://{prefix}/{created_bucket}/incremental/Product/{date}/{filename.json}.`<br><br>   **Example**: `gs://{prefix}/{created_bucket}/incremental/Product/20230801/{filename.json}.`<br><br>* **Data split by hour (24 hours)** : `gs://{prefix}/{created_bucket}/incremental/Product/{date}_{hour}/{filename.json}.`<br><br>   **Example**: `gs://{prefix}/{created_bucket}/incremental/Product/20230801_01/{filename.json}` |
||UserEvent |Files should be organized **daily** based on the time of user behavior. This means you should organize the data into one file for every 24 hours in the user's timezone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10. Also, ensure that files should not contain data spanning over multiple days.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br><br>* **Data split by day**: `gs://{prefix}/{created_bucket}/incremental/UserEvent/{date}/{filename.json}.`<br><br>   **Example**: `gs://{prefix}/{created_bucket}/incremental/UserEvent/20230801/{filename.json}.`<br><br>* **Data split by hour (24 hours)** : `gs://{prefix}/{created_bucket}/incremental/UserEvent/{date}_{hour}/{filename.json}.`<br><br>   **Example**: `gs://{prefix}/{created_bucket}/incremental/UserEvent/20230801_01/{filename.json}` |


<span id="4ef5856c"></span>
# Importing historical data to the console using GCS

Once you have prepared the files according to our requirements, you can proceed to import the historical data into the BytePlus Recommend console.

**To import data to the console using GCS:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Data screen appears.

3. Click **Import Data**.

   The Import Historical data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb878115a23f49b5bddd08d4044e59fa~tplv-goo7wpa0wc-image.image) </span>

4. Toggle the **Same credential token for all directory paths** on or off if needed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Credential</strong> and <strong>Path Directory</strong> for all data will be imported over from Trial Mode.   </div>
   

5. If the **Credential** or **Path Directory** needs to be modified, use your **Incremental** data's credential and path directory.

6. Click **Select files** for each of the data categories.

   The Select files pop\-up window appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/276a8db9028f442d912e0f2646eaab49~tplv-goo7wpa0wc-image.image) </span>

7. Select each category's files that you want to import.

8. Click **Import data**.

   The resource configuration and data import process for your historical data begins.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e815810c51824bd29f5e062c2b57c3e6~tplv-goo7wpa0wc-image.image) </span>

   For more information on the data import statuses, refer [here](https://docs.byteplus.com/recommend/docs/importing_retail_industry_data_overview#c45db7fe).

9. Once your data validation report has been generated, click **Next**.

10. Resolve your imported data errors.

   For more information on resolving data errors, refer [here](https://docs.byteplus.com/recommend/docs/data_validation_reports).

   Your historical data import is completed.


<span id="7b40612a"></span>
# Importing incremental data to the console using GCS

Once you have validated the historical data and resolved the fatal errors according to our requirements, you can proceed to import the incremental data into the BytePlus Recommend console.

**To import incremental data to the console using GCS:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Validate Historical Data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6205448459ec44a7b4b8c0d35c0719ce~tplv-goo7wpa0wc-image.image) </span>

3. Click **Next**.

   The Start incremental data import pop\-up window appears.

4. Click **Start**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After clicking Start, your historical data cannot be imported again.   </div>
   

   The Import Incremental data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0247ad7323284f25851d507c3c92dc02~tplv-goo7wpa0wc-image.image) </span>

5. Toggle the **Same credential token for all directory paths** on or off if needed.

6. Enter the **Path Directory** for User data, Product data, and User event data respectively.

7. Click **Select files** for each of the data categories.

   The Select files pop\-up window appears.

8. Select each category's files that you want to import.

9. If necessary, modify the **Sync frequency**.

10. If necessary, modify the **Content type**.

11. Click **Import data**.

   The data import process begins.

12. Once your data validation report has been generated, click **Next**.

13. Resolve your imported data errors.

   For more information on resolving data errors, refer [here](https://docs.byteplus.com/recommend/docs/data_validation_reports).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6ed22b730164ff6babbdace1f29302e~tplv-goo7wpa0wc-image.image) </span>

   Your incremental data import is completed.
