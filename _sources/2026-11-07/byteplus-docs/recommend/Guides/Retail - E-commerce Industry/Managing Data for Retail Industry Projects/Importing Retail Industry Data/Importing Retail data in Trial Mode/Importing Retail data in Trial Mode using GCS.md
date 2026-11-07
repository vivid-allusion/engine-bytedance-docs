---
title: "Importing Retail data in Trial Mode using GCS"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-importing_retail_data_in_trial_mode_using-gcs"
---

You can import your trial data using Google Cloud Services (GCS) in the BytePlus Recommend Console.

<span id="ec0c5a5e"></span>
# Prerequisites

You need to have the following criteria prepared before starting the import process:


* [GCS account](https://cloud.google.com/iam/docs/service-accounts-create).

* Create a [GCS Bucket](https://cloud.google.com/storage/docs/creating-buckets) for BytePlus Recommend.

* Assign the **Storage Object Viewer Role** to the created GCS account to ensure that the BytePlus Recommend team can access the data.

* Generate the [JSON keyfile](https://cloud.google.com/iam/docs/keys-create-delete#creating) for the GCS you have created and share it with the BytePlus Recommend team.

* Requires 1\-2 weeks of data prepared.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The dates reflected in the Import data screen reflect the valid period for the required data. If you need to import data for a different time frame, whether more or less than the required period, reach out to the BytePlus Recommend team for assistance   </div>
   

* Format your file according to our requirements.


<span id="91b7d483"></span>
# Data import file format requirements

You have to prepare your files according to our requirements to ensure minimal errors faced during the import process. These requirements differ depending on the type of data you are importing. You can either import a Trial Data file or use 1\-2 weeks of your historical data.

The requirements are in the table below:


|**Data Category** |**Data Type** |**File Organization** |**Naming Convention** |
|---|---|---|---|
|Trial Data |User |Store all the User data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br>`gs://{created_bucket}/{prefix}/trial/User/{filename.json}.` |
||Product |Store all the Product data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br>`gs://{created_bucket}/{prefix}/trial/Product/{filename.json}.` |
||UserEvent |Files should be organized **daily** based on the time of user behavior. This means you should organize the data into one file for every 24 hours in the user's timezone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10. Also, ensure that files should not contain data spanning over multiple days.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br>**One JSON file:** <br><br>`gs://{created_bucket}/{prefix}/trial/UserEvent/{date.json}.`<br><br>**Multiple JSON files:** <br><br>`gs://{created_bucket}/{prefix}/trial/UserEvent/{date}/{filename.json}.` |
|Historical (1\-2 weeks worth) |User |Store all the User data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `gs://{created_bucket}/{prefix}/historical/User/{filename.json}.` |
||Product |Store all the Product data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `gs://{created_bucket}/{prefix}/historical/Product/{filename.json}.` |
||UserEvent |Files should be organized **daily** based on the time of user behavior. This means you should organize the data into one file for every 24 hours in the user's timezone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10. Also, ensure that files should not contain data spanning over multiple days.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br>**One JSON file:** <br><br>`gs://{created_bucket}/{prefix}/historical/UserEvent/{date.json}.`<br><br>**Multiple JSON files:** <br><br>`gs://{created_bucket}/{prefix}/historical/UserEvent/{date}/{filename.json}.` |


<span id="bf244753"></span>
# Importing data to the console using GCS

Once you have prepared the files according to our requirements, you can proceed to import the trial data into the BytePlus Recommend console.

**To import data to the console using GCS:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Configure screen appears.

3. Click **Next**.

   The Import screen appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e05cf990100f4b0e98fa2956eccd8647~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   The default import method is GCS.

4. Toggle the **Same credential token for all directory paths** on or off if needed.

5. Enter the **Path Directory** for User data, Product data, and User event data respectively.

6. Click **Select files** for each of the data categories.

   The Select files pop\-up window appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e84a5bf2de5f4b3cbcaba5831ad4dab7~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

7. Select each category's files that you want to import.

8. Click **Import data**.

   The data import process begins.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d36c948ffc5846208c8672c7132ab8c4~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   For more information on the data import statuses, refer [here](https://docs.byteplus.com/recommend/docs/importing_retail_industry_data_overview#c45db7fe).
