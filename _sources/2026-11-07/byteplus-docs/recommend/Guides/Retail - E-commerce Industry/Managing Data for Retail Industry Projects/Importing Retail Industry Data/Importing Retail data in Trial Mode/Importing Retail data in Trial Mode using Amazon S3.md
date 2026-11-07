---
title: "Importing Retail data in Trial Mode using Amazon S3"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-importing_retail_data_using_amazon_s3"
---

You can import your trial data using Amazon S3 in the BytePlus Recommend Console.

<span id="1381e586"></span>
# Prerequisites

You need to have the following criteria prepared before starting the import process:


* [Amazon S3 Service Account](https://docs.aws.amazon.com/AmazonS3/latest/userguide/setting-up-s3.html).

* Create an [Amazon S3 Bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) for BytePlus Recommend.

* Generate an **AWS AccessKey ID** and **Secret AccessKey**. For more information on AWS key generation, refer [here](https://docs.aws.amazon.com/workspaces-web/latest/adminguide/getting-started-iam-user-access-keys.html).

* Requires 1\-2 weeks of data prepared.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The dates reflected in the Import data screen reflect the valid period for the required data. If you need to import data for a different time frame, whether more or less than the required period, reach out to the BytePlus Recommend team for assistance   </div>
   

* Format your file according to our requirements.


<span id="3d8da3a4"></span>
# Data import file format requirements

You have to prepare your files according to our requirements to ensure minimal errors faced during the import process. These requirements differ depending on the type of data you are importing.

The requirements are in the table below:


|**Data Category** |**Data Type** |**File Organization** |**Naming Convention** |
|---|---|---|---|
|Trial |User |Store all the User data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `s3://{created_bucket}/{prefix}/trial/User/{filename.json}.` |
||Product |Store all the Product data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br>`s3://{created_bucket}/{prefix}/trial/Product/{filename.json}.` |
||UserEvent |Files should be organized **daily** based on the time of user behavior. This means you should organize the data into one file for every 24 hours in the user's timezone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10. Also, ensure that files should not contain data spanning over multiple days.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br>**One JSON file:** <br><br>`s3://{created_bucket}/{prefix}/trial/UserEvent/{date.json}.`<br><br>**Multiple JSON files:** <br><br>`s3://{created_bucket}/{prefix}/trial/UserEvent/{date}/{filename.json}.` |
|Historical (1\-2 weeks worth) |User |Store all the User data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `s3://{created_bucket}/{prefix}/historical/User/{filename.json}.` |
||Product |Store all the Product data into one file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10.</div><br> |Store the user data into one or multiple JSON file(s) following this path: `s3://{created_bucket}/{prefix}/historical/Productg/{filename.json}.` |
||UserEvent |Files should be organized **daily** based on the time of user behavior. This means you should organize the data into one file for every 24 hours in the user's timezone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the file is too big, ensure that the number of files do not exceed 10. Also, ensure that files should not contain data spanning over multiple days.</div><br> |Store the user data into one or multiple JSON file(s) following this path:<br><br>**One JSON file:** <br><br>`s3://{created_bucket}/{prefix}/historical/UserEvent/{date.json}.`<br><br>**Multiple JSON files:** <br><br>`s3://{created_bucket}/{prefix}/historical/UserEvent/{date}/{filename.json}.` |


<span id="fe846805"></span>
# Importing data to the console using Amazon S3

Once you have prepared the files according to our requirements, you can proceed to import the trial data into the BytePlus Recommend console.

**To import data to the console using Amazon S3:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Configure screen appears.

3. Click **Next**.

   The Import screen appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e05cf990100f4b0e98fa2956eccd8647~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   The default import method is GCS.

4. Click the drop\-down menu and select **Amazon S3**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb8942a00997469ba7011958f1ffa898~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

5. Toggle the **Same credential token for all directory paths** on or off if needed.

6. Enter the **Path Directory** for User data, Product data, and User event data respectively.

7. Click **Select files** for each of the data categories.

   The Select files pop\-up window appears.

8. Select each category's files that you want to import.

9. Click **Import data**.

   The data import process begins.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d36c948ffc5846208c8672c7132ab8c4~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   For more information on the data import statuses, refer [here](https://docs.byteplus.com/recommend/docs/importing_retail_industry_data_overview#c45db7fe).
