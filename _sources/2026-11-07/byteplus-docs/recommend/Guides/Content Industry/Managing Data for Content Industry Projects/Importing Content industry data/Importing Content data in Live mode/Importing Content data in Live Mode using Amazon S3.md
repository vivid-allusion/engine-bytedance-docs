---
title: "Importing Content data in Live Mode using Amazon S3"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-importing_content_data_in_live_mode_using_amazon_s3"
---

You can import your historical or incremental data using Google Cloud Services (GCS) in the BytePlus Recommend Console.

<span id="df0114c4"></span>
# Prerequisites

You need to have the following criteria prepared before starting the import process:


* [Amazon S3 Service Account](https://docs.aws.amazon.com/AmazonS3/latest/userguide/setting-up-s3.html).

* Create an [Amazon S3 Bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) for BytePlus Recommend.

* Generate an **AWS AccessKey ID** and **Secret AccessKey**. For more information on AWS key generation, refer [here](https://docs.aws.amazon.com/workspaces-web/latest/adminguide/getting-started-iam-user-access-keys.html).

* Requires minimum 60\-100 days of data prepared.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The dates reflected in the Import data screen reflect the valid period for the required data. If you need to import data for a different time frame, whether more or less than the required period, reach out to the BytePlus Recommend team for assistance   </div>
   

* Format your file according to our requirements.


<span id="18b2c566"></span>
# Data import file format requirements

You have to prepare your files according to our requirements to ensure minimal errors faced during the import process. These requirements differ depending on the type of data you are importing.

The requirements are in the table below:


|**Data Category** |**Data Type** |**File Organization** |**Naming Convention** |
|---|---|---|---|
|Historical |User |Store all the User data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `s3://{created_bucket}/{prefix}/historical/User/{filename.json}.` |
||Content |Store all the Content data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `s3://{created_bucket}/{prefix}/historical/Content/{filename.json}.` |
||UserEvent |Files should be organized **daily** based on the time of user behavior. This means you should organize the data into one file for every 24 hours in the user's timezone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10. Also, ensure that files should not contain data spanning over multiple days.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br>**One JSON file:** <br><br>`s3://{created_bucket}/{prefix}/historical/UserEvent/{date.json}.`<br><br>**Multiple JSON files:** <br><br>`s3://{created_bucket}/{prefix}/historical/UserEvent/{date}/{filename.json}.` |
|Incremental |User |Store all the User data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br><br>* **Data split by day**: `s3://{prefix}/{created_bucket}/incremental/User/{date}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/User/20230801/{filename.json}.`<br><br>* **Data split by hour (24 hours)** : `s3://{prefix}/{created_bucket}/incremental/User/{date}_{hour}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/User/20230801_01/{filename.json}` |
||Content |Store all the Content data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br><br>* **Data split by day**: `s3://{prefix}/{created_bucket}/incremental/Content/{date}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/Content/20230801/{filename.json}.`<br><br>* **Data split by hour (24 hours)** : `s3://{prefix}/{created_bucket}/incremental/Content/{date}_{hour}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/Content/20230801_01/{filename.json}` |
||UserEvent |Files should be organized **daily** based on the time of user behavior. This means you should organize the data into one file for every 24 hours in the user's timezone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10. Also, ensure that files should not contain data spanning over multiple days.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br><br>* **Data split by day**: `s3://{prefix}/{created_bucket}/incremental/UserEvent/{date}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/UserEvent/20230801/{filename.json}.`<br><br>* **Data split by hour (24 hours)** : `s3://{prefix}/{created_bucket}/incremental/UserEvent/{date}_{hour}/{filename.json}.`<br><br>   **Example**: `s3://{prefix}/{created_bucket}/incremental/UserEvent/20230801_01/{filename.json}` |


<span id="904e85de"></span>
# Importing historical data to the console using Amazon S3

Once you have prepared the files according to our requirements, you can proceed to import the trial data into the BytePlus Recommend console.

**To import data to the console using Amazon S3:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Import Historical Data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c31e2c610f943d788ccc0c1d8d4e76d~tplv-goo7wpa0wc-image.image) </span>

   The default import method is GCS.

3. Click the drop\-down menu and select **Amazon S3**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9017a8aaa2924a4fa72a3d5a5974447c~tplv-goo7wpa0wc-image.image) </span>

4. Toggle the **Same credential token for all directory paths** on or off if needed.

5. Enter the **Path Directory** for User data, Content data, and User event data respectively.

6. Click **Select files** for each of the data categories.

   The Select files pop\-up window appears.

7. Select each category's files that you want to import.

8. Click **Import data**.

   The resource configuration and data import process for your historical data begins.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/375ee552add24668986e28918d287315~tplv-goo7wpa0wc-image.image) </span>

   For more information on the data import statuses, refer [here](https://docs.byteplus.com/recommend/docs/importing_retail_industry_data_overview#c45db7fe).

9. Once your data validation report has been generated, click **Next**.

10. Resolve your imported data errors.

   For more information on resolving data errors, refer [here](https://docs.byteplus.com/recommend/docs/data_validation_reports).

   Your historical data import is completed.


<span id="8b290f4e"></span>
# Importing incremental data to the console using Amazon S3

Once you have validated the historical data and resolved the fatal errors according to our requirements, you can proceed to import the incremental data into the BytePlus Recommend console.

**To import incremental data to the console using Amazon S3:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Validate Historical Data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c91ba8154074546b0f8ffb9cfceba6d~tplv-goo7wpa0wc-image.image) </span>

3. Click **Next**.

   The Start incremental data import pop\-up window appears.

4. Click **Start**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After clicking Start, your historical data cannot be imported again.   </div>
   

   The Import Incremental data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/863688cecd9a4c2686832eeaefd8649b~tplv-goo7wpa0wc-image.image) </span>

5. Click the drop\-down menu and select **Amazon S3**.

6. Toggle the **Same credential token for all directory paths** on or off if needed.

7. Enter the **Path Directory** for User data, Content data, and User event data respectively.

8. Click **Select files** for each of the data categories.

   The Select files pop\-up window appears.

9. Select each category's files that you want to import.

10. If necessary, modify the **Sync frequency**.

11. If necessary, modify the **Content type**.

12. Click **Import data**.

   The resource configuration and incremental data import process begins.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd82f097c3e94757b5f9cc480ee4c6b4~tplv-goo7wpa0wc-image.image) </span>

13. Once your data validation report has been generated, click **Next**.

14. Resolve your imported data errors.

   For more information on resolving data errors, refer [here](https://docs.byteplus.com/recommend/docs/data_validation_reports).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3282fc58ac0f42c399fb1cd84ef86157~tplv-goo7wpa0wc-image.image) </span>

   Your incremental data import is completed.
