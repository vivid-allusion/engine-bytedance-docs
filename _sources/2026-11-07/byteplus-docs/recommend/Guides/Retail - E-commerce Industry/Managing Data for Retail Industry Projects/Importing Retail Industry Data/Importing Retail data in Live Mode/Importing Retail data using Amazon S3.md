---
title: "Importing Retail data using Amazon S3"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-importing_retail_data_in_live_mode_using-amazon-s3"
---

You can import your historical or incremental data using Amazon S3 in the BytePlus Recommend Console.

<span id="45786c4e"></span>
# Prerequisites

You need to have the following criteria prepared before starting the import process:


* **Amazon S3 Service Account**.

* Create an **Amazon S3 Bucket** for BytePlus Recommend.

* Generate an **AWS AccessKey ID** and **Secret AccessKey**. For more information on AWS key generation, refer [here](https://docs.aws.amazon.com/workspaces-web/latest/adminguide/getting-started-iam-user-access-keys.html).

* Requires minimum 60\-100 days of data prepared.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The dates reflected in the Import data screen reflect the valid period for the required data. If you need to import data for a different time frame, whether more or less than the required period, reach out to the BytePlus Recommend team for assistance   </div>
   

* Format your file according to our requirements.


<span id="f0427f25"></span>
# Data import file format requirements

You have to prepare your files according to our requirements to ensure minimal errors faced during the import process. These requirements differ depending on the type of data you are importing.

The requirements are in the table below:


|**Data Category** |**Data Type** |**File Organization** |**Naming Convention** |
|---|---|---|---|
|Historical |User |Store all the User data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `s3://{created_bucket}/{prefix}/historical/User/{filename.json}.` |
||Product |Store all the Product data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `s3://{created_bucket}/{prefix}/historical/Product/{filename.json}.` |
||UserEvent |Files should be organized **daily** based on the time of user behavior. This means you should organize the data into one file for every 24 hours in the user's timezone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10. Also, ensure that files should not contain data spanning over multiple days.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br>**One JSON file:** <br><br>`s3://{created_bucket}/{prefix}/historical/UserEvent/{date.json}.`<br><br>**Multiple JSON files:** <br><br>`s3://{created_bucket}/{prefix}/historical/UserEvent/{date}/{filename.json}.` |
|Incremental |User |Store all the User data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br><br>* **Data split by day**: `s3://{prefix}/{created_bucket}/incremental/User/{date}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/User/20230801/{filename.json}.`<br><br>* **Data split by hour (24 hours)** : `s3://{prefix}/{created_bucket}/incremental/User/{date}_{hour}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/User/20230801_01/{filename.json}` |
||Product |Store all the Product data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br><br>* **Data split by day**: `s3://{prefix}/{created_bucket}/incremental/Product/{date}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/Product/20230801/{filename.json}.`<br><br>* **Data split by hour (24 hours)** : `s3://{prefix}/{created_bucket}/incremental/Product/{date}_{hour}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/Product/20230801_01/{filename.json}` |
||UserEvent |Files should be organized **daily** based on the time of user behavior. This means you should organize the data into one file for every 24 hours in the user's timezone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10. Also, ensure that files should not contain data spanning over multiple days.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br><br>* **Data split by day**: `s3://{prefix}/{created_bucket}/incremental/UserEvent/{date}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/UserEvent/20230801/{filename.json}.`<br><br>* **Data split by hour (24 hours)** : `s3://{prefix}/{created_bucket}/incremental/UserEvent/{date}_{hour}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/UserEvent/20230801_01/{filename.json}` |


<span id="125f607a"></span>
# Importing historical data to the console using Amazon S3

Once you have prepared the files according to our requirements, you can proceed to import the historical data into the BytePlus Recommend console.

**To import historical data to the console using Amazon S3:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Import Historical data screen appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb878115a23f49b5bddd08d4044e59fa~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

3. From the Import from drop\-down menu, select **Amazon S3**.

4. Toggle the **Same credential token for all directory paths** on or off if needed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Credential</strong> and <strong>Path Directory</strong> for all data will be imported over from Trial Mode.   </div>
   

5. If the **Credential** or **Path Directory** needs to be modified, use your **Incremental** data's credential and path directory.

6. Click **Select files** for each of the data categories.

   The Select files pop\-up window appears.

7. Select each category's files that you want to import.

8. Click **Import data**.

   The resource configuration and data import process begins.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e815810c51824bd29f5e062c2b57c3e6~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   For more information on the data import statuses, refer [here](https://docs.byteplus.com/recommend/docs/importing_retail_industry_data_overview#c45db7fe).

9. Once your data validation report has been generated, click **Next**.

10. Resolve your imported data errors.

   For more information on resolving data errors, refer [here](https://docs.byteplus.com/recommend/docs/data_validation_reports).

   Your historical data import is completed.


<span id="bb724a53"></span>
# Importing incremental data to the console using Amazon S3

Once you have validated the historical data and resolved the fatal errors according to our requirements, you can proceed to import the incremental data into the BytePlus Recommend console.

**To import incremental data to the console using Amazon S3:** 


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

6. From the Import from drop\-down menu, select **Amazon S3**.

7. Enter the **Path Directory** for User data, Product data, and User event data respectively.

8. Click **Select files** for each of the data categories.

   The Select files pop\-up window appears.

9. Select each category's files that you want to import.

10. If necessary, modify the **Sync frequency**.

11. If necessary, modify the **Content type**.

12. Click **Import data**.

   The resource configuration and incremental data import process begins.

13. Once your data validation report has been generated, click **Next**.

14. Resolve your imported data errors.

   For more information on resolving data errors, refer [here](https://docs.byteplus.com/recommend/docs/data_validation_reports).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f0d91a1101646d7b3f8117c7b564529~tplv-goo7wpa0wc-image.image) </span>

   Your incremental data import is completed.
